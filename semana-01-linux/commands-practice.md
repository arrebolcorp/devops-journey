## What I practiced this week

To sum up, this was a tough week because I studied a lot of new concepts and practiced new commands on a new OS. Still, I know it's all part of trying something new.

I would like to summarize the commands I practiced. Today, I practiced creating a new file (`example.source`) using `vim` and moving from folder to folder.

### Commands Summary by Category

| Category | Commands |
| :--- | :--- |
| **Navigation** | `pwd`, `ls`, `cd` |
| **Files** | `mkdir -p`, `touch`, `cp`, `mv`, `rm -i` |
| **Reading** | `cat`, `less`, `head`, `tail` |
| **System** | `whoami`, `uname -r`, `lsb_release -a`, `df -h`, `free -h`, `du -sh` |
| **Help** | `man`, `--help`, `history` |
| **Admin and apt** | `sudo`, `apt update`, `apt install`, `apt purge`, `apt autoremove`, `apt show`, `apt policy`, `dpkg -l`, `dpkg -L` |

I made quite a few mistakes while practicing, but I analyzed them and didn't stop trying. For example, while practicing `rm`, I accidentally typed `rn` and ended up installing an old package called `trn4`. My bad—I fixed it by purging and removing the package.

You can review my command history, my explanations, and the screenshots from my work today and throughout this week below:

<img width="401" height="322" alt="image" src="https://github.com/user-attachments/assets/009b9c87-6348-487e-8e98-4a032b260603" />
<img width="431" height="331" alt="image" src="https://github.com/user-attachments/assets/307bac99-ef8f-485f-bc9c-2116cd7a2701" />
<img width="257" height="332" alt="image" src="https://github.com/user-attachments/assets/41b202cd-5936-499b-bae6-9191017749c0" />

---

## Command Breakdown & Screenshots

| Command | Description | Screenshot |
| :--- | :--- | :--- |
| **`sudo whoami`** | Checks if I have admin / root permissions. | <img width="170" height="41" alt="image" src="https://github.com/user-attachments/assets/7d94352d-bd02-4dd3-854a-8a6f149d5f3b" /> |
| **`lsb_release -a`** | Prints detailed version information of my Linux distribution. | <img width="107" height="44" alt="image" src="https://github.com/user-attachments/assets/20d005c0-431c-4d76-9884-a6abf2af305b" /> |
| **`pwd`** | Prints my current working directory. | <img width="162" height="17" alt="image" src="https://github.com/user-attachments/assets/01af6e14-1312-40e0-a398-59fd124abf51" /> |
| **`ls`** | Prints the list of files and folders inside my current directory. | <img width="314" height="17" alt="image" src="https://github.com/user-attachments/assets/d227214b-3a97-4a38-81b6-54f16ab6278b" /> |
| **`ls -a`** | Adding `-a` to `ls` prints all files and folders, including hidden ones. | <img width="599" height="26" alt="image" src="https://github.com/user-attachments/assets/9dbb788d-ab21-436d-a465-5290684eca54" /> |
| **`ls -lah ~`** | Prints detailed information in a human-readable format, showing all files and their sizes. | <img width="257" height="199" alt="image" src="https://github.com/user-attachments/assets/273c7836-60f0-48b8-8bf4-a43af308d49c" /> |
| **`cd ..`** | Moves up one level to the parent folder in the directory structure. | <img width="98" height="26" alt="image" src="https://github.com/user-attachments/assets/bafd06c7-c0c9-4cf4-b7b7-e089a07b5e89" /> |
| **`cd -`** | Takes you back to the previous folder you were in before the last `cd` command. | <img width="83" height="23" alt="image" src="https://github.com/user-attachments/assets/fc66f9d8-4249-4b53-bbca-70de63768091" /> |
| **`cd ~`** | Returns to your personal home directory. | <img width="89" height="23" alt="image" src="https://github.com/user-attachments/assets/2eec0e7a-96d2-46d9-82ad-b483981a7b23" /> |
| **`cd /etc`** | Navigates directly to the `/etc` directory. | <img width="97" height="17" alt="image" src="https://github.com/user-attachments/assets/82533606-9e67-4cfa-a227-ab4d577ce326" /> |
| **`mkdir -p devops-lab/notes`** | Creates a new directory structure (`-p` creates parent directories as needed). | — |
| **`touch notes-demo.txt`** | Creates a new empty file. | — |
| **`cp -r notes-demo.txt backup.txt`** | Copies a file (`cp` + source file + destination file). *Note: I made several mistakes here during practice because I needed to type the full, exact file name and extension.* | — |
| **`mv backup.txt notes-demo2.txt`** | Renames `backup.txt` to `notes-demo2.txt`. | — |
| **`cat /etc/os-release`** | Reads and prints the entire content of a file in the terminal. | <img width="230" height="88" alt="image" src="https://github.com/user-attachments/assets/2a8b1986-acdb-4de6-bd2a-4a3248683009" /> |
| **`less /var/log/dpkg.log`** | Allows reading and scrolling through a file interactively. | <img width="236" height="325" alt="image" src="https://github.com/user-attachments/assets/6fb01432-ae47-4a5a-9f49-93e75b98f948" /> |
| **`head -n4 /var/log/dpkg.log`** | Displays the first `X` number of lines of a file using `-nX` (in this case, 4 lines). | <img width="176" height="43" alt="image" src="https://github.com/user-attachments/assets/8a194ef2-2e14-465d-b28a-bacde9fe1012" /> |
| **`tail -n5 /var/log/dpkg.log`** | The opposite of `head`; shows the last `X` number of lines (in this case, 5 lines). | <img width="193" height="53" alt="image" src="https://github.com/user-attachments/assets/6aaedd9f-6e82-445b-b82f-0e22d4f1f28a" /> |
| **`df -h`** | Prints available disk space across all storage partitions in human-readable format. | <img width="191" height="80" alt="image" src="https://github.com/user-attachments/assets/18a8f0b0-c686-4924-ac99-988e9b7e7fcc" /> |
| **`free -h`** | Displays available and used RAM in human-readable format. | <img width="188" height="45" alt="image" src="https://github.com/user-attachments/assets/20fb1cb4-8e4a-489a-959d-acfc19596889" /> |
| **`du -sh`** | Shows the total disk size of the current folder. | <img width="116" height="23" alt="image" src="https://github.com/user-attachments/assets/0249ebc2-98f2-4195-ac4c-352afb76c843" /> |
| **`man <command>`** | Opens the full user manual for a given command. | — |
| **`ls --help`** | Displays a quick summary and usage options for the command. | <img width="188" height="133" alt="image" src="https://github.com/user-attachments/assets/cf8e454e-adbe-49da-b3df-e4df2f9267db" /> |
| **`sudo apt update`** | Searches for and updates the list of available package versions. | — |
| **`sudo apt install tree`** | Installs the package named `tree`. | — |
| **`history`** | Prints the history of all previously executed commands. | — |
| **`sudo apt purge trn4`** | Completely removes a package along with its configuration files (`remove` only deletes the binaries/files). | — |
| **`dpkg -l trn4`** | Checks the status of the package to verify if any files or traces remain. | — |
| **`sudo apt autoremove`** | Finds and removes unused dependencies and packages. | — |
| **`vi --version`** | Checks the installed Vim version. | — |
| **`vim testfile`** | Creates and opens a new test file (you can specify any extension like `.txt`, `.source`, etc.). | — |
| **`vimtutor`** | Opens the built-in interactive tutorial that teaches how to use Vim. | — |
