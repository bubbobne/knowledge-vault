---
owner: Daniele Andreis
created: November 08, 2025 – 8:43 AM
updated: 2025-11-08
tags: [linux, console]
---

### 1 tldr

```
tldr command_name**Example:**
```

```
tldr ls
```

**Note:** If `tldr` is not installed, you can add it with:

```
sudo apt install tldr   # Debian/Ubuntu
sudo dnf install tldr   # Fedora
brew install tldr       # macOSdata/kriging/params/
```

---

### 2. Command: `bat`

**Description:** Advanced alternative to `cat`, with syntax highlighting and line numbering.
**Usage:**

```
bat filename
```

**Example:**

```
bat script.sh
```

**Note:** If `bat` is not installed, you can add it with:

```
sudo apt install bat    # Debian/Ubuntu
sudo dnf install bat    # Fedora
brew install bat        # macOS
```

---

### 3. Command: `cat`

**Description:** Displays the contents of a file, concatenates multiple files, and shows them as output.
**Usage:**

```
cat filename
```

**Example:**

```
cat file1.txt file2.txt
```

**Note:** Useful for merging multiple files into one:

```
cat file1.txt file2.txt > merged.txt
```

---

### 4. Command: `grep`

**Description:** Searches for a string inside a file or the output of a command.
**Usage:**

```
grep 'word' filename
```

**Example:**

```
grep 'error' log.txt
```

**Note:** To make the search case-insensitive:

```
grep -i 'word' filename
```

You can also use `grep` in a pipeline:

```
cat file.txt | grep 'word'
```

---

### 5. Command: `find`

**Description:** Searches for files and directories based on name, type, size, date, permissions, and more.
**Usage:**

```
find /path -name "filename"
```

**Example:** Searching for a file named "document.txt" in your home directory:

```
find ~ -name "document.txt"
```

**Other useful cases:**

- Find files larger than 100 MB:
    
    ```
    find / -size +100M
    ```
    
- Find and delete temporary files (`.tmp`):
    
    ```
    find /tmp -name "*.tmp" -delete
    ```
    

---

### 6. Command: `xargs`

**Description:** Passes output from one command as arguments to another command.
**Basic usage:**

```
echo "file1.txt file2.txt" | xargs rm
```

👉 Removes `file1.txt` and `file2.txt` by passing them to `rm`.

**Practical example:** Remove all `.log` files found with `find`:

```
find /var/log -name "*.log" | xargs rm
```

**Useful options:**

- **Run multiple processes in parallel:**
    
    ```
    find /var/log -name "*.log" | xargs -P 4 rm
    ```
    
    📌 `-P 4` runs 4 processes in parallel, useful for speeding up operations on many files.
    
- **Handle filenames with spaces correctly:**
    
    ```
    find /var/log -name "*.log" -print0 | xargs -0 rm
    ```
    
    📌 `-print0` and `-0` prevent issues with filenames containing spaces.
    

### 7. Command: `du`

**Description:** Displays the disk usage of files and directories.

### **Basic Usage:**

```bash
du -sh /path/to/directory

```

👉 Shows the total size of the specified directory in a human-readable format.

### **Examples:**

- Check the size of your home folder:
    
    ```bash
    du -sh ~
    ```
    
- Show the size of all subdirectories in the current folder:

```bash
du -sh ~
```

- Show the size of all subdirectories in the current folder:

```bash
du -sh *
```

- Find the largest directories in `/var/log`:

```bash
du -ah /var/log | sort -rh | head -10
```

📌 `-a` includes files, `-h` makes it human-readable, `sort -rh` sorts by size, and `head -10` shows the top 10.**Alternative:**
For a simpler view of disk usage, you can also use:

```bash
df -h
```

### 8. Command: `rsync`

**Description:** Synchronizes files and directories between two locations efficiently.

### **Basic Usage:**

```bash
rsync -av source/ destination/

```

👉 Copies files and directories from `source/` to `destination/` while preserving attributes.

### **Examples:**

- **Sync a local directory to another location:**
    
    ```bash
    rsync -av ~/Documents/ /media/backup/Documents/
    ```
    
- **Sync files to a remote server via SSH:**
    
    ```bash
    rsync -av -e ssh ~/Documents/ user@server:/backup/Documents/
    
    ```
    
- **Delete files in the destination that no longer exist in the source:**
    
    ```bash
    rsync -av --delete ~/Documents/ /media/backup/Documents/
    ```
    
