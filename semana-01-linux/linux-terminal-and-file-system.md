## Terminal and File System Basics
When working in a Linux terminal, your command prompt is typically divided into parts that show information like the current user, host, and working directory. For example:

~ represents your home directory.

$ indicates a normal user prompt.

-# indicates the root (admin) user.

As we saw earlier, running sudo whoami prints root.

sudo stands for "superuser do" and runs a single command with administrative rights.

## What is the Command Line?
The command line is a text-based interface—often called the shell, terminal, console, or prompt—used to interact with the operating system.

## What is the Linux File System Structure?
First, let's understand the Layout:

/ (Root Directory): The top-level directory that contains everything on the system. (Note: This is not the same as /root, which is the home directory for the root user.)

## Linux organizes its file system into key directories, each with a specific purpose:

## Essential System & Binary Directories
/bin
One of the most important directories on the system. It contains essential command-line binaries and core utilities needed for the system to function properly (such as ls, cp, mv, and cat). Regular users should not modify files here.

/sbin
Similar to /bin, but restricted to system administration commands that require root privileges (such as mount, fsck, and shutdown). These should generally not be touched or modified by standard users.

/lib (and /lib32, /lib64)
This directory functions similarly to System32 in Windows. It stores shared library files (like .dll equivalents) that provide common functionality for system programs, such as reading files or handling input/output. This area is rarely modified manually.

/usr
Standing for Unix System Resources, this directory stores user-space applications, shared libraries, and documentation. It does not store personal user files. A typical user doesn't modify these directories at the root level (e.g., /usr/bin or /usr/lib). This structure keeps the system organized and bootable even if only the root partition is available.

/boot
Contains all the files your system needs to boot up successfully, including the Linux kernel, the initial RAM disk (initrd or initramfs), and GRUB bootloader files. One key file here is GRUB.CFG, which instructs the system on how to load the operating system.

## Hardware, Configuration, & User Storage
/dev
This folder doesn't hold regular files; instead, it contains device files that act as interfaces to your hardware. In Linux, "everything is treated like a file," and hardware devices are exposed here. For example, /dev/sda typically represents your first hard drive, and /dev/null is a virtual device.
There are two main types:

Block devices (like hard drives), which handle data in chunks.

Character devices (like keyboards), which handle data as a stream of characters.
These files are managed dynamically as Linux adds or removes hardware.

/etc
The central location for system-wide configuration files, covering everything from network settings and user accounts to startup scripts and service configurations. Examples include /etc/passwd (user information) and /etc/fstab (how drives are mounted at boot). Most of these are plain-text files designed to be readable and editable by administrators. (The name originally stood for "et cetera," but many think of it as "Editable Text Configuration.")

/home
The personal space for regular users. Each user has their own subdirectory here (e.g., /home/alan or /home/arrebolcorp) where they store documents, downloads, projects, and personal settings. This keeps user data separate from system files for easier backups and management.

Hidden configuration files (like .bashrc) also live here.

Users generally do not have access to each other's /home folders, adding a layer of privacy.

Note: The root user has a separate home directory located at /root instead of inside /home for security and isolation.

## Removable Media & Temporary Storage
/media
Where modern Linux systems automatically mount removable media like USB flash drives, CDs, and DVDs. Each device gets its own subfolder here, making it easy to access photos, documents, or software.

It is user-friendly and usually doesn't require administrative privileges, as desktop environments like GNOME or KDE handle mounting automatically.

Distinction: /dev holds the raw hardware device files, while /media is where those devices are mounted for everyday use.

/mnt
Traditionally used by system administrators to manually mount external storage, secondary partitions, backup disks, or remote file systems (especially during maintenance or recovery). Unlike /media (which handles automatic user mounting), /mnt is reserved for manual, temporary mounts used by root or advanced scripts.

/tmp
Designed for short-term use, this is where applications and users store temporary working files while tasks are in progress (such as opening a file in an editor or running an installer). These files are typically deleted automatically on reboot or after a set period. It is writable by all users and protected by a special permission called the Sticky Bit.

