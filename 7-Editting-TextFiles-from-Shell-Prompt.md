## Editing Text Files from the Shell Prompt

### Objectives
After completing this section, you should be able to:
- Create and edit text files from the command line using the Vim editor.

### Editing Files with Vim
Linux commonly uses text-based files for information and configuration settings, which can be edited using any simple text editor. Vim, an improved version of the vi editor, is a highly configurable and efficient text editor widely used on Linux and UNIX systems.

#### Why Learn Vim?
- **Versatility**: Vim can be used from a text-only shell prompt, allowing editing of configuration files from a terminal window or remote logins through SSH or the Web Console.
- **Availability**: Vim is almost always installed on servers due to its compliance with the POSIX standard. This makes Vim a reliable choice for text editing on various UNIX-like operating systems, including macOS.

#### Starting Vim
Vim can be installed in two ways on Red Hat Enterprise Linux:
- **vim-minimal**: A lightweight installation with core features accessible through the `vi` command.
- **vim-enhanced**: A comprehensive installation with additional features, an online help system, and a tutorial program, accessible through the `vim` command.

Example:
```bash
[user@host ~]$ vim filename
```

**Note**: If `vim-enhanced` is installed, regular users running the `vi` command automatically get the `vim` command instead. This does not apply to root and users with UIDs below 200.

#### Vim Operating Modes
Vim operates in several modes:
- **Command mode**: For navigation and text manipulation (default mode).
- **Insert mode**: For text input (`i` to enter, `Esc` to return to command mode).
- **Visual mode**: For text selection (`v` for character, `Shift+V` for line, `Ctrl+V` for block).
- **Extended command mode**: For commands like saving and quitting (`:` to enter).

**Note**: If unsure about the current mode, press `Esc` a few times to ensure you are in command mode.

#### Basic Vim Workflow
- **Insert mode**: `i` (Enter text, `Esc` to return to command mode).
- **Undo**: `u`
- **Delete a character**: `x`
- **Save file**: `:w`
- **Save and quit**: `:wq`
- **Quit without saving**: `:q!`

#### Rearranging Existing Text
- **Copy and paste** (yank and put):
  - Position the cursor at the start of the text.
  - Enter visual mode and select text.
  - Press `y` to yank the text.
  - Move the cursor to the new location.
  - Press `p` to put the text at the cursor.

#### Visual Mode in Vim
- **Character mode**: `v` (for sentences).
- **Line mode**: `Shift+V` (for entire lines).
- **Block mode**: `Ctrl+V` (for rectangular blocks of text).

**Note**: Master the basic workflow before diving into advanced features. Practice using the core commands to get comfortable with Vim.

### Exercise
Use the `vimtutor` command to learn the core functionality of Vim. This tutorial is included with `vim-enhanced` and is an excellent resource for beginners.

```bash
[user@host ~]$ vimtutor
```

### References
- `vim(1)` and `vi(1)` man pages
