## What I practiced this week
To sump up, this week was a tough week because I studied a lot of new concepts and I practiced new commands and new OS. 
But, I suppose that it's a part to try some new. 

Well, I would like resume some commands that I was practiced and today I practice to create a new file example.source using 'vim' and I practiced moving folder-to-folder.

### Navigation: 
pwd, ls, cd.
### Files: 
mkdir -p, touch, cp, mv, rm -i.
### Reading: 
cat, less, head, tail.
### System: 
whoami, uname -r, lsb_release -a, df -h, free -h, du -sh.
### Help: 
man, --help, history.
### Admin and apt: 
sudo, apt update, apt install, apt purge, apt autoremove, apt show, apt policy, dpkg -l, dpkg -L.

I had a lot of mistakes while I'm practicing. But, I analyzed my mistakes, and don't stop for try. 
For example, I had an error while practiced the command 'rm' and I wrote 'rn' and to finally I had to install a repo named trn4, and well, my bad. I fixed and removing this repository.

You can review my 'history of commands lines and my explain about this and SS with that I worked for today and thorough this week.

<img width="401" height="322" alt="image" src="https://github.com/user-attachments/assets/009b9c87-6348-487e-8e98-4a032b260603" />
<img width="431" height="331" alt="image" src="https://github.com/user-attachments/assets/307bac99-ef8f-485f-bc9c-2116cd7a2701" />
<img width="257" height="332" alt="image" src="https://github.com/user-attachments/assets/41b202cd-5936-499b-bae6-9191017749c0" />

# Resume

### sudo whoami 
This command review if I have admin / root permission.
<img width="170" height="41" alt="image" src="https://github.com/user-attachments/assets/7d94352d-bd02-4dd3-854a-8a6f149d5f3b" />

### lsb_release -a
Prints datail version of Linux that I have.
<img width="107" height="44" alt="image" src="https://github.com/user-attachments/assets/20d005c0-431c-4d76-9884-a6abf2af305b" />

### pwd 
Prints my current directory
<img width="162" height="17" alt="image" src="https://github.com/user-attachments/assets/01af6e14-1312-40e0-a398-59fd124abf51" />

### ls
Prints the list of files or folder into the my current directory
<img width="314" height="17" alt="image" src="https://github.com/user-attachments/assets/d227214b-3a97-4a38-81b6-54f16ab6278b" />

## ls -a
If add -a in ls prints all files and folder until hide files and folders.
<img width="599" height="26" alt="image" src="https://github.com/user-attachments/assets/9dbb788d-ab21-436d-a465-5290684eca54" />

### ls -lah ~
Prints to detail any document in format easy to read. Shows all files and yours sizes. 
<img width="257" height="199" alt="image" src="https://github.com/user-attachments/assets/273c7836-60f0-48b8-8bf4-a43af308d49c" />

### cd ..
Up to the next folder in the structure.
<img width="98" height="26" alt="image" src="https://github.com/user-attachments/assets/bafd06c7-c0c9-4cf4-b7b7-e089a07b5e89" />

### cd -
It turn back you and the previous folder before that you apply the last command.
<img width="83" height="23" alt="image" src="https://github.com/user-attachments/assets/fc66f9d8-4249-4b53-bbca-70de63768091" />

### cd ~
Turn back to personal main folder.
<img width="89" height="23" alt="image" src="https://github.com/user-attachments/assets/2eec0e7a-96d2-46d9-82ad-b483981a7b23" />

###  cd /etc
Redirecting to repository /etc
<img width="97" height="17" alt="image" src="https://github.com/user-attachments/assets/82533606-9e67-4cfa-a227-ab4d577ce326" />

### mkdir -p devops-lab/notes
Creates a new folder, -p to create a folder.

### touch notes-demo.txt
Touch has a funtion to create a empty file.

### cp -r notes-demo.txt backup.txt
If I want to create a copy of any file I have to use cp -r + file 1 + new file. Note: In my current practice, I have a many mistakes here, because I need to write correctly and complete all name and type of file.

### mv backup.txt notes-demo2.txt
With mv rename a file backup.txt to notes.demo2.txt

### cat /etc/os-release
Cat helps us to read some file
<img width="230" height="88" alt="image" src="https://github.com/user-attachments/assets/2a8b1986-acdb-4de6-bd2a-4a3248683009" />

###  less /var/log/dpkg.log
Helps us to read and review in an interactive form.
<img width="236" height="325" alt="image" src="https://github.com/user-attachments/assets/6fb01432-ae47-4a5a-9f49-93e75b98f948" />

### head -n4 /var/log/dpkg.log
Has a function for show X numbers of lines with -n+X on any file to read.
<img width="176" height="43" alt="image" src="https://github.com/user-attachments/assets/8a194ef2-2e14-465d-b28a-bacde9fe1012" />

### tail -n5 /var/log/dpkg.loh
 Is the opposity of head, here show the last x numbers of lines with -n5
 <img width="193" height="53" alt="image" src="https://github.com/user-attachments/assets/6aaedd9f-6e82-445b-b82f-0e22d4f1f28a" />
 
###  df -h
Prints the available space in the all partiton storage.
<img width="191" height="80" alt="image" src="https://github.com/user-attachments/assets/18a8f0b0-c686-4924-ac99-988e9b7e7fcc" />

### free -h
Prints the available spaces of RAM.
<img width="188" height="45" alt="image" src="https://github.com/user-attachments/assets/20fb1cb4-8e4a-489a-959d-acfc19596889" />

###  du -sh
Helps us for show the size of the current folder that have select.
<img width="116" height="23" alt="image" src="https://github.com/user-attachments/assets/0249ebc2-98f2-4195-ac4c-352afb76c843" />

###  man + command
Helps us to show the manual of use the any command.

### ls --help
--help helps us to show the faster form and resume the use of the comand.
<img width="188" height="133" alt="image" src="https://github.com/user-attachments/assets/cf8e454e-adbe-49da-b3df-e4df2f9267db" />

### sudo apt update
search and uptades new releases available in our packages.

### sudo apt install tree
Installing the package named tree.

### history
prints the history of the all commands wrote.

###  sudo apt purge trn4
Purgue helps us to remove at raiz a package (files and configurations). Remove has a function to remove only files. 

### sudo -l trn4
Consulting if have files over.

###  sudo apt autoremove
helps to search all package without use and removed.

###  vi --version
Consulting vim version

### vim testfile
Creates a new file for test, I can give the type of file adding .txt, .source etc.

###  vimtutor
open the tutorial where teach how to use vim.

 

