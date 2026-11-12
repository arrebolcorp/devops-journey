## Terminal and File System Basics
When working in a Linux terminal, your command prompt is typically divided into parts that show information like the current user, host, and working directory. For example:

~ represents your home directory.

$ indicates a normal user prompt.

# indicates the root (admin) user.

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
