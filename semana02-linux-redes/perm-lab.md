# Linux Permissions & Ownership

## Core Concepts

| Concept | Summary / Notes |
| :--- | :--- |
| **Why Permissions Matter** | Permission bugs are the most common reason an app works locally on a laptop but fails on a server. In DevOps, service files must be readable only by the service's own user for security. |
| **Reading `ls -l`** | Example: `-rwxr-xr-- 1 vboxuser devteam 120 Nov 17 hello.sh`<br>• First character: file type (`-` = regular file, `d` = directory).<br>• Next 9 characters: three triplets for **owner** (`rwx`), **group** (`r-x`), and **others** (`r--`).<br>• Followed by the owner name (`vboxuser`) and group name (`devteam`). |
| **Permission Bits (Octal)** | `r` (read) = `4`, `w` (write) = `2`, `x` (execute) = `1`, `-` = `0`.<br>Add them per class:<br>• `644` (`rw-r--r--`): standard files.<br>• `755` (`rwxr-xr-x`): scripts and directories.<br>• `600` (`rw-------`): private files and SSH keys.<br>• `700` (`rwx------`): private directories. |
| **Which Class Applies** | Linux checks classes in order and picks **only one**: if you are the owner, only owner bits apply; otherwise, if you are in the file's group, group bits apply; otherwise, "others" bits apply. An owner can lock themselves out (`chmod 077`) even if group and others have full access. |
| **Permissions on Directories** | • `r`: lets you list file names inside.<br>• `x`: lets you enter/traverse the directory (`cd`).<br>• `w` + `x`: both are required to create, rename, or delete files inside the directory. |
| **Golden Rules** | • **Never use `777`** (gives write access to everyone).<br>• Be careful with recursive changes (`-R`).<br>• Only `root` (`sudo`) can transfer file ownership to another user. |

---

## Step-by-Step Testing

| Step | Command(s) Executed | Description & Result | Screenshot |
| :--- | :--- | :--- | :--- |
| **1. Initial Check** | `ls -l` | Listed files and directories in my home folder (`~`) to inspect default permissions, owners, and groups. | <img width="617" height="278" alt="image" src="https://github.com/user-attachments/assets/52a34c46-62b8-49ff-ac49-67c58ee80c73" /> |
| **2. Setup & File Creation** | `cd devops-lab`<br>`touch script-prueba.sh`<br>`ls -l script-prueba.sh` | Entered `devops-lab` and created an empty test file. By default, it was created with `-rw-rw-r--` (`664`) permissions owned by `vboxuser:vboxuser`. | <img width="544" height="62" alt="image" src="https://github.com/user-attachments/assets/68ac0562-5b3d-472e-939a-77982a1d587e" /> |
| **3. Symbolic `chmod`** | `chmod u+x script-prueba.sh`<br>`ls -l script-prueba.sh` | Added execute (`+x`) permission for the owner (`u`). Permissions changed to `-rwxrw-r--`. | <img width="531" height="57" alt="image" src="https://github.com/user-attachments/assets/b8984b97-a9b5-4a24-9c2f-367907653e8d" /> |
| **4. Numeric `chmod`** | `chmod 600 script-prueba.sh`<br>`ls -l script-prueba.sh` | Restricted permissions to read and write for the owner only (`-rw-------`), removing access for group and others. | <img width="527" height="57" alt="image" src="https://github.com/user-attachments/assets/7a4d3f46-bcb6-4176-a1e4-109b05c806ce" /> |
| **5. Inspect Metadata** | `stat script-prueba.sh` | Checked detailed file metadata, confirming octal permissions (`0600/-rw-------`), UID (`1000`), and GID (`1000`). | <img width="663" height="168" alt="image" src="https://github.com/user-attachments/assets/fdb3ab58-5c0e-4371-b1a5-37e26a6a84ad" /> |
| **6. Check Path Permissions** | `namei -l ~/devops-lab/script-prueba.sh` | Listed the permissions and ownership of every directory along the full path from `/` down to `script-prueba.sh`. | <img width="640" height="133" alt="image" src="https://github.com/user-attachments/assets/60e124c8-498e-4edc-9473-aa1ad2e81f78" /> |
| **7. Create Group & `chgrp`** | `sudo groupadd devteam`<br>`sudo chgrp devteam script-prueba.sh`<br>`ls -l script-prueba.sh` | Created a new group named `devteam` and changed the file's group ownership from `vboxuser` to `devteam`. |<img width="548" height="44" alt="image" src="https://github.com/user-attachments/assets/0a203820-0a09-4ce3-96d9-1b2f0961c60b" /> <img width="571" height="60" alt="image" src="https://github.com/user-attachments/assets/d43fa75a-5d07-4dd0-927b-ffbe88e143cd" /> |
| **8. Change Owner (`chown`)** | `sudo chown root:root script-prueba.sh`<br>`sudo chown vboxuser:vboxuser script-prueba.sh` | Transferred ownership of the file to `root:root` using `sudo`, and then restored it back to `vboxuser:vboxuser`. |<img width="672" height="62" alt="image" src="https://github.com/user-attachments/assets/9aaebc32-e287-4763-8cfe-8e7e7e11de2c" /> <img width="664" height="64" alt="image" src="https://github.com/user-attachments/assets/f956abd7-a560-4fb2-a70b-23c36f893754" /> |
| **9. Owner Lockout Test** | `chmod 077 script-prueba.sh`<br>`cat script-prueba.sh` | Removed all owner permissions (`0`) while granting full access (`77`) to group and others. Reading the file failed with `Permission denied` because Linux checks the owner class first. |<img width="519" height="59" alt="image" src="https://github.com/user-attachments/assets/17524959-7d36-4043-9670-c2b04521ea4b" /> |
| **10. Restore Permissions** | `chmod 644 script-prueba.sh`<br>`cat script-prueba.sh` | Restored standard file permissions (`-rw-r--r--`), allowing the owner to read the file normally again. | <img width="510" height="40" alt="image" src="https://github.com/user-attachments/assets/67f6ef4e-7858-49a5-86c9-0e768ae8b016" /> |

