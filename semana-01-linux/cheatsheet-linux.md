# Linux cheat sheet · Week 1

## Navigation

| Command | What it does | Example I ran |     
|---|---|---|
| `pwd` | Prints the full path of the folder that I am currently in. | `pwd` → `/home/vboxuser/devops-lab/week1-lab`  <img width="852" height="326" alt="image" src="https://github.com/user-attachments/assets/5c13fbaa-10e0-413a-8c38-0f2c400b6327" /> 
| Always run this before `mv`, `cp`, or `rm` to avoid modifying the wrong folder. |
| `ls` | Shows visible list files and folders in the current directory. | `ls` → `backup config logs notes scripts` <img width="1044" height="310" alt="image" src="https://github.com/user-attachments/assets/8ccd73dc-75ce-408c-b920-873f00f9bd00" /> 
  | Does not show hidden files starting with a dot (`.`). |
| `ls -a` | Shows all files and folders, including hidden files and folders. | `ls -a` → `. .. .bashrc config`  <img width="1394" height="473" alt="image" src="https://github.com/user-attachments/assets/09242b76-3be8-40e4-a08d-c05fb1cf4ec2" />  
| Includes `.` (current folder) and `..` (parent folder). |
| `ls -lah` | Shows the lists of all files in long format with human-readable sizes. | `ls -lah ~` → `drwxr-xr-x 4.0K ...`  <img width="804" height="676" alt="image" src="https://github.com/user-attachments/assets/5ad03e01-8217-49ec-968f-a827fc32e606" /> 
| The `-h` only works well alongside `-l`. |
| `cd` | Changes the current directory to a target path. | `cd devops-lab/week1-lab`  <img width="457" height="129" alt="image" src="https://github.com/user-attachments/assets/e1060f51-38d5-410d-83cd-b8c732669d86" /> 
| Typing `cd` alone takes you straight back to your home folder (`~`). |
| `cd ..` | Changes up one folder level to the parent directory. | `cd ..` → moves from `week1-lab` to `devops-lab` <img width="449" height="76" alt="image" src="https://github.com/user-attachments/assets/018472ee-8898-490a-9b86-b506e11d74aa" /> 
| Needs a space between `cd` and `..`; `cd..` causes a command not found error. |
| `cd ~` | Jumps up directly to my user home directory from anywhere. | `cd ~/devops-lab/week1-lab/backup`  <img width="566" height="70" alt="image" src="https://github.com/user-attachments/assets/0983f227-e272-4994-b916-680149bc92ab" /> 
| `~` always I could have expands to `/home/<username>`. |
| `cd -` | Switches back to the previous directory I was in. | `cd -` → `/home/vboxuser` <img width="530" height="73" alt="image" src="https://github.com/user-attachments/assets/89d1b286-f7f9-4f77-9eb4-34444c28c9dd" /> 
 | Only toggles between the current and the immediately previous folder. |
| `tree` | Displays the folder and file structure as a visual tree. | `tree` → shows all 5 subdirectories  <img width="556" height="343" alt="image" src="https://github.com/user-attachments/assets/b6cb2b6e-6012-4354-9bae-a5e585ed6f3e" /> 
| Not always installed by default; may require `sudo apt install tree`. |

## Files and folders

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `mkdir` | Creates a new empty directory. | `mkdir {config,logs,scripts,backup,notes}` <img width="632" height="63" alt="image" src="https://github.com/user-attachments/assets/7b59c70c-4029-4e40-a874-3b710914c5aa" /> 
 | Fails if parent folders do not exist yet (use `-p` for nested folders). |
| `mkdir -p` | Creates nested directories all at once without errors. | `mkdir -p ~/devops-lab/week1-lab`  <img width="572" height="65" alt="image" src="https://github.com/user-attachments/assets/3f4a73ce-1f28-42bb-af6b-7164c192cc92" /> 
 | Does not complain if the directory already exists. |
| `touch` | Creates an empty file or updates its timestamp. | `touch notes-demo.txt` <img width="866" height="468" alt="image" src="https://github.com/user-attachments/assets/fcba9e39-c42c-4287-a0f5-bfb2e6624681" /> 
| Running it on an existing file does not erase its content. |
| `cp` | Copies a file from a source path to a destination path. | `cp /etc/os-release config/`  <img width="760" height="459" alt="image" src="https://github.com/user-attachments/assets/a1309390-38f2-4863-97e9-61d685db5ec9" /> 
| Overwrites the destination file silently unless you use `-i`. |
| `cp -r` | Copies an entire folder and all its contents recursively. | `cp -r config backup/config-bak` <img width="657" height="439" alt="image" src="https://github.com/user-attachments/assets/1073b3d8-ba81-4e20-b3a8-08ec92041885" /> 
| Forgetting `-r` on a directory gives an `omitting directory` error. |
| `mv` | Moves a file/folder or renames it in place. | `mv notes.demo.txt notes-demo2.txt` <img width="585" height="73" alt="image" src="https://github.com/user-attachments/assets/93218b5e-3984-4920-ab3d-497ede6203a4" /> 
| If the target folder exists, it moves inside; otherwise, it renames. |
| `rm` | Permanently deletes a file. | `rm notes-demo2.txt` <img width="514" height="105" alt="image" src="https://github.com/user-attachments/assets/033b08df-a20c-47c9-bd0e-c023c276e212" /> 
| There is no trash bin in the terminal; deleted files cannot be undone. |
| `rm -ri` | Deletes folders and contents recursively, asking confirmation for each item. | `rm -ri backup/*` <img width="488" height="152" alt="image" src="https://github.com/user-attachments/assets/cbfc5003-12e9-4f04-a516-8ba8702c1f75" /> 
| Press `y` and `Enter` to confirm each file; safer than `rm -rf`. |