- **Show progress while copying large files:**
    
    ```bash
    rsync -av --progress largefile.iso /media/backup/
    ```
    

### **Explanation of Options:**

- `a` → Archive mode (preserves permissions, timestamps, symbolic links, etc.).
- `v` → Verbose mode (shows detailed output).
- `-delete` → Removes files in the destination that are not in the source.
- `-progress` → Displays progress during transfer.

🚀 **Best use case:** Ideal for backups and efficient file transfers since it only copies changed files.

Let me know if you need modifications! 😊

### 10. Command: `ncdu`

**Description:** A disk usage analyzer with an interactive interface, useful for finding large files and directories.

### **Basic Usage:**

```bash
ncdu

```

👉 Scans the current directory and shows disk usage in an interactive way.

### **Examples:**

- **Analyze a specific directory (e.g., `/home`):**
    
    ```bash
    ncdu /home
    
    ```
    
- **Sort by largest directories/files and navigate interactively:**
    - Use arrow keys to move.
    - Press `Enter` to explore a directory.
    - Press `d` to delete a file or folder directly.

### **Installation (if not installed):**

```bash
sudo apt install ncdu   # Debian/Ubuntu
sudo dnf install ncdu   # Fedora
brew install ncdu       # macOS

```

🚀 **Why use it?** `ncdu` is much faster and easier to use than `du`, especially for interactive file management and cleaning up disk space.

Let me know if you need another command! 😊

### 11. Command: `tmux`

**Description:** A terminal multiplexer that allows you to create, manage, and switch between multiple terminal sessions.

### **Basic Usage:**

```bash
tmux

```

👉 Starts a new `tmux` session where you can run multiple commands in separate panes.

### **Examples:**

- **Create a new session with a name:**
    
    ```bash
    tmux new -s mysession
    
    ```
    
- **Detach from a session (keep it running in the background):**
Press `Ctrl + b`, then `d`
- **List active sessions:**
    
    ```bash
    tmux list-sessions
    
    ```
    
- **Reattach to a session:**
    
    ```bash
    tmux attach -t mysession
    
    ```
    
- **Split the terminal into panes:**
    - Horizontal split: `Ctrl + b`, then `%`
    - Vertical split: `Ctrl + b`, then `"`
- **Switch between panes:**
Press `Ctrl + b`, then arrow keys

### **Installation (if not installed):**

```bash
sudo apt install tmux   # Debian/Ubuntu
sudo dnf install tmux   # Fedora
brew install tmux       # macOS

```

🚀 **Why use it?** `tmux` is great for managing long-running processes, multitasking in the terminal, and working remotely via SSH without losing sessions.

Let me know if you want another command! 😊

### 12. Command: `fzf`

**Description:** A powerful fuzzy finder that helps you search and filter files, directories, or command history interactively.

### **Basic Usage:**

```bash
fzf

```

👉 Opens an interactive search where you can type keywords to filter results in real-time.

### **Examples:**

- **Find and open a file quickly:**
📌 Searches for files interactively and opens the selected one in `nano`.
    
    ```bash
    find . -type f | fzf | xargs nano
    
    ```
    
- **Search through command history:**
📌 Browse and filter your shell history interactively.
    
    ```bash
    history | fzf
    
    ```
    
- **Use `fzf` for directory navigation:**
📌 Lets you navigate directories quickly using fuzzy search.
    
    ```bash
    cd $(find . -type d | fzf)
    
    ```
    

### **Installation (if not installed):**

```bash
sudo apt install fzf   # Debian/Ubuntu
sudo dnf install fzf   # Fedora
brew install fzf       # macOS

```

🚀 **Why use it?** `fzf` is incredibly fast and makes searching files, directories, and command history much more efficient.

### 13. Command: `z` (Jump to frequently used directories)

**Description:** A powerful tool that allows you to quickly jump to directories you have visited often, making navigation much faster.

### **Basic Usage:**

```bash
z folder_name

```

👉 Navigates to the most frequently used directory matching `folder_name`.

### **Examples:**

- **Jump to a frequently used directory (e.g., "projects"):**
📌 Takes you to `/home/user/Documents/projects` if that’s where you often navigate.
    
    ```bash
    z projects
    
    ```
    
