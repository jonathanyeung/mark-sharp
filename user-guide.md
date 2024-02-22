# Mark Sharp User Guide

> _Note: Some features mentioned in this guide are only available with a Mark Sharp premium license._

## Installation

See [Quick Start](./README.md#Quick_Start).

## Basics

### Opening a Markdown file with Mark Sharp

There are several ways to launch the M# editor:

1. In the [Explorer](https://code.visualstudio.com/docs/getstarted/userinterface#_explorer) view, **right click** on a Markdown file ( with a `.md` or `.markdown` file extension) > `Open With...` > `M#`. 
2. When a markdown file is open in VS Code's default editor, run the command `M#: Switch Editor Mode` from the [command palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).

### Slash Commands

Trigger slash commands by typing '/' while the cursor is at an empty space. There are markdown generation commands available for things like tables, mermaid diagrams, lists, and headers. Some options are listed below:

| Slash Command | Description                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------ |
| /list         | Insert a new list. You can specify between a numbered list, a bulleted list, or a checked list.  |
| /h1           | Insert an H1 header. You can insert headers of levels 1-6                                        |
| /5x2          | [Premium Feature] Insert a table with 5 rows, 2 columns.                                         |
| /mermaid      | [Premium Feature] Inserts a mermaid diagram, optionally with a pre-configured template           |
| /image        | [Premium Feature] Insert an image into your document                                             |
| /footnote     | [Premium Feature] Insert a footnote into your document. The footnote anchor will auto-increment. |

### Editor Switching

The command `M#: Switch Editor Mode` allows you to quickly switch between M# and the built-in editor so that you can take advantage of the viewing/editing pro's of each mode. This command will place the cursor at the same position so that you can switch modes without losing your context.

This is assigned a default shortcut of `cmd+k y` for Mac or `ctrl+k y` for Windows. This shortcut can be modified to a more convenient key combination of your choosing.

> Note: if a document hasn't yet been edited by Mark Sharp, cursor placement may be inaccurate as the markdown definition may be in a state that Mark Sharp doesn't expect.

### Collapsible Headers

For each header element, there's a collapsible chevron that will appear if you mouse over the area immediately to the left of the header. Click the chevron to toggle the child contents of that header. The fold states will sync up with the VSCode editor if you use the `M#: Switch Editor Mode` command.

### Draggable Blocks

When you mouse over any element in the document, 6 dots will appear in the left column. You can drag elements to reposition them.

## Markdown Features

Markdown elements can be created using familiar Markdown syntax. For example, you can surround a word with `_` to italicize it, or type `#` at the beginning of a line to create an H1 Header.

### Code Blocks

Type "```" to create a code block, or use the slash command `/code`. You can add a language to the code block like "```javascript " to get syntax highlighting.

- If you're on the last line of a code block, `Shift+Enter` will exit the code block and add a new paragraph below.
- If you're on the first line of a code block and the code block is at the top of the page, `Up Arrow` will add a new line above it.
- M# currently supports syntax highlighting on a limited set of languages in code blocks.

### Mermaid Diagrams

_Premium Feature_

M# supports [Mermaid diagrams](https://mermaid.js.org/). To create a mermaid diagram, either use a slash command "/mermaid" or type ```mermaid at the beginning of a line.

### Katex

_Premium Feature_

- Katex blocks and inline equations are supported with `$$` and `$f(x)$` syntax respectively.

### Lists

- Typing "- " or "1. " on a new line will trigger an unordered / ordered list respectively.
- `Enter` on an existing list item will create a new list item.
- `Enter` on a blank list item will outdent one level, or exit the list block if at the top level
- `Backspace` at the beginning of an list item will delete the list item.
- `Shift+Enter` will add a new line to the current list item.
- `Tab` will increase the indentation level, but now with an added restriction that you can only go one level higher than the previous sibling, as Markdown has this restriction.
- `Shift+Tab` will decrease the indentation level.
- Typing `- []` or `- [ ]` will create a check list (same behavior as before).
- You can convert a list type by having the cursor on a list item, and then activate a slash command and selecting your desired list type.

### Links

To create a link, type the display text in [brackets] followed by the address in (parentheses) as per Markdown link syntax. Examples:

- Markdown link syntax: [google](www.google.com)
- Raw url: www.google.com

### Images

_Premium Feature_

There are several ways to add images to your document:

1. You can paste an image from your clipboard. 
2. You can also drag and drop an image directly into your document. Note: you **must** hold down `shift` **before** starting the drag and until after the drop.
3. Using the slash command /image or `M#: Insert Image`, you can pick an image from a file picker.

When an image is put into the editor, you'll be prompted for a path. You can also set the setting `mark-sharp.imagePath` to set a default path and avoid the prompt.

### Tables

_Premium Feature_

You can generate a table by typing |header1|header2| + `space`. You can also generate a table by using a slash command and entering the desired dimensions, for example `/2x3`. A VS Code command also exists, `M#: Insert Table`. 

==right click context menu==

==select all==

### Footnotes

You can generate footnotes with a slash command `/footnote` or with the VS Code command `M#: Insert Footnote`. Footnotes generated this way will automatically increment, and the reference text will be placed at the bottom of the document.  Furthermore, if a URL is detected on the clipboard, then it'll be used as the footnote text. (This behavior may later prove to be too weird and be removed). ou can also generate a footnote by typing out a matching anchor/reference pair with `[^1]` and on a separate line typing `[^1]: foo`.

### Frontmatter

Typing "---" on the first line of a document will generate a [frontmatter](https://jekyllrb.com/docs/front-matter/) block. Clicking on the faint 'Frontmatter' text at the top of the document will expand the frontmatter for editing; clicking elsewhere in the document will hide it.

M# will also format a Header block in an H1 title for a frontmatter field named `title` and a creation date subtext for a field called `created`.

## Commands

## VS Code Commands

Mark Sharp contributes the following VS Code commands. Many of the editing commands are mirrors of options in the slash command menu.

| Command                    | Description                                                                                          |
| -------------------------- | ---------------------------------------------------------------------------------------------------- |
| M#: Switch Editor Mode     | Switches between Mark Sharp and the default VS Code editor, maintaining cursor position.             |
| M#: Insert Mermaid Diagram | Inserts a Mermaid diagram at the current cursor position. A template can be optionally chosen        |
| M#: Insert Table           | Inserts a table; dimensions can be specified                                                         |
| M#: Insert Image           | Insert an image                                                                                      |
| M#: Insert Footnote        | Inserts a footnote at the current cursor position.                                                   |
| M#: Fold All               | Folds all headers in the Mark Sharp editor. Analogous to the built-in 'Fold All' command.            |
| M#: Unfold All             | Unfolds all headers in the Mark Sharp editor. Analogous to the built-in 'Unfold All' command.        |
| M#: Manage License         | Opens the licensing page where you can purchase a license, activate a license key, or deactivate your license. |

## Settings

Settings can be adjusted in VS Code.