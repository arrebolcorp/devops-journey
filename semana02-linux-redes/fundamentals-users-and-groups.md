# Fundamental Concepts: Users and Groups

## Core Concepts

| Concept | Summary / Notes |
| :--- | :--- |
| **Multi-user & Least Privilege** | Linux is an OS multi-user: every file and process belongs to a user. In DevOps (Docker, Jenkins, Nexus), apps run under their own limited user rather than `root`. |
| **`root` vs. Normal Users** | `root` is the superuser (`UID 0`). Normal users start at `UID 1000`. |
| **Groups** | Each user has one primary group and any number of supplementary groups to share access efficiently. |
| **Key System Files** | `/etc/passwd` (user accounts), `/etc/group` (group definitions), `/etc/shadow` (encrypted password hashes — restricted access). |
| **`sudo`** | Runs a single command with `root` privileges instead of switching completely to the `root` account. |

---

## Lab Questions & Answers

| # | Lab / Question | Explanation |
| :--- | :--- | :--- |
| **1** | Find your username, UID and groups in one command. Which group gives you `sudo`? | *The difference that are when I type with sudo is that prints a diffent ID* <img width="1148" height="93" alt="image" src="https://github.com/user-attachments/assets/cfb84d20-50d0-4438-90e6-89a9dd654339" /> |
| **2** | Find your own line in `/etc/passwd` and explain its 7 fields. *(Hint: separator is `:`)* | *boxuser:x:1000:1000:vboxuser:/home/vboxuser:/bin/bash* My user in Home with vboxuser has been normal user. Ando shows the name, UID, GID, personal folder and the shell assign. <img width="567" height="72" alt="image" src="https://github.com/user-attachments/assets/bd3ac912-0bf8-4305-b1d5-240328873681" /> |

---

## Lab Evidence & Command Execution

| Command / Step | My Notes / Explanation | Screenshot |
| :--- | :--- | :--- |
| **`sudo whoami`** | *I recibed superuser permission, back `root` to confirm the root permission* | <img width="370" height="69" alt="image" src="https://github.com/user-attachments/assets/d564da04-4306-4144-b4b8-6774478a1074" /> |
| **`cat /etc/passwd`** | *Shows the content where are register all user system* | <img width="495" height="194" alt="image" src="https://github.com/user-attachments/assets/c7b53319-c51b-4604-992b-2a54b6ebcee5" /> |
| **`cat /etc/group`** | *Prints the list of all groups in the system, your GID (ID) and what users are form that group* | <img width="418" height="346" alt="image" src="https://github.com/user-attachments/assets/688d8686-bba9-4e03-a908-ee3a031e7c4b" /> |
| **`cat /etc/shadow`** | *Here, try to show the file but I cannot for problems with permissions user* Is a file with sensitive information (passwords etc.) | <img width="391" height="53" alt="image" src="https://github.com/user-attachments/assets/0f0ef4b1-da26-4572-a512-843c4797253a" /> |
| **`id`** | *Shows in only line my identity, UID, principal GID and all my groups.* | <img width="1159" height="66" alt="image" src="https://github.com/user-attachments/assets/632e362a-8c74-401e-bffe-c5561e50a9d9" /> |
| **`groups`** | *The faster for printing all groups and their information* | <img width="556" height="47" alt="image" src="https://github.com/user-attachments/assets/8cf40483-e896-4fb1-8260-9f1ac39b78de" /> |
| **`sudo adduser labuser`** | *Create a new user named `labuser` this have to create that interactive form a folder named `/home/labuser`* | <img width="968" height="366" alt="image" src="https://github.com/user-attachments/assets/1e86ce1b-5c0c-444c-be7a-3a4f476fff47" /> |
| **`ls /home`** | *Prints the personal folders inside `/home`* | <img width="506" height="65" alt="image" src="https://github.com/user-attachments/assets/12abfa0e-3293-48da-9473-b0cc9366a696" /> |
| **`sudo groupadd devteam`** | *Create a new group `devteam`* | <img width="496" height="79" alt="image" src="https://github.com/user-attachments/assets/dc8b31bd-b8bf-4b3e-9e31-adf343364981" /> |
| **`tail /etc/group`** | *Confirm the last ten lines of `/etc/group` to verify the creation of group `devteam`* | <img width="428" height="205" alt="image" src="https://github.com/user-attachments/assets/3959a8d1-0796-4801-a9cf-51fba0c47775" /> |
| **`sudo usermod -a -G devteam labuser`**<br>**`groups labuser`** | *Add the new user `labuser` in the new groups `devteam` and consult in what group are been `labuser` to confirm the correct movement* | <img width="532" height="64" alt="image" src="https://github.com/user-attachments/assets/d5d2c92f-4e24-4ad8-8111-09effdc4f897" /> |
| **`id labuser`** | *Shows the `id` of `labuser`* | <img width="695" height="42" alt="image" src="https://github.com/user-attachments/assets/41563d3d-c1c3-47a1-bd18-0f670b127680" /> |
| **New User Created: `labuser`** | *Shows the start session menu both user `labuser` and `vboxuser`* | <img width="874" height="688" alt="image" src="https://github.com/user-attachments/assets/6c89a8d1-71a3-4f24-9e2e-d7aa2884b18b" /> |
| **`ls`** | *Log in with `labuser` and review the folders and files* | <img width="666" height="274" alt="image" src="https://github.com/user-attachments/assets/08d5935b-5f7c-42fa-b0fd-62ee6cb43b38" /> |
| **`sudo ls /root`** | *Here, I try to list the `ls/root` but with this user don't have permissions because `labuser` doensn't have in root group* | <img width="472" height="139" alt="image" src="https://github.com/user-attachments/assets/b8db31b6-523a-45e6-a989-b0eeb315200d" /> |
| **`sudo gpasswd -d labuser devteam`** | *I remove `labuser` from `devteam`* | <img width="491" height="119" alt="image" src="https://github.com/user-attachments/assets/84ea1bda-3c96-46d9-8ecf-9f78ecbb0191" /> |
| **`sudo groupdel devteam`** | *Here, I delete the group `devteam` * | <img width="505" height="148" alt="image" src="https://github.com/user-attachments/assets/8b9adc97-cebc-4ac8-b968-e38715d125ac" /> |
| **`sudo userdel labuser`** | *I delete the user `labuser`* | <img width="1032" height="97" alt="image" src="https://github.com/user-attachments/assets/2abe3247-5dcf-4909-8954-dd0ecb35b050" /> |
| **`cat /etc/passwd`** | *Confirm that the user has been removed of the list of users.* | <img width="562" height="91" alt="image" src="https://github.com/user-attachments/assets/3742c218-72e6-45ec-bfbc-e1f0cd47f9db" /> |
