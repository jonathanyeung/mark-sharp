# Change Log

## 1.7.1

- Fixes line numbers in code blocks for wrapped lines.
- Mitigates a parsing issue with multiple image elements on the same line that led to a 'Unhandled scenario: image definition spans multiple nodes' error message and prevented the document from loading.
- Fixes some precedence issues with inline code spans. Creating a code span around existing elements such as links or bolded text will revert the inner formatting to plain text.

## 1.7.0

- Revamp of Images:
    - Clicking on an image or focusing on it with the cursor will now show the markdown definition text inline, rather than in a separate text box. This makes the image editing experience closer to that of editing a markdown document.
    - Multiple images on the same line will now properly render side-by-side, provided the window has enough horizontal space.
    - **Breaking Change**: When images on the clipboard are pasted sequentially, the image files will be saved to the workspace with a `image-1.jpg`, `image-2.jpg` format instead of `image (1).jpg`. This formatting is easier to work with in Markdown links.
- Fixes some parsing issues of wikilinks when there are multiple aliased wikilinks on the same line.
- Fixes box shadow styling issues in tables when the table cell editor is focused.
- Fixes an export issue with checked list items that have child elements that would cause child elements such as code blocks to get parsed incorrectly when re-opening the Mark Sharp editor.

## 1.6.2

- The `Mark Sharp: Split View` context menu on Explorer items now only shows up when right clicking on Markdown files and has been moved down the menu order.
- Fixes an issue when parsing wikilinks that have multiple '|' characters in them.
- Fixes an issue when parsing multiple images on a single line.

## 1.6.1