- **Jump to a subdirectory without typing the full path:**
📌 Will take you to the most used `dev` folder, even if it's deep in your file system.
    
    ```bash
    z dev
    
    ```
    
- **List directories sorted by usage frequency:**
    
    ```bash
    z -l
    
    ```
    

### 21. Command: `cut`

**Description:** Extracts specific columns or fields from text files or command output.

### **Basic Usage:**

```bash
cut -d' ' -f1 file.txt

```

👉 Extracts the first field from each line in `file.txt`, using a space as the delimiter.

### **Examples:**

- **Extract the first column from a CSV file:**
    
    ```bash
    cut -d',' -f1 data.csv
    
    ```
    
- **Extract characters 1-5 from each line of a file:**
    
    ```bash
    cut -c1-5 file.txt
    
    ```
    
- **Extract usernames from `/etc/passwd` (first field, separated by `:`):**
    
    ```bash
    cut -d':' -f1 /etc/passwd
    
    ```
    
- **Combine with `ls` to show only filenames:**
    
    ```bash
    ls -l | cut -d' ' -f9
    
    ```
    

### **Why use it?**

`cut` is **lightweight, fast, and useful** for processing structured text files or command output when you need to extract specific fields.

Let me know if you want another command! 😉

### 22. Command: `sort`

**Description:** Sorts lines of text in ascending or descending order.

### **Basic Usage:**

```bash
sort file.txt

```

👉 Sorts the lines in `file.txt` in alphabetical order.

### **Examples:**

- **Sort a list numerically:**
📌 Ensures numbers are sorted correctly (`1, 2, 10` instead of `1, 10, 2`).
    
    ```bash
    sort -n numbers.txt
    
    ```
    
- **Sort in reverse order:**
    
    ```bash
    sort -r file.txt
    
    ```
    
- **Sort a CSV file by the second column:**
📌 `t','` sets `,` as the delimiter, `k2` sorts by the second field.
    
    ```bash
    sort -t',' -k2 file.csv
    
    ```
    
- **Remove duplicates while sorting:**
    
    ```bash
    sort -u file.txt
    
    ```
    

### **Why use it?**

`sort` is a simple but powerful tool for organizing data, especially when combined with `uniq`, `cut`, or `awk`.

---

### **Oh My Zsh Alias of the Day: `..` (Move up one directory)**

**Alias:**

```bash
..

```

👉 Moves up one directory (equivalent to `cd ..`).

### **Other useful navigation aliases in Oh My Zsh:**

- `...` → Move up **two** directories (`cd ../..`)
- `....` → Move up **three** directories (`cd ../../..`)
- `.....` → Move up **four** directories (`cd ../../../..`)

💡 **Why use it?**

Saves typing time when navigating directories! 🚀

Let me know if you want another command or alias! 😉

### 23. Command: `uniq`

**Description:** Removes duplicate lines from a sorted file or input.

### **Basic Usage:**

```bash
uniq file.txt

```

👉 Displays `file.txt`, removing consecutive duplicate lines.

### **Examples:**

- **Remove duplicate lines from a file:**
📌 `uniq` works only on consecutive duplicates, so **sort first** to remove all duplicates.
    
    ```bash
    sort file.txt | uniq
    
    ```
    
- **Count occurrences of each unique line:**
📌 The `c` option prefixes each unique line with its count.
    
    ```bash
    sort file.txt | uniq -c
    
    ```
    
- **Ignore case when comparing:**
    
    ```bash
    sort file.txt | uniq -i
    
    ```
    
- **Show only duplicate lines:**
    
    ```bash
    sort file.txt | uniq -d
    
    ```
    
- **Show only unique lines (remove all duplicates):**
    
    ```bash
    sort file.txt | uniq -u
    
    ```
    

### **Why use it?**

`uniq` is useful when processing logs, text files, and datasets where you want to remove or analyze duplicates.

---

### **Oh My Zsh Alias of the Day: `take` (Create & Enter a Directory)**

**Alias:**

```bash
take myfolder

```

👉 Creates a directory named `myfolder` and immediately enters it (`mkdir myfolder && cd myfolder`).

### **Other useful directory-related aliases:**

- `md foo` → Same as `mkdir foo`, but shorter.
- `d` → Lists recent directories you've navigated to.

### 24. Command: `head`

**Description:** Displays the first lines of a file.

### **Basic Usage:**

```bash
head file.txt

```

👉 Shows the first 10 lines of `file.txt`.

