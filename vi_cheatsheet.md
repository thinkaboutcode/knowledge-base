# Vim (Vi) Cheat Sheet

## Basics

| **Command**  | **Description**                                      |
|--------------|------------------------------------------------------|
| `vi filename` | Open a file in Vim for editing.                      |
| `:w`         | Save the file (write changes).                       |
| `:q`         | Quit Vim.                                             |
| `:wq`        | Save and quit.                                        |
| `:q!`        | Quit without saving changes.                          |
| `:x`         | Save and quit (same as `:wq`).                        |
| `u`          | Undo the last change.                                 |
| `Ctrl + r`   | Redo the last undone change.                          |
| `:e filename`| Open a new file for editing.                          |
| `:w filename`| Save the file with a new name.                        |

## Modes

| **Mode** | **Command**         | **Description**                         |
|----------|---------------------|-----------------------------------------|
| Normal   | `Esc`               | Enter Normal mode (default mode).        |
| Insert   | `i`                 | Enter Insert mode before the cursor.     |
| Insert   | `a`                 | Enter Insert mode after the cursor.      |
| Insert   | `o`                 | Open a new line below and enter Insert mode. |
| Visual   | `v`                 | Enter Visual mode to select text.        |
| Visual   | `V`                 | Enter Visual Line mode to select lines.  |
| Visual   | `Ctrl + v`          | Enter Visual Block mode to select a block of text. |

## Navigation

| **Command** | **Description**                                      |
|-------------|------------------------------------------------------|
| `h`         | Move left (one character).                           |
| `j`         | Move down (one line).                                |
| `k`         | Move up (one line).                                  |
| `l`         | Move right (one character).                          |
| `0`         | Move to the beginning of the line.                   |
| `$`         | Move to the end of the line.                         |
| `w`         | Move to the beginning of the next word.              |
| `b`         | Move to the beginning of the previous word.          |
| `G`         | Go to the end of the file.                           |
| `gg`        | Go to the beginning of the file.                     |
| `:n`        | Go to line `n`.                                      |
| `%`         | Jump to the matching parenthesis, bracket, or brace. |

## Editing

| **Command** | **Description**                                      |
|-------------|------------------------------------------------------|
| `x`         | Delete the character under the cursor.               |
| `dd`        | Delete the current line.                             |
| `dw`        | Delete from the cursor to the end of the word.       |
| `d$`        | Delete from the cursor to the end of the line.       |
| `d0`        | Delete from the cursor to the beginning of the line. |
| `yy`        | Copy (yank) the current line.                        |
| `yw`        | Copy (yank) from the cursor to the end of the word.  |
| `p`         | Paste after the cursor.                              |
| `P`         | Paste before the cursor.                             |
| `r`         | Replace the character under the cursor.              |
| `cw`        | Change the word from the cursor.                     |
| `C`         | Change (replace) the rest of the line.               |
| `u`         | Undo the last change.                                |
| `Ctrl + r`  | Redo the undone changes.                             |

## Search and Replace

| **Command**        | **Description**                                                |
|--------------------|----------------------------------------------------------------|
| `/pattern`         | Search forward for `pattern`.                                  |
| `?pattern`         | Search backward for `pattern`.                                 |
| `n`                | Repeat the search in the same direction.                       |
| `N`                | Repeat the search in the opposite direction.                   |
| `:%s/old/new/g`    | Replace all occurrences of `old` with `new` in the file.       |
| `:%s/old/new/gc`   | Replace all occurrences with confirmation.                     |

## Visual Mode

| **Command**  | **Description**                                      |
|--------------|------------------------------------------------------|
| `v`          | Start visual mode (character-wise selection).        |
| `V`          | Start visual line mode (select whole lines).         |
| `Ctrl + v`   | Start visual block mode (select a block of text).    |
| `y`          | Copy the selected text.                              |
| `d`          | Delete the selected text.                            |
| `>`          | Indent the selected text to the right.               |
| `<`          | Indent the selected text to the left.                |

## Miscellaneous

| **Command**         | **Description**                                           |
|---------------------|-----------------------------------------------------------|
| `.`                 | Repeat the last command.                                  |
| `:r filename`       | Insert the content of `filename` below the cursor.        |
| `:set number`       | Show line numbers.                                        |
| `:set nonumber`     | Hide line numbers.                                        |
| `:set ignorecase`   | Ignore case when searching.                               |
| `:set noignorecase` | Case-sensitive searching.                                 |
| `:syntax on`        | Enable syntax highlighting.                               |
| `:syntax off`       | Disable syntax highlighting.                              |

## Exiting

| **Command** | **Description**                                      |
|-------------|------------------------------------------------------|
| `:w`        | Save the file (write changes).                       |
| `:q`        | Quit Vim.                                            |
| `:wq`       | Save and quit.                                       |
| `:x`        | Save and quit (same as `:wq`).                       |
| `:q!`       | Quit without saving changes.                         |