/run
An in-memory directory holding temporary runtime data used by the system and applications right after boot. Created early in the startup process, everything inside it disappears on reboot. It is used by running processes to communicate, track state, or store short-term process IDs and sockets.

## System Services, Logs, & Optional Software
/proc
An unusual and vital virtual directory. It contains no real files stored on disk; instead, it provides a dynamic, in-memory view of the system. While /dev represents hardware, /proc acts as a live interface to the Linux kernel and running processes (e.g., /proc/cpuinfo and /proc/meminfo).

/sys
A virtual directory similar to /proc. Part of the sysfs pseudo-file system, it acts as a dynamic interface between the Linux kernel and your hardware devices.

/srv
Short for service. This is where data for services provided by your system—such as web servers (/srv/www), FTP servers, or other hosted applications—is stored for remote users.

/var
Short for variable. This directory stores files that change frequently during system operation, such as logs, caches, and spool files. For example, /var/log tracks system activity and errors. Because it can contain sensitive information, it should be properly protected, especially on multi-user servers.

/opt
Short for optional. This is where third-party or optional software is installed, keeping large or proprietary programs (like Google Chrome under /opt/google/chrome) separate from the core system directories. This keeps things organized, makes uninstallation easier, and prevents software from interfering with standard Linux file structure rules. Like most system directories, modifying it requires administrative privileges.

## Practice and review command lines

The next step, I use the follow command lines for practice the navigation, use a commands for files and folders, reading files, system info, help and administration.
I gonna to in order, Claude helps me giving me a table with some commands lines for practice the fundamental.

## pwd
pwd helps to show up the full path of the current directory, in this case, I stay in /run/media/vboxuser/VBox_GAs_7.2.8
<img width="239" height="71" alt="image" src="https://github.com/user-attachments/assets/8744656c-4172-4bcd-b4bb-9ef40ebb9ab6" />

## ls
This command line shows lists files and folders, you can add -a for show up a hidden files, -h for readable sizes and the -l is for details. 
<img width="199" height="68" alt="image" src="https://github.com/user-attachments/assets/c4b70a18-526e-47fc-a3b9-cb378bd5e854" />
<img width="183" height="77" alt="image" src="https://github.com/user-attachments/assets/bcbba963-6513-4ab8-826c-81fe82ccaed0" />
<img width="224" height="125" alt="image" src="https://github.com/user-attachments/assets/768c0d9d-8b5b-4828-addf-3f2d01ad68b3" />

## cd
This the most common command line I guess. It helps us to change directory, .. for up one level, ~ or no argument for home, - previous directory. cd helps to move on the directories in the system.
<img width="218" height="175" alt="image" src="https://github.com/user-attachments/assets/99728f7d-2e49-402e-881f-b3aa233a88c9" />

## mkdir
Arrive to the commands for files and folders and start with mkdir, this command line helps us to create folders and if I add -p also creates parent folders. For example, mkdir -p devops-lab/notes
<img width="220" height="171" alt="image" src="https://github.com/user-attachments/assets/5e061116-d3ba-4533-b589-761f1370de34" />

## touch
This is so easy, helps us to create empy file, for example, touch notes-demo.txt
<img width="263" height="188" alt="image" src="https://github.com/user-attachments/assets/1669ce8f-f7ee-4824-88ff-fe29a3c4719f" />

## cp
cp helps us to copy files and if I add -r copy folders. For example cp -r notes backup
<img width="283" height="189" alt="image" src="https://github.com/user-attachments/assets/d188c6d3-ea3e-45d3-b232-ba90b61e4de4" />

##mv
This command has two functions, to move or to rename a file. For example, mv notes-demo.txt notes-demo2.txt
<img width="230" height="178" alt="image" src="https://github.com/user-attachments/assets/34a38c4f-b6f7-4c9d-bf3b-a5e75ee6e14d" />

## rm 
This we have a command line so important and we can use with a lot caution. This command line helps us to delete with NO TRASH, we can add -r for folders or -i for ask first. For example, rm -i notes-demo2.txt
NOTE: For my case I need to install rn with the allowing command line 'sudo apt install trn4', and as I have a user password I should put in.