### **Examples:**

- **Show the first 20 lines of a file:**
    
    ```bash
    head -n 20 file.txt
    
    ```
    
- **View the beginning of a log file in real-time:**
    
    ```bash
    head -f /var/log/syslog
    
    ```
    
- **Use with `ls` to preview the first few files in a directory:**
    
    ```bash
    ls -lh | head -n 5
    
    ```
    

### **Why use it?**

`head` is useful for quickly inspecting the start of files without opening them completely.

---

### **Oh My Zsh Alias of the Day: `gs` (Git status shortcut)**

**Alias:**

```bash
gst

```

👉 Runs `git status`, showing the current state of your Git repository.

### **Other useful Git aliases:**

- `gcmsg "commit message"` → Shortcut for `git commit -m "commit message"`
- `gco branch_name` → Shortcut for `git checkout branch_name`
- `gp` → Push changes (`git push`)
- `gl` → Show Git log in a compact format

gs open ghostscript

Thanks for sharing the full list of Oh My Zsh Git aliases! Now you can quickly check and use them. Let me know if you need any modifications or explanations about specific aliases.

### **For Today: Standard Linux Command**

### **25. Command: `tail`**

**Description:** Displays the last lines of a file.

### **Basic Usage:**

```bash
tail file.txt

```

👉 Shows the last 10 lines of `file.txt`.

### **Examples:**

- **Show the last 20 lines of a file:**
    
    ```bash
    tail -n 20 file.txt
    
    ```
    
- **Follow a log file in real-time (great for system logs!):**
    
    ```bash
    tail -f /var/log/syslog
    
    ```
    
- **View the last few lines of a large file without loading it completely:**
    
    ```bash
    tail -n 50 largefile.log
    
    ```
    

### **Why use it?**

`tail` is essential for monitoring logs and troubleshooting issues in real-time.

---

### **Oh My Zsh Alias of the Day: `glol`**

**Alias:**

```bash
glol

```

👉 Runs

```bash
git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset'

```

This gives you **a beautiful and structured Git log view** with colors, commit messages, timestamps, and author names.

### **Other useful Git log aliases:**

- `glgg` → `git log --graph` (shows branch structure)
- `glola` → `git log --graph --oneline --all` (compact view of all branches)
- `glog` → `git log --oneline --decorate --graph` (good alternative to `gl`)

💡 **Why use it?**

If you need a **better and readable Git log**, `glol` is much nicer than the default `git log`.

---

### **26. Command: `wc`**

**Description:** Counts the number of **lines, words, and characters** in a file or input.

### **Basic Usage:**

```bash
wc file.txt

```

👉 Displays the number of lines, words, and characters in `file.txt`.

### **Examples:**

- **Count the number of lines in a file:**
    
    ```bash
    wc -l file.txt
    
    ```
    
- **Count the number of words in a file:**
    
    ```bash
    wc -w file.txt
    
    ```
    
- **Count the number of characters in a file:**
    
    ```bash
    wc -c file.txt
    
    ```
    
- **Count lines in multiple files at once:**
    
    ```bash
    wc -l file1.txt file2.txt
    
    ```
    
- **Use `wc` with a pipeline (e.g., count the number of files in a directory):**
📌 This counts how many files and folders are in the current directory.
    
    ```bash
    ls | wc -l
    
    ```
    

### **Why use it?**

`wc` is great for quickly analyzing file contents, counting lines in logs, or checking word counts in text files.

---

### **Oh My Zsh Alias of the Day: `gco` (Git Checkout)**

**Alias:**

```bash
gco branch_name

```

👉 Runs

```bash
git checkout branch_name

```

📌 Quickly switches to an existing Git branch.

### **Other useful Git branch aliases:**

- `gcb my_new_branch` → Creates a new branch and switches to it (`git checkout -b my_new_branch`).
- `gcm` → Switches to the **main** branch (`git checkout main`).
- `gcd` → Switches to the **develop** branch (`git checkout develop`).
- `gcor` → **Checkout with submodules** (`git checkout --recurse-submodules`).

I

---

### **27. Command: `basename`**

**Description:** Extracts the filename from a given path.

### **Basic Usage:**

```bash
basename /home/user/documents/report.pdf

```

👉 Output:

```bash
report.pdf

```

### **Examples:**

