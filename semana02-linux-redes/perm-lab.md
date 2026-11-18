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

# Week 2 Lab

## Command Reference & Evidence Matrix

| Step | Command | Function | Why in DevOps? | Evidence (Output / Screenshot) |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `mkdir -p ~/devops-lab/week2-lab/umask-lab` | Creates nested directories recursively without throwing errors if they already exist. | Ensures idempotency in setup scripts and CI/CD workspace initialization. | `*<img width="603" height="34" alt="image" src="https://github.com/user-attachments/assets/56f0138e-dff3-4b35-a16a-e04ab46574dd" />*` |
| **1** | `cd ~/devops-lab/week2-lab/umask-lab` | Changes the current working directory into the lab workspace. | Isolates test artifacts to prevent accidental changes to system or root folders. | `*<img width="520" height="34" alt="image" src="https://github.com/user-attachments/assets/4fba6d8c-ea41-4707-8b89-863e3735bdc3" />*` |
| **1** | `umask` | Displays the current user file-creation mode mask. | Audits the default security baseline applied to newly created logs, configs, and artifacts. | `0022` *(or your output)* |
| **1** | `(umask 022; touch f1; mkdir d1); (umask 002; touch f2; mkdir d2); (umask 077; touch f3)` | Runs subshells with temporary `umask` values to create test files and directories. | Tests permission isolation (e.g., `077` for secrets/SSH keys vs. `002` for shared team repos) without altering the global session. | `*<img width="1142" height="34" alt="image" src="https://github.com/user-attachments/assets/86b2cf44-a806-420e-957f-9123d7438f57" />*` |
| **1** | `ls -ld f* d*` | Lists detailed metadata and permission bits for the matching files and directories themselves (`-d`). | Verifies that automated builds generate artifacts with the expected read/write/execute bits. | `-rw-r--r-- f1`, `drwxr-xr-x d1`, `-rw-rw-r-- f2`, `drwxrwxr-x d2`, `-rw------- f3` <img width="620" height="119" alt="image" src="https://github.com/user-attachments/assets/89de7ae7-71d9-4f72-9220-42a284c343e9" /> |
| **2** | `echo 'echo hi' > ~/t.sh` | Creates a simple shell script containing a print command inside the home directory. | Simulates a deployment script or build step stored in a specific filesystem path. | `*<img width="675" height="34" alt="image" src="https://github.com/user-attachments/assets/fa75455f-b15c-4eab-969a-d89cffeb2a1a" />*` |
| **2** | `chmod 755 ~/t.sh` | Grants full permissions (`rwx`) to the owner and read/execute (`r-x`) to group and others. | Standard permission mode required for executable scripts run by automation tools. | `*<img width="600" height="34" alt="image" src="https://github.com/user-attachments/assets/96470083-53c1-4a27-8e17-87ccfc015e62" />*` |
| **2** | `sudo -u nobody ~/t.sh` | Executes the script impersonating the unprivileged `nobody` user. | Replicates how CI/CD runners (like Jenkins or GitLab Runner) execute jobs under restricted service accounts. | `sudo: unable to execute .../t.sh: Permission denied` |
| **2** | `id nobody` | Displays the User ID (UID), Group ID (GID), and supplementary groups of `nobody`. | Confirms the exact identity and group memberships a service account possesses when debugging access issues. | `uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)` |
| **2** | `namei -l ~/t.sh` | Resolves a pathname down to its endpoint, listing owner and permissions for every parent directory. | Quickly pinpoints which parent folder in a deep path lacks execute (`x`) traversal permissions during a `Permission denied` error. | `drwxr-x---` on `/home/<user>` blocking traversal |
| **2** | `rm ~/t.sh` | Deletes the temporary test script. | Keeps build agents and environments clean after testing or pipeline execution. | `*<img width="657" height="264" alt="image" src="https://github.com/user-attachments/assets/db9afd08-48bc-4467-9bf6-63c804852eaa" />*` |

---

## Part A: Tuesday Follow-ups

### Step 1: Default Permission Control with `umask`
* **Command:** `mkdir -p ~/devops-lab/week2-lab/umask-lab && cd $_`, `umask`, `(umask 022; touch f1; mkdir d1); (umask 002; touch f2; mkdir d2); (umask 077; touch f3)`, `ls -ld f* d*`
* <img width="499" height="47" alt="image" src="https://github.com/user-attachments/assets/7127be47-fcd6-4f05-a4bf-26e94889b53a" />
<img width="613" height="133" alt="image" src="https://github.com/user-attachments/assets/865aea3e-7541-4c4f-b731-95e062dfbaf0" />

* **What I saw:**
  * `umask 022` resulted in `f1` having `-rw-r--r--` (`644`) and `d1` having `drwxr-xr-x` (`755`).
  * `umask 002` resulted in `f2` having `-rw-rw-r--` (`664`) and `d2` having `drwxrwxr-x` (`775`).
  * `umask 077` resulted in `f3` having `-rw-------` (`600`), restricting access completely to the owner.
* **What I learned:** `umask` acts as a security baseline in DevOps pipelines to ensure newly generated artifacts, logs, and configuration files follow the principle of least privilege automatically.

### Step 2: Simulating Restricted CI/CD Runners
* **Command:** `echo 'echo hi' > ~/t.sh`, `chmod 755 ~/t.sh`, `sudo -u nobody ~/t.sh`, `id nobody`, `namei -l ~/t.sh`, `rm ~/t.sh`
* **What I saw:** Even though `~/t.sh` had `755` permissions, executing it as `nobody` failed with `Permission denied`. Running `namei -l` revealed that the parent home directory had `drwxr-x---` (`750`) permissions, blocking `nobody` from traversing the path.
* <img width="631" height="288" alt="image" src="https://github.com/user-attachments/assets/ebcc1cd4-af12-443f-8776-c4c6fa5e53bb" />
* **What I learned:** A file's own permissions are useless if the service account running a CI/CD job lacks execute (`x`) traversal permissions on every parent directory leading to that file.

### Step 3: Key Takeaways
* “umask is a **bitmask** that removes permission bits from new files and folders. New files start at **666 (`rw-rw-rw-`)** and new folders at **777 (`rwxrwxrwx`)**. With umask 0002 a new file gets **664 (`-rw-rw-r--`)**, and with 0022 it gets **644 (`-rw-r--r--`)**.”
* “When Jenkins gets ‘Permission denied’, I check three things: **`ls -l`** shows the file’s owner and mode, **`id`** shows which user and groups run the job, and **`namei -l`** shows the permissions of every folder in the path.”