## Reading 

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `cat` | Prints the entire content of a file directly to the terminal. | `cat config/os-release` <img width="753" height="260" alt="image" src="https://github.com/user-attachments/assets/74a1e303-3251-4222-b3c5-3c4e66f3a451" /> 
| Avoid using `cat` on huge files like `/etc/services` because it floods the screen. |
| `less` | Opens a file in a scrollable viewer one page at a time. | `less /var/log/apt/history.log` <img width="1153" height="852" alt="image" src="https://github.com/user-attachments/assets/e9e7ec2f-bbca-4de1-bb70-d933df137e87" /> 
| Press `/` to search text, `n` for next match, and `q` to quit. |

## System info

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `whoami` | Shows my current effective username. | `whoami` → `vboxuser` <img width="421" height="82" alt="image" src="https://github.com/user-attachments/assets/bf5436ea-2918-4cc1-95f4-85066207a16b" /> 
| Running `sudo whoami` returns `root`. |
| `hostname` | Displays the network name of the machine. | `hostname` → `ubuntu-lab` <img width="380" height="104" alt="image" src="https://github.com/user-attachments/assets/7089b5c6-4174-4bd1-942f-53f6c0ab312a" /> 
| Useful to confirm which server or VM you are connected to. |
| `lsb_release -a` | Shows detailed Ubuntu distribution and version information. | `lsb_release -a` → `Ubuntu 24.04..1 LTS` <img width="434" height="143" alt="image" src="https://github.com/user-attachments/assets/64b91812-8c95-446e-a061-764312802e96" /> 
| The `-a` flag stands for "all" fields. |
| `uname -r` | Prints the active Linux kernel release version. | `uname -r` → `7.0.0-43-generic` <img width="404" height="72" alt="image" src="https://github.com/user-attachments/assets/b72c8ad7-419e-4b16-8603-aaabb7722db0" /> 
 | Lowercase `-r` shows only the kernel version; `-a` shows full system architecture. |
| `df -h` | Shows free and used disk space on mounted filesystems. | `df -h /` → `40G Size, 6.6G Used` <img width="675" height="191" alt="image" src="https://github.com/user-attachments/assets/20f6598b-ed89-4800-ad1a-8653a1bab9e3" />
| Use `-h` (with a hyphen), not `.h`. |
| `du -sh` | Summarizes the total disk size of the current folder. | `du -sh` → `88 K .` <img width="349" height="59" alt="image" src="https://github.com/user-attachments/assets/a130b962-c1d4-453f-97d6-2400c2525469" /> 
| Measures directory weight, whereas `df` measures whole disk partitions. |
| `free -h` | Displays total, used, and available RAM and swap memory. | `free -h` → `3.3G total, 1.5G used` <img width="695" height="100" alt="image" src="https://github.com/user-attachments/assets/b31d4004-04be-402d-893e-402251a18cc8" /> 
| Look at the `available` column rather than `free` to know real usable RAM. |
| `htop` | Opens a live interactive monitor for CPU, RAM, and processes. | `htop` <img width="1181" height="898" alt="image" src="https://github.com/user-attachments/assets/fb39b306-b10b-447a-a35f-1f1cb122d48c" />
| Press `q` to exit cleanly; may need to be installed first. |

## Help

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `man` | Opens the full official manual page for a command. | `man ls` <img width="1170" height="896" alt="image" src="https://github.com/user-attachments/assets/aebaa05d-0a71-48ec-9915-f42979118255" /> 
| Do not put a hyphen before the command name (`man -ls` fails). |
| `--help` | Prints a quick summary of flags and usage directly in the terminal. | `ls --help` <img width="1164" height="868" alt="image" src="https://github.com/user-attachments/assets/a03a0d6b-a66d-4ef4-a73d-2e9bb5d9faad" /> 
| Pipe it to `less` (`ls --help \| less`) if the output scrolls off screen. |