- **Get the filename from a full path:**
    
    ```bash
    basename /var/log/syslog
    
    ```
    
    📌 Output: `syslog`
    
- **Remove a specific file extension:**
    
    ```bash
    basename /home/user/photo.jpg .jpg
    
    ```
    
    📌 Output: `photo`
    
- **Use with a script to get only the filename of a passed argument:**
    
    ```bash
    filename=$(basename "$1")
    echo "Processing file: $filename"
    
    ```
    

### **Why use it?**

`basename` is useful in scripts or commands where you need to extract just the filename from a full path.

---

### **Oh My Zsh Alias of the Day: `gcm` (Switch to Main Branch)**

**Alias:**

```bash
gcm

```

👉 Runs

```bash
git checkout $(git_main_branch)

```

📌 Switches to the **main branch** of your Git repository.

### **Other Git branch navigation aliases:**

- `gco branch_name` → Switch to a specific branch (`git checkout branch_name`).
- `gcd` → Switch to the **develop** branch (`git checkout develop`).
- `gcb new_branch` → Create a new branch and switch to it (`git checkout -b new_branch`).

💡 **Why use it?**

It **saves keystrokes** when switching between branches in Git! 🚀

---

### **28. Command: `dirname`**

**Description:** Extracts the directory path from a given file path.

### **Basic Usage:**

```bash
dirname /home/user/documents/report.pdf

```

👉 Output:

```bash
/home/user/documents

```

### **Examples:**

- **Get the directory from a full file path:**
    
    ```bash
    dirname /var/log/syslog
    
    ```
    
    📌 Output: `/var/log`
    
- **Use it inside a script to get the parent directory of a given file:**
    
    ```bash
    dir_path=$(dirname "$1")
    echo "File is located in: $dir_path"
    
    ```
    
- **Combine with `basename` to split full paths:**
    
    ```bash
    filepath="/home/user/photo.jpg"
    echo "Directory: $(dirname "$filepath")"
    echo "Filename: $(basename "$filepath")"
    
    ```
    
    📌 Output:
    
    ```bash
    Directory: /home/user
    Filename: photo.jpg
    
    ```
    

### **Why use it?**

`dirname` is useful when handling file paths in **scripts and automation**, allowing you to extract only the directory part.

---

### **Oh My Zsh Alias of the Day: `gcmsg` (Git Commit with Message)**

**Alias:**

```bash
gcmsg "Commit message"

```

👉 Runs

```bash
git commit -m "Commit message"

```

📌 Quickly commits changes with a message.

### **Other useful Git commit aliases:**

- `gca "Message"` → Commit **all** changes (`git commit -a -m "Message"`)
- `gcam "Message"` → Commit all changes and **sign off** (`git commit -a -s -m "Message"`)
- `gc!` → Amend the last commit (`git commit --amend -v`)

---

### **29. Command: `tee`**

**Description:** Reads input and writes it **both** to a file and standard output (screen).

### **Basic Usage:**

```bash
echo "Hello, world!" | tee output.txt

```

👉 Output (on screen):

```bash
Hello, world!

```

👉 And `output.txt` will contain:

```bash
Hello, world!

```

### **Examples:**

- **Save command output to a file while still displaying it:**
    
    ```bash
    ls -l | tee filelist.txt
    
    ```
    
    📌 Shows the output of `ls -l` on the screen and saves it to `filelist.txt`.
    
- **Append instead of overwriting:**
    
    ```bash
    echo "New log entry" | tee -a log.txt
    
    ```
    
    📌 `-a` appends instead of replacing the file.
    
- **Combine with `sudo` to write protected files:**
    
    ```bash
    echo "127.0.0.1 example.com" | sudo tee -a /etc/hosts
    
    ```
    
    📌 Writes to `/etc/hosts`, even though `sudo echo` alone wouldn’t work.
    

### **Why use it?**

`tee` is useful when **you want to save and see output at the same time**, especially for logs or debugging.

---

### **Oh My Zsh Alias of the Day: `gp` (Git Push)**

**Alias:**

```bash
gp

```

👉 Runs

```bash
git push

```

📌 Pushes your commits to the remote repository.

### **Other useful Git push aliases:**

- `gpf` → **Force push** (`git push --force-with-lease`)
- `ggp` → Push current branch (`git push origin $(git_current_branch)`)
- `gpsup` → Set upstream branch and push (`git push --set-upstream origin $(git_current_branch)`)

