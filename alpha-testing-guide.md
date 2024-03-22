# Mark Sharp Alpha Testing Guide

_The extension is referred to as 'M#' in this guide for short_

## Setup

VSIX Download Link: https://mark-sharp.s3.us-west-2.amazonaws.com/mark-sharp-0.0.10.vsix

[Installation Instructions for .VSIX](https://code.visualstudio.com/docs/editor/extension-marketplace#_install-from-a-vsix)

### Additional VS Code setup

==**IMPORTANT!**== Turn off any formatters for Markdown, as this will interfere with the extension:

In your VSCode's `settings.json`, add:

```json
"[markdown]": {
    "editor.defaultFormatter": null,
    "editor.formatOnSave": false
}
```

==**IMPORTANT!**== Make sure you have your notes backed up (via Git or your method of choice) before using Mark#. There's a chance that your notes may get altered in unintentional ways with alpha builds.

## Basic User Guide

M# is intended to be intuitive and discoverable, but there are currently a lot of shortcomings that require more implementation and/or spec'ing.

This app intends to follow [Github Flavored Markdown](https://github.github.com/gfm/), but not all features are implemented yet.

In the meantime, a few words about how to use M#:

M# will register as the default Markdown editor in your VS Code instance when you install it (I may alter this behavior pre-launch). Just open up a `.md` Markdown file in VS Code and it _should_ launch (although there seem to be some cases where VS Code doesn't and falls back to the built-in editor. In this case, you can right-click on a .md file in explorer > Open With... > M#.

The M# editor is a [Custom Text Editor](https://code.visualstudio.com/api/extension-guides/custom-editors#custom-text-editor), so when you hit save with the editor opened, it'll perform those operations on the underlying `.md` file. As you type in the M# editor, the updates will propagate to the underlying file in near-real time.

### Editor Switching

It's convenient to quickly switch between M# and the built-in-editor so that you can take advantage of the viewing/editing pro's of each mode. There's a built in command for this: `Switch Editor Mode`. This is assigned a default shortcut of `cmd+k y` for Mac or `ctrl+k y` for Windows (picked so that it's unlikely to interfere with existing shortcuts). I recommend modifying this shortcut to something easier.

#### Bugs / Limitations

- When switching modes, M# tries to place the cursor in the same position. However, there are a few edge cases where the calculation is incorrect or fails. If M# fails to calculate the cursor position, the cursor will be moved to the end of the document.

### Slash Commands

Slash commands can be triggered by typing '/'. There are basic markdown generation commands available for things like tables, mermaid diagrams, lists, and headers.

The following VSCode equivalent command palette commands are available, more coming later:

- `M#: Insert Mermaid Diagram`
- `M#: Insert Table`
- `M#: Insert Footnote`
- `M#: Insert Image`

### Collapsible Headers

For each header element, there's a collapsible chevron that will appear if you mouse over the area immediately to the left of the header. Click the chevron to toggle the child contents of that header. The fold states will sync up with the VSCode editor if you use the `Switch Editor Mode` command.

### Draggable Blocks

When you mouse over any element in the document, 6 dots will appear in the left column. You can drag elements to reposition them.

#### Bugs / Limitations

- The drop target can be quite small - when dragging an item, a blue line must appear before releasing the mouse click, else the element won't get repositioned.  It's a bit finicky right now - especially when trying to drop an item at the bottom of the document.
- Dragging a group of elements - not implemented yet, but something I want to add later.  For example, dragging an H1 and all its children together as one unit.
- **BUG**: Dragging collapsed headers will cause sections to get out of order.

## Markdown Features

_This section goes through the capabilities and limitations of M# with respect to each Markdown feature._

### Code Blocks, Diagrams

Type "``` " to trigger a code block

- If you're on the last line of a code block, `Shift+Enter` will add a new paragraph below (discoverability improvements TBD)
- If you're on the first line of a code block and the code block is at the top of the page, `Up Arrow` will add a new line above it.
- M# currently supports syntax highlighting on a limited set of languages in code blocks.
- M# supports Mermaid diagrams
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

This just follows Markdown link syntax. Examples:

- Markdown link syntax: [google](www.google.com)
- Raw url: www.google.com

### Images

There are several ways to add images to your document:

1. You can paste an image from your clipboard. 
2. You can also drag and drop an image, but the behavior is currently very finnicky (see bugs section below). 
3. Using the slash command /image or `M#: Insert Image`, you can pick an image from a file picker.

When an image is put into the editor, you'll be prompted for a path. You can also set the setting `mark-sharp.imagePath` to set a default path and avoid the prompt.

#### Bugs / Limitations

- You **must** hold down `shift` **before** starting the drag and until after the drop.

### Tables

You can generate a table by typing |header1|header2| + `space`. You can also generate a table by using a slash command and entering the desired dimensions, for example `/2x3`. A VS Code command also exists, `M#: Insert Table`. The table implementation is still quite raw.

#### Bugs / Limitations

- Text formatting (bold, italics) don't work in table cells

### Footnotes

You can generate footnotes with a slash command `/footnote` or with the VS Code command `M#: Insert Footnote`. Footnotes generated this way will automatically increment, and the reference text will be placed at the bottom of the document.  Furthermore, if a URL is detected on the clipboard, then it'll be used as the footnote text. (This behavior may later prove to be too weird and be removed). ou can also generate a footnote by typing out a matching anchor/reference pair with `[^1]` and on a separate line typing `[^1]: foo`

#### Bugs / Limitations

- Cursor doesn't automatically move to text box once footnote is generated.
- If you manually type out (or modify) the footnote anchor, the parsing logic currently only will trigger when typing a space after the concluding ']'.

### Frontmatter

Typing "---" on the first line of a document will generate a [frontmatter](https://jekyllrb.com/docs/front-matter/) block. Clicking on the faint 'Frontmatter' text at the top of the document will expand the frontmatter for editing; clicking elsewhere in the document will hide it.

M# will also format a Header block for any frontmatter field for `title`, as well as a creation date subtext for a field called `created`. This behavior is currently hardcoded, but I want to make it configurable later (the current behavior is biased towards Dendron).

### Features Not Yet Implemented

- Collapsible sections (`<details/>` blocks) and other raw HTML elements.
- A presentation mode that is read-only that won't cause markdown elements (such as '#', '*', '_') to be expanded and cleans up other unnecessary UI elements.

## Other Notes

- VSCode's diff view gets messed up when diffing a Markdown file with M# registered as the default Markdown editor. If you want to diff a markdown file with the default editor, the only way I've found that you can do it is to temporarily disable M#.

## Issue Reporting / Feedback

2 ways:

1. Open a bug on Github: https://github.com/jonathanyeung/mark-sharp/issues
2. Just shoot me a message.

### Areas of Focus

All bug reports are welcome, but a couple of points of bug reporting and feedback are top of mind:

- Usability and ergonomic feedback of the editor
- Missing markdown features that are important to you
- Bugs where the underlying markdown gets messed up, i.e. text gets garbled. (These are P0 showstopping bugs.)

Thank you!!!