## Packages (apt and dpkg)

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `sudo apt update` | Refreshes the local list of available packages from repositories. | `sudo apt update` <img width="805" height="248" alt="image" src="https://github.com/user-attachments/assets/111432b1-1181-4125-9c14-9bbb15fd079e" /> 
| Updates the catalog only; it does not upgrade installed software. |
| `sudo apt install` | Downloads and installs a new package and its dependencies. | `sudo apt install htop` <img width="820" height="465" alt="image" src="https://github.com/user-attachments/assets/dcc888c4-34f8-4e82-aba0-acbf06b60a0e" /> 
| Always run `apt update` first so you don't fetch broken package links. |
| `sudo apt purge` | Removes a package along with its system configuration files. | `sudo apt purge htop` <img width="641" height="307" alt="image" src="https://github.com/user-attachments/assets/76c9253c-a22f-4681-8a89-627c1f87bf87" /> 
| Unlike `apt remove`, `purge` leaves no leftover config files behind. |
| `sudo apt autoremove` | Cleans up unused dependency packages no longer needed. | `sudo apt autoremove` <img width="550" height="96" alt="image" src="https://github.com/user-attachments/assets/74c45e7e-cce2-4e88-982c-64352fa90875" /> 
| Always review the list of packages before confirming with `y`. |
| `dpkg -l` | Checks the installation status of a package in the local database. | `dpkg -l htop` → `un  htop` <img width="472" height="74" alt="image" src="https://github.com/user-attachments/assets/4d127379-d4e6-4630-9d92-902da8c4e63c" /> 
| The first two letters show desired and actual state (e.g., `un` = not installed, `ii` = installed). | 

## Vim

| Command | What it does | Example I ran | Gotcha |
|---|---|---|---|
| `vim <file>` | Opens or creates a file in the Vim terminal editor. | `vim notes/system-report.txt` <img width="1020" height="875" alt="image" src="https://github.com/user-attachments/assets/3d1477af-5672-4d16-942e-92c28ec6d319" /> 
| Opens in Normal mode; you cannot type text until you press `i`. |
| `i` / `Esc` | `i` enters Insert mode to type; `Esc` returns to Normal mode. <img width="766" height="318" alt="image" src="https://github.com/user-attachments/assets/d4e4eb76-8256-4a0c-b7f1-d6e9ed779d40" /> 
| Pressed `i`, typed `# comment`, pressed `Esc` | Always press `Esc` before typing commands like `:wq` or `:50`. |
| `:wq` / `:q!` | `:wq` saves changes and quits; `:q!` quits without saving. <img width="1020" height="875" alt="image" src="https://github.com/user-attachments/assets/636f0be1-12d2-446f-b5f5-573f6cf0f234" />

| `:wq` | Using `:q` alone fails if you made unsaved edits. |
| `:set number` | Displays line numbers along the left margin inside Vim. | `:set number` <img width="852" height="888" alt="image" src="https://github.com/user-attachments/assets/23285f9d-ba82-40a2-93a6-2d7d42fc33fa" /> 
| Helps navigate large files like `/etc/services`. |
| `:<line>` and `/<word>` | Jumps directly to a line number or searches forward for text. | `:50` then `/ssh` <img width="554" height="95" alt="image" src="https://github.com/user-attachments/assets/b0234120-47e0-444e-87ae-9682b9047744" />
| Press `n` after searching to jump to the next occurrence. |


## Path rules

| Concept / Element | Description |
| :--- | :--- |
| **Absolute vs. relative paths** | An absolute path starts from the root `/` (like `/etc/os-release`) and works from anywhere, while a relative path starts from my current folder (like `config/os-release`). |
| **`~` (tilde)** | A shortcut that always points to my personal home directory (`/home/vboxuser`). |
| **`..` (double dot)** | Represents the parent directory one level above my current location. |
| **A typed path alone tries to run** | Typing a file path without a command (like `/etc/services`) makes the shell try to execute it as a program, causing a `Permission denied` or `Is a directory` error. |

## Mistakes that taught me

| Situation / Mistake | Explanation |
| :--- | :--- |
| **`rn` vs `rm` and the `trn4` install** | Typing `rn` by mistake instead of `rm` triggers Ubuntu's command-not-found helper, which suggests installing an old newsreader package called `trn4`. |
| **`./` vs `cat` vs `cd` on a file** | Using `./file` tries to execute it, `cat file` prints its text, and `cd file` fails because `cd` only works on directories. |
| **Placeholders like `<package-name>`** | Angle brackets in guides mean "replace this with a real name" (such as `htop`); typing the `<` and `>` symbols literally causes syntax errors. |
| **`cd..` without a space** | Because `cd` is a command and `..` is its argument, omitting the space makes bash look for a nonexistent command named `cd..`. |
| **`mv` renaming vs. moving** | `mv` does both jobs—if the target path is an existing folder, it moves the file inside; if the target is a new filename in the same folder, it renames the file. |