💡 **Why use it?**

It **simplifies Git push commands**, reducing typing and errors! 🚀

---

Let me know if you need another command or alias! 😊

### **30. Command: `diff`**

**Description:** Compares the contents of two files line by line.

### **Basic Usage:**

```bash
diff file1.txt file2.txt

```

👉 Shows the differences between `file1.txt` and `file2.txt`.

### **Examples:**

- **Ignore case differences when comparing:**
    
    ```bash
    diff -i file1.txt file2.txt
    
    ```
    
- **Compare files side-by-side (easier to read):**
    
    ```bash
    diff -y file1.txt file2.txt
    
    ```
    
- **Only show differences, not identical lines:**
    
    ```bash
    diff --suppress-common-lines -y file1.txt file2.txt
    
    ```
    
- **Compare directories recursively:**
    
    ```bash
    diff -r dir1 dir2
    
    ```
    
- **Use `diff` for checking changes in system configs:**
    
    ```bash
    diff /etc/default/grub /etc/default/grub.bak
    
    ```
    

### **Why use it?**

`diff` is useful for **tracking file changes, debugging, and merging configurations**.

---

### **Oh My Zsh Alias of the Day: `gst` (Git Status)**

**Alias:**

```bash
gst

```

👉 Runs

```bash
git status

```

📌 Shows the current state of your Git repository, including **staged, unstaged, and untracked files**.

### **Other useful Git status aliases:**

- `gs` → `git status -s` (Short status format)
- `gss` → `git status -s` (Another shortcut)
- `gsb` → `git status -sb` (Short format with branch info)

💡 **Why use it?**

### **32. Command: `chmod`**

**Description:** Changes the permissions of a file or directory.

### **Basic Usage:**

```bash
chmod 755 script.sh

```

👉 Sets **read, write, execute** permissions for the owner and **read, execute** for others.

### **Examples:**

- **Make a script executable for the owner only:**
    
    ```bash
    chmod 700 script.sh
    
    ```
    
- **Give everyone read & write access:**
    
    ```bash
    chmod 666 file.txt
    
    ```
    
- **Remove write permissions for a file (read-only mode):**
    
    ```bash
    chmod 444 file.txt
    
    ```
    
- **Change permissions using symbolic mode:**
    
    ```bash
    chmod u+x script.sh   # Give execute permission to the owner
    chmod g-w file.txt    # Remove write permission for the group
    chmod o+r file.txt    # Give read permission to others
    
    ```
    

### **Why use it?**

`chmod` is essential for **managing file security and access control**.

---

### **Oh My Zsh Alias of the Day: `grh` (Git Reset HEAD)**

**Alias:**

```bash
grh

```

👉 Runs

```bash
git reset HEAD

```

📌 Unstages files but keeps changes in the working directory.

### **Other useful Git reset aliases:**

- `grhh` → **Hard reset** (removes all changes, dangerous!) (`git reset --hard`)
- `gru` → Unstages everything (`git reset --`)
- `gca!` → Amend last commit (`git commit --amend`)

💡 **Why use it?**

It’s **useful when you accidentally `git add` something** but don’t want to commit it yet! 🚀

---

Let me know if you need another command or alias! 😊

---

### **33. Command: `ps`**

**Description:** Displays information about **running processes** on the system.

### **Basic Usage:**

```bash
ps

```

👉 Shows processes in the **current shell/session**.

---

### **More useful forms:**

- **Show all processes for your user:**
    
    ```bash
    ps -u $USER
    
    ```
    
- **Show all processes running on the system (with full details):**
    
    ```bash
    ps aux
    
    ```
    
- **Search for a specific process (e.g., python):**
    
    ```bash
    ps aux | grep python
    
    ```
    
- **Show processes as a tree (useful for parent-child structure):**
    
    ```bash
    ps -ejH
    
    ```
    
    or
    
    ```bash
    ps axjf
    
    ```
    

---

### **Field meanings in `ps aux`:**

- `USER` → the process owner
- `PID` → process ID
- `%CPU` / `%MEM` → CPU/memory usage
- `STAT` → process state
- `COMMAND` → name of the command being run

---

### **Why use it?**

`ps` is essential for **monitoring running jobs**, **debugging scripts**, and **finding processes to kill**.

---

### **Oh My Zsh Alias of the Day: `gds` (Git Diff Staged)**

**Alias:**

