# Friday, Nov 20: Bash scripts II and environment variables

**Goal:** make `system-report.sh` smarter with a function, an `if` check and an environment variable.

**Where it fits:** it builds on Thursday's scripts and exit codes. It unlocks Saturday's SSH and droplet lab, and later Jenkins and Ansible.

## 3. Practice summary

### Step 1: environment variables
```bash
cd ~/devops-lab/week2-lab/scripts
echo $HOME
echo $USER
echo $PATH
APP_ENV="dev"
echo $APP_ENV
bash -c 'echo "Inside child: $APP_ENV"'
export APP_ENV
bash -c 'echo "Inside child: $APP_ENV"'
```
Expected: `/home/vboxuser`, `vboxuser`, a list of folders, `dev`, `Inside child: ` (empty), then `Inside child: dev` after `export`.

<img width="841" height="456" alt="image" src="https://github.com/user-attachments/assets/e5896ca7-db1c-4437-9ae8-a35423dadc0d" />


### Step 2 and 3: `disk-check.sh`
```bash
#!/bin/bash
limit="${DISK_LIMIT:-80}"
usage=$(df --output=pcent / | tail -1 | tr -d ' %')

if [ "$usage" -gt "$limit" ]; then
    echo "WARNING: disk usage is ${usage}% (limit ${limit}%)"
    exit 1
else
    echo "OK: disk usage is ${usage}% (limit ${limit}%)"
    exit 0
fi
```
```bash
chmod u+x disk-check.sh
./disk-check.sh
echo $?
DISK_LIMIT=10 ./disk-check.sh
echo $?
```
Expected: `OK ...` and `0`, then `WARNING ...` and `1`.

<img width="644" height="224" alt="image" src="https://github.com/user-attachments/assets/278a82a1-eef5-41ca-ad33-29404cfa1bc7" />


### Step 4 (and optional loop): `system-report.sh` v3
```bash
#!/bin/bash
# system-report.sh v3 - report with a function, an env variable and a folder check
report_dir="${REPORT_DIR:-.}"

if [ ! -d "$report_dir" ]; then
    echo "Error: $report_dir does not exist"
    exit 1
fi

report_file="$report_dir/system-report-$(date +%F).txt"

add_section() {
    echo "" >> "$report_file"
    echo "--- $1 ---" >> "$report_file"
}

echo "===== System report =====" > "$report_file"
echo "Date: $(date)" >> "$report_file"
echo "User: $(whoami)" >> "$report_file"
echo "Host: $(hostname)" >> "$report_file"

add_section "OS"
lsb_release -d >> "$report_file"
uname -r >> "$report_file"

add_section "Disk (/)"
df -h / | tail -1 >> "$report_file"

add_section "Memory"
free -h | head -2 >> "$report_file"

add_section "Largest folders in ~/devops-lab"
du -h --max-depth=1 ~/devops-lab 2>/dev/null | sort -rh | head -5 >> "$report_file"

add_section "Important folders"
for folder in /etc /var/log /tmp; do
    if [ -d "$folder" ]; then
        echo "OK: $folder exists" >> "$report_file"
    else
        echo "MISSING: $folder does not exist" >> "$report_file"
    fi
done

add_section "Uptime"
uptime -p >> "$report_file"

echo "Report saved to $report_file"
```
```bash
./system-report.sh
REPORT_DIR=/nonexistent ./system-report.sh
echo $?
mkdir -p ~/reports
REPORT_DIR="$HOME/reports" ./system-report.sh
```
Expected: `Report saved to ./system-report-<date>.txt`, then `Error: /nonexistent does not exist` and `1`, then the report saved in `/home/vboxuser/reports/`.

<img width="802" height="116" alt="image" src="https://github.com/user-attachments/assets/48103be8-7912-4da7-8313-39de68fcebca" />

<img width="804" height="551" alt="image" src="https://github.com/user-attachments/assets/e89032b2-1e56-4966-a53d-aa00b1012911" />


## 4. Fill-in-the-blank table: what each command does

### Step 1: environment variables
Word bank: child, commands, home, prints, spaces, username, variable, wq, X

| # | Command or syntax | Function |
|---|---|---|
| 1 | `cd ~/devops-lab/...` | `cd` Change the current folder. `~` means your home folder. |
| 2 | `echo $HOME` | `echo` prints text. `$HOME` holds the path of your home folder. |
| 3 | `echo $USER` | Prints your username. |
| 4 | `echo $PATH` | The folders where the shell looks for commands, separated by `:`. |
| 5 | `APP_ENV="dev"` | Creates a variable in the current shell. There are no spaces around `=`. |
| 6 | `bash -c '...'` | Starts a new bash, a child process, and runs the text in quotes. |
| 7 | `export APP_ENV` | Makes the variable available to child processes. |
| 8 | nano and vim exit | In nano press Ctrl+X to exit. In vim press Esc, then `:wq` to save and quit. |

### Step 2: `disk-check.sh`
Word bank: closes, current, execute, exit code, failure, false, greater than, header, last, deletes, output, owner, percent, shebang, spaces, success, true, value

