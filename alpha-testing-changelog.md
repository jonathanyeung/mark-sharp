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