- Upgrades the Mermaid version from `10.9.1` to `11.4.0`. For details, please see the [mermaid-js changelog](https://github.com/mermaid-js/mermaid/releases).
- Improves reliability of cursor position placement when switching editor modes.
- Fixes parsing issues with list indentation level when the lists are indented by tabs.
- Expands the supported language set for syntax highlight in code blocks.

## 1.6.0

### Right to Left Text Mode

This version introduces a right-to-left (RTL) text mode to improve the experience of authoring Markdown documents in RTL languages, such as Arabic, Hebrew, and Persian. When RTL mode is enabled, the text direction will flow from right to left, and the text alignment will be right-aligned. You can toggle RTL mode in several ways:

1. When Mark Sharp is open, run the command `Mark Sharp: Change Text Directionality`.
2. In the status bar on the bottom right, click on 'LTR' (or 'RTL') to toggle between the two modes.

### Fixes

- Fixes an issue where the prompt to select a destination path for an image being pasted from the clipboard would appear multiple times.
- Fixes an issue that prevented images with spaces in the path name while inside a table or HTML block from properly resolving.

## 1.5.1

- Adds a setting for adjusting the font size, `mark-sharp.display.fontSize`. This setting can also be adjusted through two convenience commands when an M# document is open, `mark-sharp.increase-font-size` and `mark-sharp.decrease-font-size` so that keyboard shorcuts can be added to quickly scale the text.
- **Premium feature** - premium users can now customize the fonts in the editor with the setting `mark-sharp.display.fontFamily`.
- Fixes an issue where using relative image paths would cause the image to not render
- Fixes an issue where adding multiple images from the clipboard would overwrite existing files - subsequent files will now incrementing suffixes in the file name.
- Fixes an issue for image paths that had parentheses in the file name.
- Fixes an issue when pasting text inside the image definition text box.

## 1.5.0

**Breaking Change**: The setting `mark-sharp.mermaidTheme` has been renamed to `mark-sharp.display.mermaidTheme` - if you had previously changed this setting, then you'll need to set it again (run `> Preferences: Open User Settings`, search for "Mark Sharp").

### Styling Updates

- A default dark theme is now available to all users. To get editor colors matching those of your favorite VS Code theme, please see [Mark Sharp Premium](https://github.com/jonathanyeung/mark-sharp/blob/main/licensing-and-activation.md).
- **Premium Feature:** Premium users can now switch the theme of their Mark Sharp editor windows among the default light, default dark, and VS Code themes with the `Mark Sharp: Editor Color Theme` command. This command will update the setting `mark-sharp.display.editorTheme`.
- Improves the page layout for docs with wide tables - text within cells will now be wrapped to better fit the screen dimensions. For tables that have a lot of columns, a horizontal scroll bar will appear for the table element. Furthermore, other elements in the document will now wrap properly instead of running the width of the table.
- Fixes a white screen flicker issue that would occur when opening a document in dark mode.
- Cleans up styling in various areas.

### Critical Windows Fix

- Fixes critical text skew issues affecting Windows users (particularly, documents with CRLF line endings) that would sometimes cause characters to move around or line breaks to be inserted in incorrect places.

### Other fixes

- Fixes an initialization error when using Mark Sharp on the web (vscode.dev).
- Improves editing performance for documents with large tables.
- Fixes an issue where adding new line items to an existing list would sometimes add erroneous line breaks.
- Fixes an error when importing a link within a formatted text block.

## 1.4.1

- Fixes an issue that prevented copying/pasting of HTML blocks
- Fixes an issue where deleting a formatted node sometimes led to a webview error (Lexical Error Code 113).

## 1.4.0

### HTML Blocks

HTML blocks are now supported (see the Github Flavored Markdown Spec [Section 4.6](https://github.github.com/gfm/#html-blocks)).

- HTML blocks will now be parsed during document import and exported as a contiguous block.
- Double click on an HTML block to see and edit the HTML definition.
- _Premium Feature:_ Create HTML blocks quickly with a new slash command entry, `/HTML`. Templates have been added to quickly generate a generic block, a centered `<div/>`, and a resized `<img/>`.

**Limitations**:

- Inline HTML elements are not yet fully supported.
- Interleaving Markdown syntax with HTML code is not yet supported (for example, with a `<details>` block) - this is technically not an HTML block as per the GFW spec.

### Other Fixes

- Images in tables will now render properly.
- Fixes code block parsing issues with documents using CRLF line endings (this primarily affects Windows users).
- Fixes `<br>` imports in table cells.

## 1.3.2

- Mermaid Improvements
    - Improves readability with the color theming of Mermaid diagrams.
    - Adds a new setting `mark-sharp.mermaidTheme` that allows you to use Mermaid's default themes. See the [user guide](https://github.com/jonathanyeung/mark-sharp/blob/main/user-guide.md#mermaid-diagrams) for more details.
    - Fixes an issue where the diagram would disappear when making modifications to the diagram definition that wouldn't alter the diagram appearance (i.e., adding a comment).
    - Upgrades the Mermaid library version to `10.9.1`.
- **Behavior Change**: the outline view will no longer auto-minimize even a Mark Sharp editor goes out of focus. This change also fixes an issue where the outline view would sometimes be hidden even when a Mark Sharp editor was in focus.
- Adds a 'Report' button to the notification popup when a webview error is encountered. Clicking on the button will take you to the [bug reporting page](https://github.com/jonathanyeung/mark-sharp/issues/new?assignees=&labels=&projects=&template=bug_report.yaml) of the project Github.
- Fixes an issue when deleting the first character in a formatting element that would cause the editor to freeze.
- Fixes an issue when pasting text that was copied from inside a formatting element.
- Fixes an issue with cursor navigation when pressing Home/End with an Equation element at the start or end of a line, respectively.
- Fixes an issue when a link surrounded by formatting elements would lose its formatting on import.
- Fixes an issue where the cursor would jump to the top the document when switching focus back into VS Code and hovering over a code block.
- Fixes an issue where code block menu details would be visible when the page first loads.

## 1.3.1

- Fixes a regression from `1.3.0` where typing text in a new paragraph created from clicking at the bottom of the document below a table or code block would lead to document skew on export.
- Fixes some code highlighting issues for certain languages, including HTML and XML.
- Fixes an issue where code blocks would still be editable in presentation mode.
- Fixes an issue where if the opening fence of a code block contained spaces in the language definition, the code block would not get parsed.
- Fixes an issue where a header with only a single formatted element child would stay expanded with '#' tags even after losing focus.
- Renames the display name from 'Mark Sharp' to 'Mark Sharp - Markdown Editor'.

## 1.3.0

**New Premium Feature: Presentation Mode**

When presentation mode is enabled, Mark Sharp enters a read-only state and further stream lines the appearance of the document. This mode is useful when you're trying to present or just read your document without editing.

To switch between presentation mode and edit mode, you can either:

1. Click on the M# entry in the [status bar](https://code.visualstudio.com/api/ux-guidelines/status-bar) at the bottom of the VS Code window. When not in presentation mode, the status bar item will display `M#: Edit Mode`.
2. Run the VS Code Command `Mark Sharp: Toggle Presentation Mode`. You can assign a keyboard shortcut of your choice to this command, which makes switching between presentation mode and edit mode a breeze.

When in presentation mode, the following behaviors change:

- The document is no longer editable.
- The light-gray frontmatter text is no longer visible. The title and created header will still be displayed if present in the frontmatter fields.
- Clicking on markdown elements will no longer trigger their unformatted state - for example, clicking on **bold** text won't show its '*' tags, clicking on a header won't show '#' tags.
    - Similarly, clicking on an image won't show its markdown definition below the image
    - Clicking on a Katex element will not expand to its markdown definition.
- Clicking on link, wikilinks, and footnote references will now directly navigate you to the destination in a single-click.
- Mermaid diagrams will display in 'diagram-only' mode.
- Hovering on the edges of a table will not display the '+' signs to add columns and rows.
- The draggable 6-dot icon on the left side no longer shows up.

_Note: this feature is only available in the premium version of Mark Sharp. Please see licensing for details._

**New Outline Panel**

This version introduces an outline panel which displays the headers in the current active Mark Sharp document. This can be found in the [Explorer view](https://code.visualstudio.com/docs/getstarted/userinterface#_explorer-view) when a Mark Sharp document is open.

- Click on a header to scroll to its position in the page
- Hover your mouse over a header to get a quick pop-up preview of the contents at that header
- As you scroll up and down the page, the current header will be highlighted in the panel
- Header sections that have children of a higher heading level can be collapsed

You can re-arrange the position of the outline panel as you like, see [Custom Layout](https://code.visualstudio.com/docs/editor/custom-layout).

_Note: the outline panel is only displayed when a Mark Sharp editor is in focus._

**Other Fixes**

- Adds support for angle brackets in link URI's as per the [CommonMark Spec](https://spec.commonmark.org/0.30/#link-destination).
- When clicking at the bottom of a page that doesn't have a paragraph as the last element (i.e. the document ends in a code block), Mark Sharp adds a paragraph below the last element to make it easy to add more content. However, this sometimes leads to accidentally dirtying the document from stray clicks. Now, the document will no longer be dirtied until you start typing.
- Fixes a parsing issue when typing multiple links or wikilinks on the same line. Previously, only the first link element would get parsed and subsequent typed items would remain as plain text.
- Fixes an issue where modifying a link text from the leading bracket `[` would sometimes lose the changes after becoming unfocused.
- Fixes an edge case where adding to a list which was converted from an existing paragraph via a slash command could lead to a double bullet point issue.

## 1.2.6

- Fixes an issue with lists where importing a list item with no contents would lead to errors
- Fixes a document skew issue that would be caused on save if the user has VS Code settings that change the document save, such as `trimTrailingWhitespace`, `insertFinalNewline`, or `trimFinalNewlines`.
- Fixes and improves the error message popup when webview errors are encountered.

## 1.2.5

- Fixes various issues with lists:
    - Fixes an issue with creating new list items on slash-command-generated lists that led to `insertAfter: list node is not parent of list item node` error messages
    - Fixes export and parsing of nested check lists
    - Fixes Shift+Enter behavior on check lists

## 1.2.4

- Fixes a regression introduced in version `1.2.3` where an imported document can be initialized incorrectly after being edited for the first time by Mark Sharp

## 1.2.3

- Fixes a critical issue where text could get garbled when switching from Mark Sharp to the VS Code editor
- Improves markdown parsing robustness, particularly around lines containing multiple links or wikilinks
- Fixes various table import issues:
    - Rows with fewer columns than the table definition will now parse correctly and be filled with blanks
    - Rows with more columns will get truncated (but a table will still form)
    - Cells with list delimiters such as '-' and '*' will no longer cause parsing exceptions
- Improves table export formatting for cells with double wide characters (such as CJK characters and emojis)
- Improved cursor behavior when editing footnote anchors

## 1.2.2

- Tables pasted from HTML sources will now produce a Markdown table
- Fixes an issue with table editing after paste operations were performed the table
- Fixes a table issue where inserting above the header row or deleting the header row would leave the table with two heading rows or no heading rows, respectively.

## 1.2.1

- Fixes an import/export issue when the last item on a list is empty
- Fixes import parsing of headers with formatted elements
- Fixes the 'Switch Editor Mode' icon color for Dark Themes
- Adds support for formatted elements within table cells - formatted text (bold, italics, highlights, etc.), links, and wikilinks.
- Improves copy paste behavior within table cells

## 1.2.0

- **Support for wikilinks**: wikilinks can link to local files, such as other Markdown files or images. To create a wikilink, surround the name of the note with double brackets, i.e. `my note`. For details, see the [usage guide](https://github.com/jonathanyeung/mark-sharp/blob/main/user-guide.md#wikilinks).
- Added a button in the editor title bar at the top right of a document tab, M→. Clicking this button will run the `Switch Editor Mode` command and toggle between the Mark Sharp editor and VS Code's editor.
- Link text now can contain formatted text such as bold, italics, and inline code. Links would previously parse incorrectly if there was formatted text in the link text.
- Fixed a bug where clicking on a page would occasionally incorrectly add a paragraph at the bottom of the document and steal focus.

## 1.1.0

- **Behavioral Change**: All commands have had their prefixes renamed from 'M#' to 'Mark Sharp' for better discoverability in the command palette (the underlying command ID's remain unchanged, so shortcuts do not need to be updated).
- Added support for same-page header links (i.e., with `#header-1` as the link destination)
- Added support for local links to other files on your file system. This works with both markdown files and any other file that VS Code can open (including code files, .jpg's, etc.)
- Updated Mermaid Library; Added Gitgraph, Mindmap, and Timeline chart types. Additionally, some parsing issues with Mermaid diagrams were addressed.
- Fixed an issue when invoking the 'Split View' command from the command palette.
- Table Improvements:
    - **Behavioral Change**: typing into a cell will replace the text contents; double clicking in a cell before typing will append to the existing contents.
    - Fixed issues with arrow navigation into tables
    - Enter will move the focused cell down one row.
    - Hitting Enter on the final cell will create a new row
    - Fixed some table navigation issues
- List Improvements:
    - Fixed issues with tabbing behavior
    - Fixed issues with mixing list types for sublists
    - Fixed general stability issues
    - Updated list style type themes
- Fixed a few issues with arrow key navigation.
- Clicking at the bottom of a page will place the cursor there, making it easier to add contents after a table, code block, or diagram.

## 1.0.0

Initial Public Release

## 0.0.10

- Removed the logic of automatically setting M# as the default Markdown editor
- Fixed Undo/Redo logic on Windows and Linux
- Fixed an issue where text formatters could cause a crash
- Fixed a cursor jumping issue whenusing nested text formatters
- Improved code block and frontmatter block usability issues:
    - You can now click on a border of code block to select it. Pressing `Backspace` or `Delete` will remove the code block if selected.
    - Fixed some border issues with code blocks.
    - Pasting a copied frontmatter block in the middle of a document will convert it to a regular code block
    - Fixed some layout issues when pasting code blocks.
    - Fixed some shift+Enter behavior issues with back-to-back code blocks.
    - Pasting content into a code block will now properly preserve newline delimitations
- Fixed an issue where sometimes typing after a collapsed header would cause the child contents of the header to be out of order
- Fixed an issue where sometimes text would still be formatted as a header even if the '#' were deleted.
- Fixed a few issues around pressing `Enter` in the middle of a list.

## 0.0.9

- **Upgraded Slash Commands**
    - Revamped the look of the slash command menu
    - Experimenting with sub-menus on Headings and Mermaid Diagram to reduce clutter on the initial menu. Note: you can still type `/h1` to create a heading 1 without needing to navigate the submenus.
    - Re-ordered the initial list of options
    - Added UI hints around `/mxn` table generation
    - Fixed an issue where a mouse pointer could interfere with arrow scrolling of the menu
    - Added a 'No Results' UI feedback item if all possiblities have been filtered. Previously, the menu would automatically close.
- **Improved Markdown Links**
    - There was a usability issue when clicking on a Markdown-formatted link would immediately open the URL _and then_ expand the text, making it hard to modify the link text without also opening it. The behavior has been changed so that if you click on a formatted link, the cursor will first get placed into the text, thus expanding it - you can then click on the now-visible URL if you want to launch the URL, or you can start typing to manipulate the link text. Furthermore, the link text and the `[`, `(` characters are no longer part of the 'a' tag, so manipulating the unformatted link text is easier.
    - Link syntax parsing is much more robust now. For example, adding the missing `]` to `[link text(www.google.com)` will now parse into a link. Previously, the only trigger would be the trailing `)` character.
- **Table Tweaks**:
    - Fixed issue where imported tables would have cells with leading and trailing whitespaces
    - Enhanced styling of table context menu
- **Image Tweaks**:
    - The markdown textbox below an image is no longer expanded by default
    - Fixed a dark theme issue with the cursor in the markdown definition textbox
    - Added a slash command `/image` and a corresponding VS Code command `M#: Insert Image` that inserts an mage from a file picker.
- Updated the logo

## 0.0.8

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

- Switch editor functionality has been consolidated into a single command, which is now called `mark-sharp.switch-editor-mode`, whereas previously two separate commands controlled this behavior
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
- A licensing page has been added (`M#: Manage License`). Activation (or lack thereof) doesn't affect any M# functionality in alpha builds.

## 0.0.6

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

- Initial release
