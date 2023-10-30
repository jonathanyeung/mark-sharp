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