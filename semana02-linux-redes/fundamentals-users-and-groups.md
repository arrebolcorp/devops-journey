# Fundamental Concepts: Users and Groups

## Lab Questions & Answers

| # | Lab / Question | Explanation |
| :--- | :--- | :--- |
| **1** | Find your username, UID and groups in one command. Which group gives you `sudo`? | The command `id` prints my username (`vboxuser`), my UID (`1000`), and all my groups in one line. The group that gives me administrative permissions is **`sudo`** (`27(sudo)`). |
| **2** | Find your own line in `/etc/passwd` and explain its 7 fields. *(Hint: separator is `:`)* | `vboxuser:x:1000:1000:vboxuser,,,:/home/vboxuser:/bin/bash`<br>1. `vboxuser`: Username.<br>2. `x`: Password placeholder (the actual password hash is stored safely in `/etc/shadow`).<br>3. `1000`: UID (User ID).<br>4. `1000`: GID (Primary Group ID).<br>5. `vboxuser,,,`: GECOS field (extra user information or full name).<br>6. `/home/vboxuser`: User's home directory.<br>7. `/bin/bash`: Default login shell. |
| **3** | Create the user `labuser` with a home directory, and the group `devteam`. | I used `sudo adduser labuser` and `sudo groupadd devteam`. I chose `adduser` instead of `useradd` because `adduser` is an interactive script that automatically creates the `/home/labuser` folder and prompts for a password, while `useradd` is a low-level command that requires extra flags to do the same. |
| **4** | Add `labuser` to `devteam` without losing its other groups. What happens if you run `usermod` without `-a`? | Using `sudo usermod -aG devteam labuser` appends (`-a`) the new group without removing existing ones. When I tested adding a second group (`qa`) using `sudo usermod -G qa labuser` **without `-a`**, it overwrote the supplementary groups and `labuser` lost its membership in `devteam`. |
| **5** | Prove it with `id` and `getent group`. | Running `id labuser` and `getent group devteam` confirmed that `labuser` belongs to its primary group (`labuser`) and its supplementary groups. |
| **6** | Switch to `labuser` and try `sudo ls /root`. What happens, and why? | The command fails with the message: `labuser is not in the sudoers file. This incident will be reported.` This happens because `labuser` is not in the `sudo` group, demonstrating the **least privilege** principle in action. |
| **7** | Delete the user (with its home) and the group, then verify they’re gone. | Running `sudo userdel labuser` without `-r` removed the user from `/etc/passwd`, but left `/home/labuser` behind. When I ran `ls -l /home`, the owner showed as `1001 1001` (the raw UID/GID) because Linux could no longer map that ID to a username. I deleted the leftover folder with `sudo rm -rf /home/labuser` and removed the group with `sudo groupdel devteam`. |

---

## Lab Questions & Answers

| # | Lab / Question | Explanation |
| :--- | :--- | :--- |
| **1** | Find your username, UID and groups in one command. Which group gives you `sudo`? | *The command line is in one line* <img width="1148" height="93" alt="image" src="https://github.com/user-attachments/assets/cfb84d20-50d0-4438-90e6-89a9dd654339" /> |
| **2** | Find your own line in `/etc/passwd` and explain its 7 fields. *(Hint: separator is `:`)* | *boxuser:x:1000:1000:vboxuser:/home/vboxuser:/bin/bash* My user in Home with vboxuser has been normal user. Ando shows the name, UID, GID, personal folder and the shell assign. <img width="567" height="72" alt="image" src="https://github.com/user-attachments/assets/bd3ac912-0bf8-4305-b1d5-240328873681" /> |

---

## Lab Evidence & Command Execution

