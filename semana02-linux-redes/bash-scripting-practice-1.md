# Bash Scripting fundamentals
Today I introduced in bash scripting fundamentals and I did a practice using a some basic lines for this and I created an account of Digital Ocean for start practicing droplets for the Saturday.

# Key lines to remember
### #!/bin/bash 
This is the first line in a `.sh` file. This line tells Linux which program runs the file. A `#` it use for starts a coment.
### name="Alan"
This command don't have spaces around of `=`. Later we call the variable `name` with `$name`.
### $(date +%F) 
This command runs and get de date and it uses to output.
### Arguments
We can use `$+number` for generate argument for example; `$1` `$#` `$0`, where `$1` is the first argument, `$#` counts them, `$0` is the script name.

| Step | Command | For what | Lab |
|---|---|---|---|
| **1. Prepare the directory** | `mkdir -p ~/devops-lab/week2-lab/scripts`<br>`cd ~/devops-lab/week2-lab/scripts` | Created the `scripts` folder inside `week2-lab` using `-p` so parent folders are created if needed, then moved into it with `cd`. | <img width="601" height="245" alt="image" src="https://github.com/user-attachments/assets/8b6ff1d9-c0b7-4fd3-9c7c-ffef7b6e393c" /> |
| **2. First script (`hello.sh`)** | `vim hello.sh` *(press `i`, type lines, `Esc`, `:wq`, `Enter`)*<br>`./hello.sh`<br>`chmod u+x hello.sh`<br>`./hello.sh` | Created a simple Bash script with `vim`. Running `./hello.sh` first gave `Permission denied` because it had no execute bit. After `chmod u+x hello.sh`, it printed `Hello, DevOps!`. It's so important start own `.sh` file with `#!/bin/bash`| <img width="661" height="173" alt="image" src="https://github.com/user-attachments/assets/fccd0dbf-4942-4ff4-bcaf-050792331c56" /> |
| **3. Variables & quotes (`vars.sh`)** | `vim vars.sh` *(add script lines)*<br>`chmod u+x vars.sh`<br>`./vars.sh`<br>*(test `team = "devops"`, then remove it)* | Tested variables (`$name`, `$today`) and command substitution (`$(whoami)`, `$(hostname)`). Double quotes expand variables, while single quotes print `$name` literally. Spaces around `=` cause `command not found`. | <img width="644" height="312" alt="image" src="https://github.com/user-attachments/assets/2292f9fc-3666-4a0c-aa37-96962dac84c4" /> <img width="641" height="282" alt="image" src="https://github.com/user-attachments/assets/211041e5-2544-4a93-9a14-11aca2675a68" /> |
| **4. Arguments (`greet.sh`)** | `vim greet.sh` *(add `$0`, `$1`, `$2`, `$#` lines)*<br>`chmod u+x greet.sh`<br>`./greet.sh Ana Luis`<br>`./greet.sh`<br>`./greet.sh "Ana Maria" Luis` | Learned positional arguments (`$1`, `$2`), script name (`$0`), and argument count (`$#`). Quotes around `"Ana Maria"` keep it as a single argument, so the count stays `2`. |<img width="635" height="305" alt="image" src="https://github.com/user-attachments/assets/2f92af1e-9822-49fd-b0cd-608e50412df7" /> <img width="569" height="431" alt="image" src="https://github.com/user-attachments/assets/7853dad5-79d7-40f4-a940-dbd0b160aa2e" /> |
| **5. Exit codes (`check.sh`)** | `ls /etc/hostname`<br>`echo $?`<br>`ls /nonexistent`<br>`echo $?`<br>`vim check.sh` & `chmod u+x check.sh`<br>`./check.sh /etc/hostname`<br>`./check.sh /nonexistent` | Checked exit status with `$?` (`0` means success, non-zero like `2` means error). In `check.sh`, redirected output and errors to `/dev/null` (`> /dev/null 2>&1`) so only the exit code is shown. | <img width="518" height="155" alt="image" src="https://github.com/user-attachments/assets/bac28dd1-6fb1-4a28-864d-60afdafbaa9d" /> <img width="532" height="285" alt="image" src="https://github.com/user-attachments/assets/57a6c945-17ca-4f1b-9af5-89706817010e" /> |
| **6. System report v1 (`system-report.sh`)** | `vim system-report.sh` *(add report script)*<br>`chmod u+x system-report.sh`<br>`./system-report.sh` | Built a script that saves date, user, host, OS, disk (`df`), memory (`free`), and top 5 largest items in `~/devops-lab` (`du`) into a dated `.txt` file, then prints it with `cat`. | <img width="659" height="532" alt="image" src="https://github.com/user-attachments/assets/73997a11-82f5-47b3-8247-f7af0cf95fac" /> <img width="703" height="572" alt="image" src="https://github.com/user-attachments/assets/e7f7dbd5-14ad-4705-9705-7172236ae3e8" /> |
| **7. Add Uptime section** | `vim system-report.sh` *(add `uptime -p` before the last two lines)*<br>`./system-report.sh` | Updated `system-report.sh` to append (`>>`) a new `--- Uptime ---` section using `uptime -p` and ran it again to verify the updated report. | <img width="718" height="654" alt="image" src="https://github.com/user-attachments/assets/ca388863-c250-4114-b831-9ae25b4cfb01" /> <img width="682" height="513" alt="image" src="https://github.com/user-attachments/assets/0a8437ac-44cb-47fd-88c3-639efb072af9" /> |


## Quiz Answers

| # | Question | My Answer |
| :--- | :--- | :--- |
| **1** | What does `#!/bin/bash` on the first line do? | It is the **shebang**. It tells the Linux kernel which interpreter to use to run the script (`/bin/bash`), so the script runs with Bash even if you execute it directly with `./script.sh`. |
| **2** | Why does `name = "x"` fail but `name="x"` works? | In Bash, spaces around `=` are not allowed when assigning a variable. `name = "x"` makes the shell think `name` is a command with arguments `=` and `"x"`, causing `command not found`. `name="x"` creates the variable properly. |
| **3** | What is the difference between `"$name"` and `'$name'`? | Double quotes (`"$name"`) expand variables, so it prints the value stored inside `name`. Single quotes (`'$name'`) keep everything literal, so it prints the exact text `$name`. |
| **4** | What does `$(date +%F)` do? | It runs `date +%F` (which formats today's date as `YYYY-MM-DD`) and substitutes the output into a string or variable so you can use the current date dynamically, like in a report filename. |
| **5** | What does exit code `0` mean, and why does Jenkins care? | Exit code `0` means the command or script succeeded with no errors (any non-zero code means something failed). Jenkins checks exit codes to know if a pipeline step passed or failed—if a step returns a non-zero code, Jenkins marks the build/job as failed and stops or alerts you. |
