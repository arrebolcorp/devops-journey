# Linux cheat sheet · Week 1

## Navigation

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `pwd` | Prints the full path of the folder that I am currently in. | `pwd` → `/home/vboxuser/devops-lab/week1-lab` | Always run this before `mv`, `cp`, or `rm` to avoid modifying the wrong folder. |
| `ls` | Shows visible list files and folders in the current directory. | `ls` → `backup config logs notes scripts` | Does not show hidden files starting with a dot (`.`). |
| `ls -a` | Shows all files and folders, including hidden files and folders. | `ls -a` → `. .. .bashrc config` | Includes `.` (current folder) and `..` (parent folder). |
| `ls -lah` | Shows the lists of all files in long format with human-readable sizes. | `ls -lah ~` → `drwxr-xr-x 4.0K ...` | The `-h` only works well alongside `-l`. |
| `cd` | Changes the current directory to a target path. | `cd devops-lab/week1-lab` | Typing `cd` alone takes you straight back to your home folder (`~`). |
| `cd ..` | Changes up one folder level to the parent directory. | `cd ..` → moves from `week1-lab` to `devops-lab` | Needs a space between `cd` and `..`; `cd..` causes a command not found error. |
| `cd ~` | Jumps up directly to my user home directory from anywhere. | `cd ~/devops-lab/week1-lab/backup` | `~` always I could have expands to `/home/<username>`. |
| `cd -` | Switches back to the previous directory I was in. | `cd -` → `/home/vboxuser` | Only toggles between the current and the immediately previous folder. |
| `tree` | Displays the folder and file structure as a visual tree. | `tree` → shows all 5 subdirectories | Not always installed by default; may require `sudo apt install tree`. |

## Files and folders

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `mkdir` | Creates a new empty directory. | `mkdir {config,logs,scripts,backup,notes}` | Fails if parent folders do not exist yet (use `-p` for nested folders). |
| `mkdir -p` | Creates nested directories all at once without errors. | `mkdir -p ~/devops-lab/week1-lab` | Does not complain if the directory already exists. |
| `touch` | Creates an empty file or updates its timestamp. | `touch notes-demo.txt` | Running it on an existing file does not erase its content. |
| `cp` | Copies a file from a source path to a destination path. | `cp /etc/os-release config/` | Overwrites the destination file silently unless you use `-i`. |
| `cp -r` | Copies an entire folder and all its contents recursively. | `cp -r config backup/config-bak` | Forgetting `-r` on a directory gives an `omitting directory` error. |
| `mv` | Moves a file/folder or renames it in place. | `mv backup.txt notes-demo2.txt` | If the target folder exists, it moves inside; otherwise, it renames. |
| `rm` | Permanently deletes a file. | `rm notes-demo.txt` | There is no trash bin in the terminal; deleted files cannot be undone. |
| `rm -ri` | Deletes folders and contents recursively, asking confirmation for each item. | `rm -ri backup/*` | Press `y` and `Enter` to confirm each file; safer than `rm -rf`. |

## Reading

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `cat` | Prints the entire content of a file directly to the terminal. | `cat config/os-release` | Avoid using `cat` on huge files like `/etc/services` because it floods the screen. |
| `less` | Opens a file in a scrollable viewer one page at a time. | `less /var/log/apt/history.log` | Press `/` to search text, `n` for next match, and `q` to quit. |

## System info

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `whoami` | Shows my current effective username. | `whoami` → `vboxuser` | Running `sudo whoami` returns `root`. |
| `hostname` | Displays the network name of the machine. | `hostname` → `ubuntu-lab` | Useful to confirm which server or VM you are connected to. |
| `lsb_release -a` | Shows detailed Ubuntu distribution and version information. | `lsb_release -a` → `Ubuntu 24.04..1 LTS` | The `-a` flag stands for "all" fields. |
| `uname -r` | Prints the active Linux kernel release version. | `uname -r` → `7.0.0-43-generic` | Lowercase `-r` shows only the kernel version; `-a` shows full system architecture. |
| `df -h` | Shows free and used disk space on mounted filesystems. | `df -h /` → `40Gi Size, 6.5Gi Used` | Use `-h` (with a hyphen), not `.h`. |
| `du -sh` | Summarizes the total disk size of the current folder. | `du -sh` → `1.2M .` | Measures directory weight, whereas `df` measures whole disk partitions. |
| `free -h` | Displays total, used, and available RAM and swap memory. | `free -h` → `3.3Gi total, 4.1Gi used` | Look at the `available` column rather than `free` to know real usable RAM. |
| `htop` | Opens a live interactive monitor for CPU, RAM, and processes. | `htop` | Press `q` to exit cleanly; may need to be installed first. |