| # | Command or syntax | Function |
|---|---|---|
| 9 | `chmod u+x file` | Gives the user owner permission to execute the file. |
| 10 | `./disk-check.sh` | Runs the file in the current folder. |
| 11 | `echo $?` | Prints the exit code of the last command. |
| 12 | `#!/bin/bash` | The shebang. It tells Linux which program runs the file. |
| 13 | `limit=80` | Stores a value in a variable. |
| 14 | `df --output=pcent /` | Prints a header line and then the percent used of the disk. |
| 15 | `tail -1` | Keeps only the last line. |
| 16 | `tr -d ' %'` | Deletes spaces and the `%` sign. |
| 17 | `$( ... )` | Captures the output of a command into a variable. |
| 18 | `[ ... ]` | A test command. It needs spaces inside the brackets. |
| 19 | `-gt` | Means greater than for numbers. |
| 20 | `then`, `else`, `fi` | `then` starts the true block. `else` runs when the test is false. `fi` closes the `if`. |
| 21 | `exit 1` | Stops the script and reports failure. A CI tool marks the job as failed. |
| 22 | `exit 0` | Reports success. |

### Step 3: a setting from the environment
Word bank: default, one

| # | Command or syntax | Function |
|---|---|---|
| 23 | `${DISK_LIMIT:-80}` | Uses `DISK_LIMIT`, or the default value `80` if it is not set. |
| 24 | `DISK_LIMIT=10 ./disk-check.sh` | Sets the variable for this one run only. |

### Step 4: `system-report.sh`

| # | Command or syntax | Function |
|---|---|---|
| 25 | `${REPORT_DIR:-.}` | The `.` means the current folder. |
| 26 | `-d` | True if the path exists and is a directory. |
| 27 | `!` | Means not. |
| 28 | `date +%F` | Prints today's date as YYYY-MM-DD. |
| 29 | `add_section() { ... }` | Defines a function. `$1` is its first argument. |
| 30 | `>` | Creates a file or overwrites it. |
| 31 | `>>` | Appends to the end of a file. |
| 32 | `lsb_release -d` | Shows the Ubuntu version. |
| 33 | `uname -r` | Shows the kernel version. |
| 34 | `df -h /` | Shows disk usage in human-readable units. |
| 35 | `free -h` | Shows memory in human-readable units. |
| 36 | `head -2` | Keeps the first 2 lines. |
| 37 | `du -h --max-depth=1` | Shows sizes of the folder and its direct subfolders. |
| 38 | `2>/dev/null` | Throws away error messages. |
| 39 | `sort -rh` | Sorts sizes with the biggest first. |
| 40 | `head -5` | Keeps the first five lines. |
| 41 | `uptime -p` | Shows how long the machine has been on. |
| 42 | `mkdir -p` | Creates a folder and gives no error if it already exists. |
| 43 | `REPORT_DIR=/nonexistent ./system-report.sh` | Tests the if check. You see an error and exit code 1. |

### Optional: the `for` loop
Word bank: current, else, item, loop, appends, folder

| # | Command or syntax | Function |
|---|---|---|
| 44 | `for folder in /etc /var/log /tmp; do` | Repeats the block once per item. |
| 45 | `"$folder"` | Holds the current item of the list in each round. |
| 46 | `-d "$folder"` | True if the folder exists. |
| 47 | `echo "OK: ..." >> "$report_file"` | Appends the line to the report. |
| 48 | `echo "MISSING: ..."` | Runs in the else branch when the folder does not exist. |
| 49 | `done` | Closes the loop. |

## 5. Quiz: write your answers in your own words

1. What does `export` do?
Turns a regular variable in the shell into an environment varible, it gets passed down to child processes (susch as subshells or scripts you run from my current session)
 
2. What does `${DISK_LIMIT:-80}` mean?
It sets a default value for a variable: if `DISK_LIMIT` is unset or empty. Bash uses `80`. If `DISK_LIMIT` already has a value assigned, it uses that value instead.

3. Why does `[ "$usage" -gt "$limit" ]` need spaces inside the brackets?
Because in bash. `[` is actually a built-in command and `]` is its final argument. Without spaces, Bash treats them as a single joined word and causes a syntax error.

4. Why does `exit 1` matter to Jenkins?
In Linux CI/CD pipelines, any non-zero exit code such as `exit 1` signals that a command or script *failed*. Jenkins reads this exit code to mark the build as failed (`FAILURE`), stop the pipeline, and alert the team instead of continuing with broken steps.

5. What does a function save you from repeating in `system-report.sh`?
It saves you from repeating the same formatting o logic blocks multiple times-such as printing section headers, appending output (`>>`) to the report file, or running repetitive checks. If I need to update how a section looks, you only have to edit in *one place*.

6. In the `for` loop, what does `folder` hold in each round?
In each iteration (round) of the loop, the variable `folder` holds *one folder path or item* from the list at a time, allowing the script to process each folder individually before moving to the next one.

7. What is the difference between `>` and `>>`?
`>` overwrite: creates the file if it doesn't exist, or erases all existing content before writing the new output.
`>>` append: creates the file if it doesn't exist, or *adds the new output to the end* without deleting previous lines.