```bash
gds

```

👉 Runs

```bash
git diff --staged

```

📌 Shows differences between the **staged changes** and the last commit (i.e., what you’re about to commit).

---

### **Other related Git diff aliases:**

- `gd` → Show unstaged changes
- `gdca` → Compare staged and committed
- `gdup` → Compare with upstream
- `gdv` → View diff in `vim`
- `gdw` → Word-level diff

💡 **Why use it?**

Helps ensure your **commit only includes what you want**, especially when staging files manually! 🚀

---

Let me know if you want another command or a deeper dive into `ps` or `git diff` options! 😊

### **34. Command: `kill`**

**Description:** Sends a signal to a process—most commonly used to **terminate** it.

---

### ✅ **Basic Usage:**

```bash
kill PID

```

👉 Sends the default `SIGTERM` (terminate) signal to the process with the given PID (process ID).

---

### 🛠️ **Examples:**

- **Find and kill a process by name (combined with `ps` and `grep`):**
    
    ```bash
    ps aux | grep myscript.py
    kill 12345           # Replace 12345 with actual PID
    
    ```
    
- **Forcefully kill a process (SIGKILL):**
    
    ```bash
    kill -9 12345
    
    ```
    
    📌 `-9` sends `SIGKILL`, which immediately stops the process without cleanup.
    
- **Gracefully stop all processes by name:**
    
    ```bash
    pkill myscript
    
    ```
    
    📌 `pkill` is an easier alternative to `kill` when you know the process name.
    
- **Kill all processes for a user (use with caution!):**
    
    ```bash
    pkill -u username
    
    ```
    

---

### 🔄 **Check Available Signals:**

```bash
kill -l

```

👉 Lists all possible signals (like `SIGTERM`, `SIGINT`, `SIGHUP`, `SIGKILL`, etc.)

---

### 💡 **Why use it?**

`kill` is essential for **managing or stopping misbehaving processes**—especially useful when something hangs or consumes too many resources.

---

### **Oh My Zsh Alias of the Day: `gpf` (Git Push Force with Lease)**

**Alias:**

```bash
gpf

```

👉 Runs

```bash
git push --force-with-lease

```

📌 Safely force-push changes to your branch without overwriting others' commits.

---

### 🔁 Related Aliases:

- `gpf!` → `git push --force` (dangerous!)
- `ggp` → Push current branch
- `gpsup` → Push and set upstream

💡 **Why use it?**

Use `gpf` to rewrite Git history (e.g. after `git commit --amend`) while avoiding the risks of `--force`.

---

Let me know if you want a `killall`, `pkill`, or `xkill` deep dive next! 🚀

### **35. Command: `which`**

**Description:** Tells you **which executable** is run when you type a command.

---

### ✅ **Basic Usage:**

```bash
which ls

```

👉 Output:

```bash
/bin/ls

```

📌 Shows the **full path** of the command being executed.

---

### 🛠️ **Examples:**

- **Find out where Python is installed:**
    
    ```bash
    which python3
    
    ```
    
- **Check if a program is available in your `PATH`:**
    
    ```bash
    which git
    
    ```
    
    📌 If it prints nothing, the command is **not installed or not in your PATH**.
    
- **See which version of a command is being run (helpful if you installed multiple):**
    
    ```bash
    which node
    
    ```
    

---

### 🧠 **Why use it?**

Great for **debugging path issues**, understanding **which version** of a tool is being used, or ensuring a script uses the right interpreter (e.g., Python, Bash).

---

### **Oh My Zsh Alias of the Day: `gcb` (Git Checkout Branch)**

**Alias:**

```bash
gcb new-branch

```

👉 Runs

```bash
git checkout -b new-branch

```

📌 Creates a new Git branch and switches to it in one step.

---

### 🧠 Related Git aliases:

- `gco` → `git checkout branch-name`
- `gcm` → `git checkout main`
- `gcd` → `git checkout develop`

💡 **Why use it?**

Fast way to start a **new feature branch** without typing the full `git checkout -b`.

---

Let me know if you want the next command to be a networking tool, file tool, or shell utility! 😊

### **36. Command: `env`**

**Description:** Displays the current **environment variables** or runs a command in a modified environment.

---

### ✅ **Basic Usage:**

```bash
env

```

👉 Shows a list of all environment variables (like `PATH`, `HOME`, `USER`, etc.).

---

