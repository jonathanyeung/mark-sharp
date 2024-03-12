# Mark Sharp

Mark Sharp is a fast, modern Markdown editor for VS Code. With Mark Sharp you can author Markdown quickly with Markdown syntax while still getting the final rendered Markdown state (what-you-see-is-what-you-get).

Mark Sharp is based on [Github Flavored Markdown](https://github.github.com/gfm/) and supports extension features such as tables, Mermaid diagrams, checklists, and more.

## Quick Start

### Installing the Extension

1. _Pre-requisite_: First install [VS Code](https://code.visualstudio.com/) if you haven't already.
2. Install Mark Sharp from the VS Code Extension Store ==link tbd==

### Launching Mark Sharp

There are several ways to launch the M# editor:

1. In the [Explorer](https://code.visualstudio.com/docs/getstarted/userinterface#_explorer) view, **right click** on a Markdown file ( with a `.md` or `.markdown` file extension) > `Open With...` > `M#`.
2. When a markdown file is open in VS Code's default editor, run the command `M#: Switch Editor Mode` from the [command palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).

> _Additional Setup Notes:_
>
> 1. When you edit a markdown file with Mark Sharp, **your existing document layout may be altered**. It is recommended to back up your documents with a version control system like Git or another method of your choice.
> 2. In order for Mark Sharp to work correctly, markdown auto-formatting must be disabled. When you install Mark Sharp, the following lines will be added to your settings.json file:
>
> ```json
> "[markdown]": {
>     "editor.defaultFormatter": null,
>     "editor.formatOnSave": false
> }
> ```

### Setting Mark Sharp as the default Markdown editor

You may optionally set Mark Sharp as your default Markdown editor. To do this, In the [Explorer](https://code.visualstudio.com/docs/getstarted/userinterface#_explorer) view, **right click** on a Markdown file ( with a `.md` or `.markdown` file extension) > `Open With...` > `Configure Default Editor for '.md'...` >  `M#`.

## In Depth Guides

- [In Depth User Guide](./user-guide.md)
- [Telemetry Notice](./telemetry.md)

## Licensing

To unlock the premium features of Mark Sharp, see [obtaining a license](./licensing-and-activation.md). The basic version of Mark Sharp can still fully render Markdown files, but some editing features are limited.

Please read the ==End User License Agreement==

## Acknowledgements

Mark Sharp would not be possible without the following frameworks and libraries. We would like to give special acknowledgement to the following:

==Coming Soon...==

- Lexical
- Mermaid
- Katex

And lastly, thank you to everyone who has supported Mark Sharp, especially those who have helped with testing, filed bugs, and made feature suggestions! This editor is made for you and would not be possible without your help.

==Lookup how Typora did acknowledgements.==