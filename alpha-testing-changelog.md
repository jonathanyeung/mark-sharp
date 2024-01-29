## 0.0.8

[0.0.8 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.8.vsix)

- Fixed a cursor jumping issue when creating a formatting tag in the middle of a line
- Fixed an issue where in some cases, typing a `- ` in the middle of a paragraph would create a list item and delete some text
- Fixed a regression from 0.0.7 where `Switch Editor Mode` wouldn't work sometimes with a newly opened document. Also fixed an issue where `Switch Editor Mode` wouldn't work when the cursor was at the end of a line with trailing whitespace
    - Made an enhancement with `Switch Editor Mode` that will attempt to place the cursor in the same general vertical position of the screen; this makes it a bit easier to find your cursor when switching modes.
- **Performance Fix**: Fixed an issue where pasting a larger block of text _or_ deleting a larger block of text would be very slow, sometimes even crashing M#.
- Fixed some cases where pasting would fail with a "Lexical 113 Error".
- Fixed an issue where when using a VS Code chord shortcut that included a modifier, for example `Cmd + K, Cmd + C`, the trailing letter 'C' would get typed.
- Fixed an issue where if you did an `UNDO` immediately after opening a document, the document would disappear.
- **List Enhancements**
    - Multi-line list items are now handled properly according to the GFW spec:
        - When you're in a list item, press `Shift+Enter` to create a new line within the current list item. You can add other elements as children to a list item - code blocks, quote blocks, etc.
        - Indentation level is now properly imported and exported
    - A lot of ergonomic improvements have been made to largely mimic the experience found in Microsoft Word. Here's a summary of the behavior:
        - `Enter` on an existing list item will create a new list item.
        - `Enter` on a blank list item will outdent one level, or exit the list block if at the top level
        - `Backspace` at the beginning of an list item will delete the list item.
        - `Shift+Enter` will add a new line to the current list item.
        - `Tab` will increase the indentation level, but now with an added restriction that you can only go one level higher than the previous sibling, as Markdown has this restriction.
        - `Shift+Tab` will decrease the indentation level.
        - Typing `- []` or `- [ ]` will create a check list (same behavior as before).
        - You can convert a list type by having the cursor on a list item, and then activate a slash command and selecting your desired list type.
    - Whenever two lists are placed immediately next to each other and are of the same type (numbered, bulleted, or a checklist), they will get merged. You can always separate them at the desired point with `Backspace`.

## 0.0.7

[0.0.7 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.7.vsix)

==**Breaking Change**==: With 0.0.7, you will need to update your keyboard shortcut for the `Switch Editor Mode` command. Please do the following after installing 0.0.7:

1. In VSCode Command Palette: `> Open Default Keyboard Shortcuts (JSON)`.
2. In keybindings.json, delete these two entries if they exist:
    1. `"command": "mark-sharp.go-to-source"`
    2. `"command": "mark-sharp.go-to-wysiwyg"`
3. Also in keybindings.json, update the key binding for `"command": "mark-sharp.switch-editor-mode"` to your desired keystroke.  It used to be `cmd+y` / `ctrl+y` for mac/Windows respectively.

_Explanation_: 0.0.7 consolidates the switch editor mode functionality into a single command, which is now called `mark-sharp.switch-editor-mode`, whereas previously two separate commands controlled this behavior (I titled the two commands the same to hide this fact). Sideloading the app _may_ not remove the existing keybindings, and those commands no longer exist so VS Code will show an error when you press it. I also changed the default from `ctrl+y` to the chord press `ctrl+k y` because I forgot that this is the shortcut for 'Redo' in Windows... I think it's safer to assign it to an obscure keystroke initially and let the user change it themselves.

**Other 0.0.7 Updates**:

- Ctrl/Cmd+B will now properly bold text; Ctrl/Cmd+I will now properly italicize text.
    - **Note 1**: these commands won't do anything (by design) if your cursor highlight spans multiple lines or spans certain non-formattable elements.
    - **Note 2**: these may interfere with your workflow if you already have Cmd+B / I mapped to a VS Code shortcut; you may start accidentally bolding and italicizing your document when trying to trigger your VSCode shortcut action. I'll probably add a setting later to disable these formatting shortcuts.
- Fixed a few theming issues for the inline Katex equation editor that made text hard to read in dark mode.
- Headings can now have formatted text within them; fixed an issue where new-lining in the middle of a header would cause the new line to also have header formatting.
- Code Block Fixes:
    - **Behavioral Change**: Instead of `Ctrl+Enter` exiting a code block when the cursor is on the last line, the key combo is now `Shift+Enter`. As before, `ArrowDown` will also exit a code block when pressed on the last line, even if there isn't a subsequent paragraph.
    - Fixed an issue where pressing `Enter` in an empty code block wouldn't do anything.
    - Some fixes in Frontmatter blocks that would put it in an invalid state
