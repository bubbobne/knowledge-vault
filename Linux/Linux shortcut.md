---
owner: Daniele Andreis
created: September 2, 2025 – 8:43 AM
updated: 2025-11-06
tags: [linux, terminal, shortcuts, bash, commands]
---

# 🧠 Linux Keyboard Shortcuts  
Quick reference for Bash and Zsh command line editing.  
Most of these shortcuts work in any terminal.

---

## 🏃 Movement

| Action | Shortcut | Description |
|--------|-----------|--------------|
| Move to beginning of line | `Ctrl + A` | Jump to the start of the line |
| Move to end of line | `Ctrl + E` | Jump to the end of the line |
| Move one word left | `Alt + B` | Move to beginning of previous word |
| Move one word right | `Alt + F` | Move to end of next word |
| Swap two characters | `Ctrl + T` | Switch the two characters around cursor |
| Swap two words | `Esc + T` | Swap the order of last two words |

---

## ✏️ Editing

| Action | Shortcut | Description |
|--------|-----------|--------------|
| Delete to start of line | `Ctrl + U` | Cut from cursor to beginning |
| Delete to end of line | `Ctrl + K` | Cut from cursor to end |
| Delete previous word | `Ctrl + W` | Cut the word before the cursor |
| Delete next word | `Alt + D` | Cut the word after the cursor |
| Delete one character | `Ctrl + D` | Delete character under cursor |
| Paste last deleted text | `Ctrl + Y` | Paste what you deleted with U, K, or W |
| Uppercase word | `Alt + U` | Make word uppercase |
| Lowercase word | `Alt + L` | Make word lowercase |
| Capitalize word | `Alt + C` | Capitalize first letter of the word |

---

## 💻 Terminal Control

| Action | Shortcut | Description |
|--------|-----------|--------------|
| Stop current command | `Ctrl + C` | Interrupt running process |
| Suspend process | `Ctrl + Z` | Pause current process (resume with `fg`) |
| Logout / Exit terminal | `Ctrl + D` | Exit if line is empty |
| Clear screen | `Ctrl + L` | Clear terminal output |
| Repeat last command | `!!` | Rerun the most recent command |
| Repeat last command with sudo | `sudo !!` | Run previous command as root |
| Autocomplete | `Tab` | Complete filenames or commands |
| Search command history | `Ctrl + R` | Reverse search through command history |
| Show command history | `history` | List previously used commands |

---

## 🧩 Extra Tips

| Tip | Command / Shortcut | Description |
|-----|--------------------|--------------|
| Reuse last argument | `Alt + .` | Insert last word of previous command |
| Clear command buffer | `Ctrl + C` | Cancels typed command before execution |
| Cancel search | `Ctrl + G` | Exit from history search mode |
| Re-execute nth command | `!<number>` | Example: `!35` runs command #35 from history |
| Repeat matching command | `!<pattern>` | Example: `!ls` reruns last command starting with `ls` |

---

## 🧭 Notes

- Works on **Bash**, **Zsh**, and most modern shells.  
- In Zsh you can enable extended keybindings via:
  ```bash
  bindkey -v       # vi-mode
  bindkey -e       # emacs-mode (default)