## cat
The next command line is cat, it helps to prints the whole file. For example cat /etc/os-release
<img width="233" height="178" alt="image" src="https://github.com/user-attachments/assets/8b1061a9-0b52-4682-a8a5-aa41c3f20372" />

## less
The function for this command line is for showing a file page by page, you should add /text to search and q to quit.
For example, less /var/log/dpkg.log
<img width="218" height="185" alt="image" src="https://github.com/user-attachments/assets/c5be5d73-1bdb-4f6a-95ec-bd4b7433c44e" />

## head
This command has a similar function that less, but head helps us for showing the first lines on the any file, and if you add a -n sets how many lines you should read. For example, head -n 5 /var/log/dpkg.log
<img width="242" height="182" alt="image" src="https://github.com/user-attachments/assets/0fcc064b-67c5-4a5d-a674-fa8a2bf6c93d" />

## tail
Is the oppose of head, shows the last lines and the -n have the same function. For example, tail -n 5 /var/log/dpkg.log
<img width="232" height="178" alt="image" src="https://github.com/user-attachments/assets/0332a528-a290-4853-a4b9-3ebf5eaa244b" />

## whoami
This command line shows the current user.
<img width="222" height="175" alt="image" src="https://github.com/user-attachments/assets/8e2f30ac-2219-49b1-a324-885cd505ca86" />

## uname
uname have a function for showing system info, and if you add -r shows the kernel version and -a for shows everything.
For example, uname -r
<img width="219" height="164" alt="image" src="https://github.com/user-attachments/assets/f6541883-dda6-4d76-818c-2f46a34aadfd" />

## lsb_release -a
This important to learn because shows the ubuntu distribution and version. 
<img width="218" height="170" alt="image" src="https://github.com/user-attachments/assets/5eb09cbf-1073-408a-bee6-0b443e29983a" />

## df -h
This command line helps us to show disk space for partition. 
<img width="215" height="158" alt="image" src="https://github.com/user-attachments/assets/e17532a6-ea9a-47f7-b59a-43ace526cb7b" />

## free -h
This command line helps us to show used and free RAM.
<img width="213" height="170" alt="image" src="https://github.com/user-attachments/assets/980e5265-e449-4c52-8e30-3bed3aacce49" />

## du -sh 
This command helps up to show the total size of a folder.
<img width="227" height="169" alt="image" src="https://github.com/user-attachments/assets/6c6c5a1f-7306-40a2-8fdf-a18e2ac46f8c" />

## man
This command is important, because shows the manual for a command (press q to quit). For example man ls

## --help
This command helps us to print a quick summary of a command's options. For example, ls --help
<img width="216" height="166" alt="image" src="https://github.com/user-attachments/assets/99920e84-c6a3-40b5-8505-14898f3eb8c2" />

## sudo
This is a lot important command line because runs one command with admin rights. For example, sudo whoami
<img width="212" height="164" alt="image" src="https://github.com/user-attachments/assets/ce330591-e607-47ff-a111-9dfe6830d6ff" />

## sudo apt update
This command line helps us to refresh the list of available packages. For example, sudo apt update
<img width="213" height="164" alt="image" src="https://github.com/user-attachments/assets/a58dade1-4e40-4f6b-969a-3f7dc86532f7" />

## sudo apt install
This command has a funtion to install a package. For example, I gonna to install a package named tree, this package helps us for illustrate a directory in tree form.  sudo apt install tree
<img width="220" height="172" alt="image" src="https://github.com/user-attachments/assets/fdd2ad32-2fab-4e1c-86c3-db0c35b3b088" />

## history
And, the last one. History helps us for print the list commands you have typed.
<img width="397" height="257" alt="image" src="https://github.com/user-attachments/assets/d1a5ad76-dc45-4b68-a85a-43b0ccb05b91" />
<img width="397" height="260" alt="image" src="https://github.com/user-attachments/assets/a99be501-7df8-40cf-ad13-a5f41f93d39f" />

And it's all for today, tomorrow I follow the next note class. See you 