- Quote Block Fixes:
    - Quote blocks can now have nested elements, such as headers, code blocks, and other quote blocks.
    - Improved Quote block ergonomics:
        - `Shift+Enter` will exit a quote block. `Shift+Enter` in the middle of a quote block will split it into two; Shift+Enter on the last line will add an empty paragraph outside the quote block
        - `Enter` inside a quote block will now create a new line within the quote block
        - `ArrowDown` on the last line of a quote block will create an empty paragraph if it doesn't exist
        - If the quote block is at the top of the document, `ArrowUp` on the first line of a quote block will add a line above
    - Fixed a few import/export issues with quote blocks.
    - Improved quote block styling
- Fixed a styling issue where the page would have a scroll bar even if the document was empty. Footnotes will also appear within the viewport if the note height is short enough to allow it.
- Fixed a styling issue where the collapsible header sidebar would be obscured if the page contents was too wide.
- Fixed an issue where using `Shift+Enter` in a normal paragraph would cause the exported Markdown to have unexpected line breaks.
- When both M# and the VS Code editor are visible at the same time, editing on the VS Code side will now push updates to M#. This should prevent any out-of-sync issues with the editors.  Now you can have both views open together and edit on either side - furthermore, the `switch-editor-mode` command will now work in side-by-side mode as well, instead of always re-opening the doc in the existing tab group.
    - **Note**: when the editor pushes an update to M#, M#'s current implementation re-renders the entire document - if you have tables or diagrams, it leads to unsightly flashing; performance may also be slower for large documents.
- A licensing page has been added (`M#: Manage License`). If you're curious or want to test it out, see [instructions here](./licensing-and-activation.md). Activation (or lack thereof) doesn't affect any M# functionality in alpha builds. And when the time comes, all alpha testers will get free licenses :)

## 0.0.6

[0.0.6 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.6.vsix)

- When highlighting a selection, formatted text in the middle of the selection no longer get expanded. If the anchor or focus cursors are inside formatted text, they will continue to be expanded.
- Fixed an issue where `Ctrl/Cmd + A` Select-All wouldn't keep the selection or error out when the document has a code block.
- Slash command improvements:
    - Added icons, cleaned up some styling; menu now reflects the current theme
    - Fixed the 'code' command that generates code blocks
    - Fixed cursor placement issues when using a 'header' command
    - Added an explicit entry for creating a table.  Note: typing a dimension (such as 3x5) can create a table of your desired dimension.
- Theme fixes in checkboxes, tables, quote blocks, and text selection.
- Table improvements:
    - Tables will be neatly formatted when exported in markdown to make columns align.
    - The cell action button (the down chevron icon) has been removed to free up space in the cell.  The same menu can now be accessed with a right click.
    - Clicking near the left edge of the table can now select an entire row; clicking near the top edge of a column will select the entire column. Clicking on the top left corner will select the entire table.
    - Fixed an issue where copying cells from the header and pasting it in a non-header row would cause the non-header row to have the same background shading as the header.
- Fixed a handful of copy / paste errors that were failing to paste and causing 'Minified Lexical Error 113' messages to show up.
- Fixed a theming issue with Mermaid diagrams

## 0.0.5

[0.0.5 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.5.vsix)

- Fixed an issue with cursor placement when switching to the editor while on a blank line
- Fixed some copy paste issues with formatted text
- Fixed the extra 'ghost' line issue that appeared immediately after Frontmatter blocks
- Added Collapsible Headers.
    - For each header element, there's now a collapsible chevron that will appear if you mouse over the area immediately to the left of the header. Click the chevron to toggle the child contents of that header.
    - Switching editor mode will sync the fold status of the headers.
    - I added two convenience commands: `M#: Fold All` and `M#: Unfold All`. These behave exactly like the built-in `Fold All` and `Unfold All` commands, but are available when M# is open. I haven't added additional fold commands (VSCode has a whole slew of them), since you can quickly switch back to the VSCode editor, run fold commands as you wish, then go back to M#, and the fold status will sync over.
    - **Note**: Setting the folding state on the vscode editor side takes a couple hundred milliseconds - so if you jam the 'switch editor' command repeatedly, the folds may get out of the state you expect.