| Command / Step | My Notes / Explanation | Screenshot |
| :--- | :--- | :--- |
| **`sudo whoami`** | *I received superuser permission; the terminal returned root to confirm administrative access.* | <img width="370" height="69" alt="image" src="https://github.com/user-attachments/assets/d564da04-4306-4144-b4b8-6774478a1074" /> |
| **`cat /etc/passwd`** | *Shows the file where all system user accounts are registered.* | <img width="495" height="194" alt="image" src="https://github.com/user-attachments/assets/c7b53319-c51b-4604-992b-2a54b6ebcee5" /> |
| **`cat /etc/group`** | *Prints the list of all groups in the system, their GIDs, and which users belong to each group.* | <img width="418" height="346" alt="image" src="https://github.com/user-attachments/assets/688d8686-bba9-4e03-a908-ee3a031e7c4b" /> |
| **`cat /etc/shadow`** | *Tried to read the file, but got a Permission denied error because regular users cannot access it. It stores encrypted password hashes (not plain-text passwords) for security. | <img width="391" height="53" alt="image" src="https://github.com/user-attachments/assets/0f0ef4b1-da26-4572-a512-843c4797253a" /> |
| **`id`** | *Shows my full identity in a single line: UID, primary GID, and all supplementary groups.* | <img width="1159" height="66" alt="image" src="https://github.com/user-attachments/assets/632e362a-8c74-401e-bffe-c5561e50a9d9" /> |
| **`groups`** | *A faster command that prints only the names of the groups my user belongs to (without the ID numbers). * | <img width="556" height="47" alt="image" src="https://github.com/user-attachments/assets/8cf40483-e896-4fb1-8260-9f1ac39b78de" /> |
| **`sudo adduser labuser`** | *Created a new user named labuser interactively, automatically generating /home/labuser and setting a throwaway password.* | <img width="968" height="366" alt="image" src="https://github.com/user-attachments/assets/1e86ce1b-5c0c-444c-be7a-3a4f476fff47" /> |
| **`ls /home`** | *Prints the personal folders inside `/home`* | <img width="506" height="65" alt="image" src="https://github.com/user-attachments/assets/12abfa0e-3293-48da-9473-b0cc9366a696" /> |
| **`sudo groupadd devteam`** | *Create a new group `devteam`* | <img width="496" height="79" alt="image" src="https://github.com/user-attachments/assets/dc8b31bd-b8bf-4b3e-9e31-adf343364981" /> |
| **`tail /etc/group`** | *Confirm the last ten lines of `/etc/group` to verify the creation of group `devteam`* | <img width="428" height="205" alt="image" src="https://github.com/user-attachments/assets/3959a8d1-0796-4801-a9cf-51fba0c47775" /> |
| **`sudo usermod -a -G devteam labuser`**<br>**`groups labuser`** | *Added labuser to the devteam group while keeping existing groups (-a), and verified the change with groups labuser.* | <img width="532" height="64" alt="image" src="https://github.com/user-attachments/assets/d5d2c92f-4e24-4ad8-8111-09effdc4f897" /> |
| **`id labuser`** | *Shows the `id` of `labuser`* | <img width="695" height="42" alt="image" src="https://github.com/user-attachments/assets/41563d3d-c1c3-47a1-bd18-0f670b127680" /> |
| **New User Created: `labuser`** | *Shows the start session menu both user `labuser` and `vboxuser`* | <img width="874" height="688" alt="image" src="https://github.com/user-attachments/assets/6c89a8d1-71a3-4f24-9e2e-d7aa2884b18b" /> |
| **`ls`** | *Log in with `labuser` and review the folders and files* | <img width="666" height="274" alt="image" src="https://github.com/user-attachments/assets/08d5935b-5f7c-42fa-b0fd-62ee6cb43b38" /> |
| **`sudo ls /root`** | *Tried to list /root as labuser, which was denied with labuser is not in the sudoers file because labuser has no sudo privileges.* | <img width="472" height="139" alt="image" src="https://github.com/user-attachments/assets/b8db31b6-523a-45e6-a989-b0eeb315200d" /> |
| **`sudo gpasswd -d labuser devteam`** | *I remove `labuser` from `devteam`* | <img width="491" height="119" alt="image" src="https://github.com/user-attachments/assets/84ea1bda-3c96-46d9-8ecf-9f78ecbb0191" /> |
| **`sudo groupdel devteam`** | *Here, I delete the group `devteam` * | <img width="505" height="148" alt="image" src="https://github.com/user-attachments/assets/8b9adc97-cebc-4ac8-b968-e38715d125ac" /> |
| **`sudo userdel labuser`** | *Deleted the user labuser and cleaned up its leftover /home/labuser directory (which showed 1001 as the numeric owner after user deletion).* | <img width="1032" height="97" alt="image" src="https://github.com/user-attachments/assets/2abe3247-5dcf-4909-8954-dd0ecb35b050" /> |
| **`cat /etc/passwd`** | *Confirm that the user has been removed of the list of users.* | <img width="562" height="91" alt="image" src="https://github.com/user-attachments/assets/3742c218-72e6-45ec-bfbc-e1f0cd47f9db" /> |
