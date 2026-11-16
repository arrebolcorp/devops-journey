## Terminal and File System Basics

When working in a Linux terminal, your command prompt is typically divided into parts that show information like the current user, host, and working directory:

| Symbol / Command | Meaning |
| :--- | :--- |
| **`~`** | Represents your home directory. |
| **`$`** | Indicates a normal user prompt. |
| **`#`** | Indicates the root (admin) user prompt. |
| **`sudo`** | Stands for *"superuser do"* and runs a single command with administrative rights (e.g., running `sudo whoami` prints `root`). |

### What is the Command Line?
The command line is a text-based interface—often called the **shell**, **terminal**, **console**, or **prompt**—used to interact with the operating system.

---

## Linux File System Structure

At the top of the hierarchy is **`/` (Root Directory)**, which contains everything on the system. *(Note: This is not the same as `/root`, which is the home directory for the root user.)*

Linux organizes its file system into key directories, each with a specific purpose:

### Essential System & Binary Directories

| Directory | Purpose & Details |
| :--- | :--- |
| **`/bin`** | Contains essential command-line binaries and core utilities needed for the system to function properly (such as `ls`, `cp`, `mv`, and `cat`). Regular users should not modify files here. |
| **`/sbin`** | Similar to `/bin`, but restricted to system administration commands that require root privileges (such as `mount`, `fsck`, and `shutdown`). |
| **`/lib`** *(and `/lib32`, `/lib64`)* | Functions similarly to `System32` in Windows. It stores shared library files (`.dll` equivalents) that provide common functionality for system programs, such as reading files or handling I/O. |
| **`/usr`** | Standing for *Unix System Resources*, this stores user-space applications, shared libraries, and documentation (e.g., `/usr/bin`, `/usr/lib`). It does not store personal user files, keeping the system organized and bootable even if only the root partition is available. |
| **`/boot`** | Contains all the files needed to boot up successfully, including the Linux kernel, the initial RAM disk (`initrd` or `initramfs`), and GRUB bootloader files (such as `grub.cfg`). |

### Hardware, Configuration, & User Storage

| Directory | Purpose & Details |
| :--- | :--- |
| **`/dev`** | Contains device files that act as interfaces to your hardware (e.g., `/dev/sda` for your first hard drive, `/dev/null` as a virtual device). Managed dynamically by Linux, it includes **Block devices** (hard drives, handling data in chunks) and **Character devices** (keyboards, handling data as a stream). |
| **`/etc`** | The central location for system-wide plain-text configuration files, covering network settings, user accounts (`/etc/passwd`), and mount rules (`/etc/fstab`). Originally stood for *"et cetera,"* often thought of as *"Editable Text Configuration."* |
| **`/home`** | The personal space for regular users (e.g., `/home/alan` or `/home/arrebolcorp`) where documents, projects, and hidden settings (like `.bashrc`) live. Users cannot access each other's folders. *(The root user lives separately in `/root` for security.)* |

### Removable Media & Temporary Storage

| Directory | Purpose & Details |
| :--- | :--- |
| **`/media`** | Where modern Linux desktop environments (like GNOME or KDE) automatically mount removable media like USB drives, CDs, and DVDs for everyday user access. *(Distinction: `/dev` holds raw hardware files; `/media` mounts them for use.)* |
| **`/mnt`** | Reserved for system administrators to manually mount external storage, secondary partitions, or remote file systems during maintenance or recovery. |
| **`/tmp`** | Short-term storage for temporary working files while tasks are in progress. Writable by all users, protected by the **Sticky Bit** permission, and typically cleared on reboot. |
| **`/run`** | An in-memory directory holding temporary runtime data (process IDs, sockets, state tracking) created early at boot. Everything inside disappears on reboot. |

### System Services, Logs, & Optional Software

| Directory | Purpose & Details |
| :--- | :--- |
| **`/proc`** | A vital virtual directory with no real files on disk; it provides a live, in-memory interface to the Linux kernel and running processes (e.g., `/proc/cpuinfo`, `/proc/meminfo`). |
| **`/sys`** | A virtual directory part of the `sysfs` pseudo-file system, acting as a dynamic interface between the Linux kernel and hardware devices. |
| **`/srv`** | Short for *service*. Stores data for services hosted by your system—such as web servers (`/srv/www`) or FTP servers—for remote users. |
| **`/var`** | Short for *variable*. Stores files that change frequently during operation, such as system logs (`/var/log`), caches, and spool files. |
| **`/opt`** | Short for *optional*. Where third-party or proprietary software (like Google Chrome under `/opt/google/chrome`) is installed to keep it separate from core system directories. |

---

## Command Line Practice & Review

Next, I practiced fundamental commands covering navigation, file management, file reading, system info, help, and administration:

| Command | Description & Example | Screenshot(s) |
| :--- | :--- | :--- |
| **`pwd`** | Shows the full path of the current working directory (e.g., `/run/media/vboxuser/VBox_GAs_7.2.8`). | <img width="239" height="71" alt="image" src="https://github.com/user-attachments/assets/8744656c-4172-4bcd-b4bb-9ef40ebb9ab6" /> |
| **`ls`** | Lists files and folders. Add `-a` for hidden files, `-l` for details, and `-h` for human-readable sizes. | <img width="199" height="68" alt="image" src="https://github.com/user-attachments/assets/c4b70a18-526e-47fc-a3b9-cb378bd5e854" /><br><img width="183" height="77" alt="image" src="https://github.com/user-attachments/assets/bcbba963-6513-4ab8-826c-81fe82ccaed0" /><br><img width="224" height="125" alt="image" src="https://github.com/user-attachments/assets/768c0d9d-8b5b-4828-addf-3f2d01ad68b3" /> |
| **`cd`** | Changes directories (`..` moves up one level, `~` or no argument goes home, `-` returns to the previous directory). | <img width="218" height="175" alt="image" src="https://github.com/user-attachments/assets/99728f7d-2e49-402e-881f-b3aa233a88c9" /> |
| **`mkdir`** | Creates folders; adding `-p` creates parent directories as needed. Example: `mkdir -p devops-lab/notes` | <img width="220" height="171" alt="image" src="https://github.com/user-attachments/assets/5e061116-d3ba-4533-b589-761f1370de34" /> |
| **`touch`** | Creates a new empty file. Example: `touch notes-demo.txt` | <img width="263" height="188" alt="image" src="https://github.com/user-attachments/assets/1669ce8f-f7ee-4824-88ff-fe29a3c4719f" /> |
| **`cp`** | Copies files, or folders when adding `-r`. Example: `cp -r notes backup` | <img width="283" height="189" alt="image" src="https://github.com/user-attachments/assets/d188c6d3-ea3e-45d3-b232-ba90b61e4de4" /> |
| **`mv`** | Moves or renames files and folders. Example: `mv notes-demo.txt notes-demo2.txt` | <img width="230" height="178" alt="image" src="https://github.com/user-attachments/assets/34a38c4f-b6f7-4c9d-bf3b-a5e75ee6e14d" /> |
| **`rm`** | Permanently deletes files with **no trash** (`-r` for folders, `-i` to prompt before deleting). Examples: `rm -i notes-demo2.txt`, `rm -ri <folder>` | — |
| **`cat`** | Prints the entire content of a file in the terminal. Example: `cat /etc/os-release` | <img width="233" height="178" alt="image" src="https://github.com/user-attachments/assets/8b1061a9-0b52-4682-a8a5-aa41c3f20372" /> |
| **`less`** | Displays a file page by page (`/text` to search, `q` to quit). Example: `less /var/log/dpkg.log` | <img width="218" height="185" alt="image" src="https://github.com/user-attachments/assets/c5be5d73-1bdb-4f6a-95ec-bd4b7433c44e" /> |
| **`head`** | Shows the first lines of a file (`-n` sets the line count). Example: `head -n 5 /var/log/dpkg.log` | <img width="242" height="182" alt="image" src="https://github.com/user-attachments/assets/0fcc064b-67c5-4a5d-a674-fa8a2bf6c93d" /> |
| **`tail`** | Opposite of `head`; shows the last lines of a file. Example: `tail -n 5 /var/log/dpkg.log` | <img width="232" height="178" alt="image" src="https://github.com/user-attachments/assets/0332a528-a290-4853-a4b9-3ebf5eaa244b" /> |
| **`whoami`** | Prints the currently logged-in username. | <img width="222" height="175" alt="image" src="https://github.com/user-attachments/assets/8e2f30ac-2219-49b1-a324-885cd505ca86" /> |
| **`uname`** | Displays system info (`-r` for kernel version, `-a` for all details). Example: `uname -r` | <img width="219" height="164" alt="image" src="https://github.com/user-attachments/assets/f6541883-dda6-4d76-818c-2f46a34aadfd" /> |
| **`lsb_release -a`** | Shows the Ubuntu distribution and release version. | <img width="218" height="170" alt="image" src="https://github.com/user-attachments/assets/5eb09cbf-1073-408a-bee6-0b443e29983a" /> |
| **`df -h`** | Shows available and used disk space across partitions in human-readable format. | <img width="215" height="158" alt="image" src="https://github.com/user-attachments/assets/e17532a6-ea9a-47f7-b59a-43ace526cb7b" /> |
| **`free -h`** | Displays used and available RAM in human-readable format. | <img width="213" height="170" alt="image" src="https://github.com/user-attachments/assets/980e5265-4499-4c52-8e30-3bed3aacce49" /> |
| **`du -sh`** | Shows the total disk size of a directory. | <img width="227" height="169" alt="image" src="https://github.com/user-attachments/assets/6c6c5a1f-7306-40a2-8fdf-a18e2ac46f8c" /> |
| **`man`** | Opens the manual page for a command (`q` to quit). Example: `man ls` | — |
| **`--help`** | Prints a quick summary of a command's options. Example: `ls --help` | <img width="216" height="166" alt="image" src="https://github.com/user-attachments/assets/99920e84-c6a3-40b5-8505-14898f3eb8c2" /> |
| **`sudo`** | Executes a single command with administrative (root) privileges. Example: `sudo whoami` | <img width="212" height="164" alt="image" src="https://github.com/user-attachments/assets/ce330591-e607-47ff-a111-9dfe6830d6ff" /> |
| **`sudo apt update`** | Refreshes the local list of available packages and updates. | <img width="213" height="164" alt="image" src="https://github.com/user-attachments/assets/a58dade1-4e40-4f6b-969a-3f7dc86532f7" /> |
| **`sudo apt install`** | Installs a new package (e.g., `tree`, which displays directories in a tree format: `sudo apt install tree`). | <img width="220" height="172" alt="image" src="https://github.com/user-attachments/assets/fdd2ad32-2fab-4e1c-86c3-db0c35b3b088" /> |
| **`history`** | Prints the list of previously executed commands. | <img width="397" height="257" alt="image" src="https://github.com/user-attachments/assets/d1a5ad76-dc45-4b68-a85a-43b0ccb05b91" /><br><img width="397" height="260" alt="image" src="https://github.com/user-attachments/assets/a99be501-7df8-40cf-ad13-a5f41f93d39f" /> |

---

*That's all for today—continuing with the next class notes tomorrow!*
