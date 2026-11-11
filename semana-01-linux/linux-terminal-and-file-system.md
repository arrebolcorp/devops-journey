## Terminal and file system
Each prompt or command line in a terminal in this case I references to Linux terminal, you use a prompts that this prompts are divide in parts. Each part can be user, host, current directory etc. For example;
## ~ <-- is your home.
## $ <-- is for normal user.
## '#' <-- would mean root.

In the previous file I use the 'sudo whoami' and printed 'root'.
## sudo <-- runs one command with admin rights.

## What is Command Line?
The command line is a text interface, often called the shell, terminal, console or prompt.

## What is Linux file system structure?
For the first we learn the 'Layout';
## Layout (/) <-- is the root directory of everything doesn't the same that '/root'

The linux file system structure have a ten directory categories;
## 1. System binaries 
## 3. Configuration files
## 4. User-related
## 5. Shared libraries
## 6. Mount Points & media
## 7. System info.
## 8. Multi-user Resources
## 9. Temporary files
## 10. Optional Software

Some directories are:

## /bin
this is a the most important directories, this folder contains the most important and essential command-line that are needed for the system to function properly. Commands are; is, cp, mv, cat. This directory don't have modify.
## /sbin
This is a directory where it requires admin or root permissions, don't touch and modify this directory. Commands are; mount, fsck, shutdown.
## /lib
Depends of you system, you might also see /lib32 and /lib64. This directory function is similar to System32 in windows where their have files type .dll, this library provide common funtionality like reading files or hangin input and output.
This space don't is modify regularity. 
## /usr
It doesn't store personal user files. It stands for Unix System Resources and contains most of the system's user-space applications, libraries and documentation. A typical user doesn't usually modify this directories form the root level, like /usr/lib, /usr/bin, /usr/sbin. 
This complements exist for keeping the system organized and bootable even  if only the root partition is available.

## 2. Boot & kernel-related
## /boot
This folder contains all the files your system needs to boot up, like Linux kernel, initial RAM disk (initrd or initramfs) and GRUB bootloader files. One important file here is GRUB.CFG, which tells the system how to load the operating system. 
## /dev
This folder doesn't hold regular files, instead, it contains device files that act as interfaces to your hardware. I see that linux, everything is treated like a file, even devices, and this is where they're exposed to the system.
For example, /dev/sda might represent your first hard drive. Whether it's your hard drive, USB stick, keyboard or even virtual devices live /dev/null they all show up here.
I will find two main types: -- Block devices, like hard devices, which handle date in chunks; and -- Character devices, like keyboards, which handle data as a stream of characters. This files are managed dynamically, Linux adds or removes them as hardware changes.
## /etc
This is the central location for system-wide configuration files, covering everything from network settings and user accounts to startup scrips and service configuration. 
For example, /etc/passwd holds basic user information and
/etc/fstab defines how drives are mounted at boot.
Most of theses are plain-text-files, designed to be readable and editable by system administrators.
The name 'etc' originally stood for et cetera, but some like to think of it as Editable Text Configuration.
## /home
This is the personal space for regular users. Each userr has their own subdirectory here, like /home/alan or /home/arrebolcorp, where they store documents, downloads, projects and personal settings.
These folders keep user data separate from system files, making backups and account management much easier. 
User-specific configuration files often live here too. Many are hidden by default.
Hidden files in Linux usually start with .,like .bashrc.
By default, users don't have access to each other's /home folders unless permissions are changed, adding a layer of privacy.
--This is own space to create, modify and safe files freely.
--The root user, however, has a separate /home directory located at /root instead of inside /home to keep it isolated and more secure.
## /media
This is a directory is where modern Linux systems automatically mount removable media like USB drives, CDs and DVDs. Each device gets its own subfolder inside /media, often named after the volume label. It's the place where users can access the actual contents like photos, documents or software.
--/media is user-friendly and often doesn't require admnistrative priviliges. Desktop environments like GNOME or KDE handle this seamlessly, so your flash drive just appears ready use.
To clarify, --/dev holds the device files that represent the hardware itself, while --/media is where those devices are mounted and usable by the system.
## /mnt
Traditionally, this is where system administrators would manually mount external storage, like USB drives, partitions, backup disk or remote file systems, specially during system maintenance or recovery. 
Unlike /media, which automatically mounts removable devices for user access. 
--/mnt is reserved for manual, temporally mounts and is typically used by the root user or advanced scrips.
For example, if you need to access the contents of a failing hard drive or mount a network share during troubleshooting, /mnt is the go-to location.
## /proc
One of the unusual directories in Linux. Like /dev, /proc is vital for filesystem. It doesn't contain real files stored on disk, but instead provides a dynamic, in-memory view of the system.
While /dev represents hardware,
/proc acts as a live interface to the Linux kernel and running process. Files like /proc/cpuinfo and /proc/meminfo.
## /sys
Is a virtual directory like /proc, but with a different purpose. It's part of the sysfs pseudo file system and acts as a dynamic interface between the Linux  kernel and your hardware.
## /Run
This in-memory directory holds temporary runtime data used by the system and applications right after boot. It's created very early in the startup process, before most the filesystem is ready and everything inside it disappear on reboot. 
/run is writable and is uded by running processes to communicate, track state or sotre short-lived files process IDs and sockets.
## /srv 
Short for service. This is where data for services provided by the system like web servers, FTP servers or other hosted services is stored. Think of it as the content served to users connecting to your machine remotely. 
For example, if your system is running a web server, the actual website files might live under /srv/www.
## /var
The /var directory is used for storing files that change frequently during system operation like logs, caches, spool files and more.
For example, /var/log holds system logs that track activity and errors, and these logs are often rotated to prevent them from using too much space.
Package managers also use this directory. Debian-based systems for instance keep important metadata in /var/lib.
/var can contain sensitive information and should be properly protected, especially on multi-user or server setups.
## /tmp
This directory was designed for short-term use – /tmp.
This is where temporary files go, often created by applications or users while tasks are in progress. For example, when you open a file in a text editor or install a program, temporary working files may be stored here. These files aren't meant to stick around, they're typically deleted automatically on reboot or after a certain period.
/tmp is writable by all users, but it includes a special permission called the Sticky Bit.

## /opt
And lastly, we have /opt.
/opt is where optional or third-party software is installed, often kept separate from the system's main directories. Each application usually has its own subfolder, like /opt/google/chrome, which helps keep things organized and makes uninstalling easier.
This directory is especially common in enterprise or commercial environments where large, proprietary programs are installed outside the usual package manager paths.
On many systems, /opt may even be empty unless manually used. Because software here doesn't always follow standard Linux file structure rules, /opt provides a safe space without interfering with core system files.
Like most system directories, modifying it requires administrative privileges.