## Help

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `man` | Opens the full official manual page for a command. | `man ls` | Do not put a hyphen before the command name (`man -ls` fails). |
| `--help` | Prints a quick summary of flags and usage directly in the terminal. | `ls --help` | Pipe it to `less` (`ls --help \| less`) if the output scrolls off screen. |

## Packages (apt and dpkg)

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `sudo apt update` | Refreshes the local list of available packages from repositories. | `sudo apt update` | Updates the catalog only; it does not upgrade installed software. |
| `sudo apt install` | Downloads and installs a new package and its dependencies. | `sudo apt install htop` | Always run `apt update` first so you don't fetch broken package links. |
| `sudo apt purge` | Removes a package along with its system configuration files. | `sudo apt purge htop` | Unlike `apt remove`, `purge` leaves no leftover config files behind. |
| `sudo apt autoremove` | Cleans up unused dependency packages no longer needed. | `sudo apt autoremove` | Always review the list of packages before confirming with `y`. |
| `dpkg -l` | Checks the installation status of a package in the local database. | `dpkg -l htop` → `un  htop` | The first two letters show desired and actual state (e.g., `un` = not installed, `ii` = installed). |

## Vim

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `vim <file>` | Opens or creates a file in the Vim terminal editor. | `vim notes/system-report.txt` | Opens in Normal mode; you cannot type text until you press `i`. |
| `i` / `Esc` | `i` enters Insert mode to type; `Esc` returns to Normal mode. | Pressed `i`, typed `# comment`, pressed `Esc` | Always press `Esc` before typing commands like `:wq` or `:50`. |
| `:wq` / `:q!` | `:wq` saves changes and quits; `:q!` quits without saving. | `:wq` | Using `:q` alone fails if you made unsaved edits. |
| `:set number` | Displays line numbers along the left margin inside Vim. | `:set number` | Helps navigate large files like `/etc/services`. |
| `:<line>` and `/<word>` | Jumps directly to a line number or searches forward for text. | `:50` then `/ssh` | Press `n` after searching to jump to the next occurrence. |

## sudo

| Command | What it does (my words) | Example I ran | Gotcha |
|---|---|---|---|
| `sudo` | Runs a single command with superuser (`root`) privileges. | `sudo gpasswd --add $USER xboxusers` | Never use `sudo` to edit files in your own home folder or bypass lab permission checks. |

## Path rules

- **Absolute vs. relative paths:** An absolute path starts from the root `/` (like `/etc/os-release`) and works from anywhere, while a relative path starts from my current folder (like `config/os-release`).
- **`~` (tilde):** A shortcut that always points to my personal home directory (`/home/vboxuser`).
- **`..` (double dot):** Represents the parent directory one level above my current location.
- **A typed path alone tries to run:** Typing a file path without a command (like `/etc/services`) makes the shell try to execute it as a program, causing a `Permission denied` or `Is a directory` error.

## Mistakes that taught me

- **`rn` vs `rm` and the `trn4` install:** Typing `rn` by mistake instead of `rm` triggers Ubuntu's command-not-found helper, which suggests installing an old newsreader package called `trn4`.
- **`./` vs `cat` vs `cd` on a file:** Using `./file` tries to execute it, `cat file` prints its text, and `cd file` fails because `cd` only works on directories.
- **Placeholders like `<package-name>`:** Angle brackets in guides mean "replace this with a real name" (such as `htop`); typing the `<` and `>` symbols literally causes syntax errors.
- **`cd..` without a space:** Because `cd` is a command and `..` is its argument, omitting the space makes bash look for a nonexistent command named `cd..`.
- **`mv` renaming vs. moving:** `mv` does both jobs—if the target path is an existing folder, it moves the file inside; if the target is a new filename in the same folder, it renames the file.