- Persisted cursor position - if you switch between M# tabs, the cursor should remain at its last position for each respective tab.
- Fixed an issue where using a vscode [chord shortcut](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-rules) (for example `ctrl+k, m` / `cmd+k, m`) would type an 'm' character in M#. The code will stop the additional keypress for any chords registered to `ctrl/cmd+k` or `ctrl/cmd+j`, but not others. A follow up is to make his work for all chord shorctcuts of the user.
- Theming fixes
    - Improved dark theme visibility on the table add row/column buttons and the cell context menu button. It's still not perfect yet.
    - Fixed dark theme with mermaid diagrams. I also enhanced the look a little bit to match the current VS Code theme.
    - Improved dark themes around code block menus
- Fixed an issue when there are multiple mermaid diagrams on the same page.
- Fixed an issue here Ctrl+A / Select All would cause a crash. There are still some problematic cases with select-all.

## 0.0.4

[0.0.4 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.4.vsix)

- Fixes critical skew bug around undo/redo. Previously, using undo/redo would likely cause the document offset to get skewed, which in turn caused the document to get garbled.
- Improvements to tables
    - Arrow keys and tabs work much better now when the cell editor is in focus
    - Add/Remove header option has been removed, since markdown tables always have a header
    - Fixed a bug where a table sometimes would get locked by the selection and couldn't be edited
    - Column left/right/center alignments can now be altered in the table context menu and will be properly imported/exported to markdown.
- Fixed an issue with formatted text (bold, italics) where clicking into the middle of a node and then typing would cause weird cursor jumping issues
- Fixed some issues where pressing 'END' wouldn't always move the cursor to the end of the line when formatted text was present
- Improvements to footnotes
    - Introduced a new command `M#: Insert Footnote` and a corresponding slash command that will insert a footnote. Footnote references added this way get placed at the end of a document and the keys will auto-increment. If a URL is detected on the clipboard, then it'll be used as the footnote text. (This behavior may later prove to be too weird and be removed).
    - The footnote anchor will now show the raw syntax `[^1]` when in focus. The key can be edited, which will also update the corresponding reference key. Breaking the footnote anchor pattern will remove the footnote. Some usability issues still exist here, particularly in re-detecting the anchor (you need to type out an additional space after the trailing ']' to trigger it.)
    - Hovering over a footnote anchor will show the reference text
    - Some minor styling enhancements in the footnote section
    - Bug fixes around Enter and deletion/reversion of footnote anchors

## 0.0.3

[0.0.3 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.3.vsix)

- Check boxes in a check list can now be toggled.
- Multi-line quote blocks are now parsed correctly
- Support for Katex, both inline and in blocks.  Inline is triggered with $f(x)$ syntax, while a Katex block can be created by typing `$$ `
- Fixed issue where deleting an opening formatting tag and then re-adding it wasn't reapplying the formatting.
- Added a convenience command for inserting tables: `M#: Insert Table`
- Fixed issue with code block generation when the language had symbols like in "c#" or "c++"
- Fixed gap styling issue when there are consecutive code blocks on a page
- Various fixes around cursor placement when toggling between editor modes
- Fixed issue where empty headers like "### " would disappear and no longer be selectable or editable
- Pressing Home/End keys will now mimic the behavior of VS Code by moving the cursor to the front and end of the line. It will no longer scroll the webview up or down.
- Ctrl+F will now open a Find Widget
- Pressing Shift+Tab anywhere on a 2nd + level list item will now outdent it.
- Typing "-" followed by "[]" or "[ ]" will now convert the bullet list to a check list

## 0.0.2

[0.0.2 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.2.vsix)

- Improvements to cursor behavior:
    - Cursor has an initial placement when an empty markdown file is open.
    - A cursor is added to the end of the document when an existing markdown file is opened.
    - The click target for focusing on the editor now span the page
- An initial prototype of slash commands. Press '/' to activate - there are a limited set of available commands.
- A new convenience command `M#: Insert Mermaid Diagram` that can create mermaid diagrams with basic templates. This functionality is also available in slash commands. Intention is to figure how the feel of Command Palette driven interaction vs. in-line slash command interaction.
- Horizontal Rule support - this can be triggered by typing `***` or `---`.
- Improvements to tables
    - Fixed positioning of '+' buttons to add new rows
    - Fixed an issue where highlighting a table and pressing backspace caused an exception.
    - Pressing Arrow keys while on the top and bottom row of a table can now properly navigate out of the table.
    - General styling cleanup.

## 0.0.1

[0.0.1 Download Link](https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.1.vsix)

- Initial release