### 🛠️ **Examples:**

- **See your current environment (good for debugging):**
    
    ```bash
    env
    
    ```
    
- **Run a command with a temporary environment variable:**
    
    ```bash
    env VAR=value command
    
    ```
    
    Example:
    
    ```bash
    env DEBUG=1 python script.py
    
    ```
    
- **Check the value of a single environment variable (alternative):**
    
    ```bash
    echo $PATH
    
    ```
    
- **Clear all environment variables and run a command (careful!):**
    
    ```bash
    env -i bash
    
    ```
    
    📌 `-i` starts a clean shell without any environment variables.
    

---

### 🧠 **Why use it?**

Great for **debugging**, understanding **how your shell is configured**, and **testing programs with custom variables** (e.g., API keys, config flags).

---

### **Oh My Zsh Alias of the Day: `glg` (Git Log with Stats)**

**Alias:**

```bash
glg

```

👉 Runs:

```bash
git log --stat

```

📌 Shows each commit with a summary of **files changed, insertions, deletions**.

---

### 🔁 Related aliases:

- `glgp` → `git log --stat -p` (adds diff)
- `glgga` → `git log --graph --decorate --all`
- `glog` → Compact, colored graph view of Git history

💡 **Why use it?**

Perfect to **see what each commit modified** without showing the full diff

---

### **Oh My Zsh Alias of the Day: `gpoat`**

**Alias:**

```bash
gpoat
```

👉 Runs:

```bash
git push origin --all && git push origin --tags
```

📌 Pushes **all branches** and **all tags** to the remote.

---

### 🧠 Related aliases:

- `gp` → Push current branch
- `ggp` → `git push origin $(current_branch)`
- `gpf` → Force push with lease

### **38. Command: `history`**

**Description:** Displays the list of **commands you've previously executed** in your current shell session.

---

### ✅ **Basic Usage:**

```bash
history
```

👉 Shows all the commands you've run, with numbered entries.

---

### 🛠️ **Examples:**

- **Show the last 10 commands:**
- `history | tail -10`
- **Repeat a specific command from history by its number:**
- `!123`
    
    📌 Re-executes command number 123 from the history list.
    
- **Search your history for a keyword (e.g., "ssh"):**
- `history | grep ssh`
- **Clear your command history (⚠️ irreversible):**
- `history -c`
- **Save history immediately (not just at session end):**
- `history -a`

---

### 🧠 Pro Tip for Zsh & Oh My Zsh:

- Zsh stores history in `~/.zsh_history`, and you can customize it with:
- `HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000`

---

### **Why use it?**

`history` helps you **recall old commands**, **fix mistakes**, and **repeat common operations quickly**.

---

### **Oh My Zsh Alias of the Day: `grhh` (Git Reset Hard Head)**

**Alias:**

```bash
grhh
```

👉 Runs:

📌 Resets your working directory and index to the last commit—**dangerous but powerful**.

---

### ⚠️ Use with caution:

- `grhh` discards all local changes!
- Combine with `git log` or `git stash` if you’re unsure.

💡 **Why use it?**

Sometimes, you just want a **clean slate**—`grhh` gives you that instantly.

### 

### 40 uptime

Mostra da quanto il sistema è acceso, quanti utenti sono connessi e il carico medio.

Uso base:

```jsx
uptime
```

Esempio output:

13:53:19 up 4:37, 5 users, load average: 1.87, 1.83, 1.54

Significato:

```
up 4:37: acceso da 4h 37min

5 users: utenti attivi

load average: carico CPU (1, 5, 15 minuti)

```

#### Suggerimento Zsh:
Aggiungi questo alias per una versione più leggibile:

alias up='uptime -p'

### 41. Comando: `find . -maxdepth 1 -type f -printf '%T@ %p\n' | sort -n | tail -n 10`

**Descrizione:** Mostra i 10 file modificati più di recente nella cartella corrente (non ricorsivo), ordinati dal più vecchio al più nuovo.
**Utilizzo:**

```
find . -maxdepth 1 -type f -printf '%T@ %p\n' | sort -n | tail -n 10
```

**Significato:**

- `find . -maxdepth 1 -type f` → cerca solo i file nel livello corrente
- `printf '%T@ %p\n'` → stampa timestamp e percorso file
- `sort -n` → ordina per data
- `tail -n 10` → ultimi 10 (cioè i più recenti)