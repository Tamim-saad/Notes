## **🔄 `mv` – Move or Rename Files and Directories**

---

### **✅ Purpose**

* Move files or directories from one place to another

* Rename files or directories

---

### **📌 Basic Syntax**

mv \[options\] source target

---

### **🧪 Examples and Use Cases**

| Command | Description |
| ----- | ----- |
| `mv file1 file2` | Renames `file1` to `file2`. Overwrites `file2` if it exists. |
| `mv file folder/` | Moves `file` **into** `folder/` if folder exists |
| `mv folder1 folder2` | If `folder2` **doesn’t exist** → renames `folder1` to `folder2` |
|  | If `folder2/` **exists** → moves `folder1` **inside** `folder2/` |
| `mv *.txt folder/` | Moves all `.txt` files into `folder/` |
| `mv file1 file2 folder/` | Moves both `file1` and `file2` into `folder/` |
| `mv dir1/* dir2/` | Moves all contents of `dir1/` into `dir2/` |
| `mv *.sh ../` | ✅ Moves all `.sh` files to parent directory. |
| `mv folder1/* .` | Moves all contents of `folder1/` to current directory |
| `Mv folder1/* “$(pwd)”` | Also moves all contents of `folder1/` to current directory |

---

### **⚠️ What Happens If Target Exists?**

#### **🗂️ `mv file1 file2`**

* If `file2` **exists** → **Overwrites** it silently

Use `-i` to confirm before overwrite:

 mv \-i file1 file2

* 

#### **📁 `mv folder1 folder2`**

* If `folder2` **exists** → `folder1` is moved **into** `folder2/`

* If `folder2` **does not exist** → `folder1` is **renamed** to `folder2`

---

### **🛠️ Common Options**

| Option | Description |
| ----- | ----- |
| `-i` | Prompt before overwrite (interactive) |
| `-n` | Never overwrite existing files |
| `-v` | Verbosely show files as they are moved/renamed |
| `-u` | Move only if source is newer than destination |

---

### **📌 Special Notes**

* `mv file file` → No effect (source and target are the same)

* You **can't move a folder into a file**

* You **can move a file into a folder**

* Overwriting is **silent by default**, so use `-i` for safety

---

---

### **📂 `cd` Command – Change Directory**

`cd` stands for **"change directory"**, and it's used to navigate between directories in the terminal.

---

### **✅ Basic Syntax:**

cd \[directory\_path\]

---

### **🧭 Common Usages:**

| Command | Meaning |
| ----- | ----- |
| `cd folder1` | Go into `folder1` (a subdirectory of current directory) |
| `cd ..` | Move **one level up** (to parent directory) |
| `cd ../..` | Move **two levels up** |
| `cd /home/user` | Go to an **absolute path** |
| `cd ~` or just `cd` | Go to your **home directory** |
| `cd -` | Go to your **previous working directory** |

---

### **🔍 Tip:**

* Use `pwd` to confirm where you are.

* Use `ls` to list what’s in the current directory.

---

---

### **🔐 `chmod` – Change Mode**

* **Full form:** `chmod` stands for **"change mode"**

* **Purpose:** Modifies **file/directory permissions** in Linux/Unix systems

* **Permissions apply to:**

  * `u` → user (owner)

  * `g` → group

  * `o` → others

  * `a` → all (`u`, `g`, `o`)

---

### **🔤 Symbolic Mode Examples:**

| Command | Meaning |
| ----- | ----- |
| `chmod +x file` | Adds **execute** permission to **user, group, and others** (same as `a+x`) |
| `chmod =x file` | Sets permission to **only execute** for **all** (`ugo`), removes read/write |
| `chmod u+x file` | Adds **execute** permission to **user (owner)** only |
| `chmod g+r file` | Adds **read** permission to **group** only |

---

### **🔢 Numeric (Octal) Mode:**

Each permission is represented by a **3-digit number**:

* `r = 4`, `w = 2`, `x = 1`

* Format: `USER GROUP OTHERS`

| Command | Meaning |
| ----- | ----- |
| `chmod 100 file` | Gives **execute** to user, no permissions for group/others (`--x------`) |
| `chmod +100 file` | Adds **execute** permission to **user (owner)** only |

---

### **💡 Notes:**

* `chmod +x` → shorthand for `chmod a+x`

* `chmod =x` → removes all permissions except execute

* Numeric mode is strict: `chmod 755 file` → `rwxr-xr-x`

---

---

### **📂 `ls -ltr` – List Files in Detail, Sorted by Time**

* **Full form:** `ls` stands for **"list directory contents"**

* **Purpose:** Displays files/directories with details, sorted by **modification time (oldest first)**

---

### **🔤 Flag Breakdown:**

| Flag | Meaning |
| ----- | ----- |
| `-l` | Long listing format — shows file permissions, owner, size, time, name |
| `-t` | Sort by **modification time** (most recent first by default) |
| `-r` | Reverse the order — shows **oldest modified first** |

---

### **🧾 What `ls -ltr` Displays:**

\-rw-r--r--  1 user group  1234 Aug  2 12:34 example.txt

| Field | Description |
| ----- | ----- |
| `-rw-r--r--` | File permissions |
| `1` | Number of hard links |
| `user` | File owner |
| `group` | Group owner |
| `1234` | File size (in bytes) |
| `Aug 2 12:34` | Last modification date and time |
| `example.txt` | File name |

---

### **✅ Summary:**

`ls -ltr` lists files with **detailed info**, sorted by **modification time (oldest first)**.

---

---

### **📁 `ls -d */` – List All Directories in Current Folder**

#### **🔹 Purpose:**

* Lists only **directories**, **not files**

* `*/` is a **glob pattern** matching all names ending in `/` (i.e., directories)

---

### **✅ Usage:**

ls \-d \*/

| Part | Meaning |
| ----- | ----- |
| `ls` | List files and directories |
| `-d` | List the **name** of the directory, not its contents |
| `*/` | Match all **directories** in current path |

---

### **📌 Output:**

If you have:

file1.txt  dirA/  dirB/

Then:

ls \-d \*/

Returns:

dirA/  dirB/

---

### **🧠 Why use this?**

* You want a **clean list of just directories**

* Without `-d`, `ls */` would show the **contents inside** each directory

---

---

### **📌 `whatis` – One-Line Command Summary**

#### **🔹 Purpose:**

* Shows a **brief, one-line description** of a command

* It’s like a quick version of `man`

---

### **✅ Basic Syntax:**

whatis \[command\_name\]

#### **📌 Example:**

whatis ls

**Output:**

ls (1)               \- list directory contents

---

### **🔤 Breakdown of Output:**

| Field | Description |
| ----- | ----- |
| `ls` | Command name |
| `(1)` | Section of the manual (`man 1`) |
| Description | Short explanation of the command |

---

### **🧠 Use Cases:**

* Quickly check what a command does

* Confirm if a command exists

* See the relevant man section

---

### **🔧 Notes:**

* If it shows **nothing**, update the manual database:

sudo mandb

---

### **🔁 Related Commands:**

| Command | Purpose |
| ----- | ----- |
| `man ls` | Full manual page for `ls` |
| `whatis ls` | One-line summary |
| `man -f ls` | Same as `whatis ls` |
| `man -k list` | Search all man pages containing "list" |

---

---

### **📘 `man` – Manual Pages**

#### **🔹 Purpose:**

* Displays the **manual (help/documentation)** for a given Linux command

* Great for understanding **usage, flags, and options** of a command

---

### **✅ Basic Syntax:**

man \[command\_name\]

#### **📌 Example:**

man ls

→ Shows the manual page for the `ls` command

---

### **📚 Manual Sections:**

Linux manuals are divided into **sections**:

| Section | Contents |
| ----- | ----- |
| 1 | User commands (e.g., `ls`, `cd`) |
| 2 | System calls |
| 3 | Library functions |
| 4 | Device files |
| 5 | File formats |
| 6 | Games and screensavers |
| 7 | Miscellaneous |
| 8 | System administration commands |

#### **Example:**

man 5 crontab

→ Opens section 5 (file format) of `crontab`

---

### **🔸 Controls While Reading:**

| Key | Action |
| ----- | ----- |
| `Up/Down` | Scroll line by line |
| `Space` | Next page |
| `q` | Quit manual |
| `/text` | Search for "text" in the man page |
| `n` | Go to next search match |

---

### **🧠 Tip:**

If unsure what a command does, try:

man \<command\>

To find where a command is documented (all sections):

man \-f printf     \# same as \`whatis printf\`  
man \-k network    \# search all man pages with "network" keyword

---

---

### **📌 `touch` – Update File Timestamps or Create Empty Files**

#### **🔹 Purpose:**

* Creates **empty files** if they don’t exist

* Updates the **access and modification time** of existing files

---

### **✅ Basic Syntax:**

touch filename

* Creates the file `filename` if it doesn’t exist

* If it exists, updates its **modified** and **access** time to the current time

---

### **🧪 Example:**

touch test.txt

* Creates `test.txt` if missing

* Updates timestamp if it already exists

---

### **📘 `$ whatis touch` Output:**

touch (1)           \- change file timestamps

| Part | Explanation |
| ----- | ----- |
| `touch (1)` | Section 1 of the manual — user command |
| Description | Short explanation: modifies file times |

🔸 Unlike `mkdir`, there is **no `touch (2)`** because `touch` is not a system call — it uses underlying system calls like `utime()` or `open()` internally.

---

### **📚 Manual Page:**

View the full man page:

man touch

---

### **🧠 Common Use Cases:**

| Command | Description |
| ----- | ----- |
| `touch file.txt` | Create or update `file.txt` |
| `touch file1 file2` | Create/update multiple files |
| `touch -t 202508021530 file.txt` | Set custom timestamp (YYYYMMDDhhmm) |

---

---

# **📝 Vim – Vi IMproved (Linux Text Editor)**

---

## **📌 What is Vim?**

* **`vim`** stands for **Vi IMproved**

* An enhanced version of the classic `vi` text editor

* Used to **create and edit text/code files** in the terminal

* Popular among programmers for its **speed**, **power**, and **customizability**

---

## **✅ How to Install Vim**

### **🔸 Ubuntu/Debian:**

sudo apt update  
sudo apt install vim

---

## **🖥️ How to Use**

vim filename

* Opens `filename` for editing

* Creates the file if it doesn’t exist

---

## **🔤 `$ whatis vim`**

vim (1) – Vi IMproved, a programmers text editor

---

## **🎮 Modes in Vim**

| Mode | Purpose | Enter Mode With |
| ----- | ----- | ----- |
| Normal | Navigate & run commands | `Esc` |
| Insert | Insert text | `i`, `a`, `o` |
| Visual | Select and manipulate text | `v`, `V`, `Ctrl + v` |
| Command-line | Save, quit, search, etc. | `:` (in normal mode) |

---

## **🧠 Essential Vim Commands**

| Task | Command |
| ----- | ----- |
| Enter insert mode | `i` |
| Save file | `:w` |
| Quit Vim | `:q` |
| Save and quit | `:wq` or `ZZ` |
| Quit without saving | `:q!` |
| Delete current line | `dd` |
| Undo | `u` |
| Redo | `Ctrl + r` |
| Search for text | `/text` |
| Move to next match | `n` |
| Move to previous match | `N` |
| Copy (yank) line | `yy` |
| Paste | `p` |
| Cut (delete) word Enable syntax highlighting (if disabled) | `dw :syntax on`  |

---

## **⚙️ Configuration File**

* **User config:** `~/.vimrc`

Can be used to set things like:

 set number          " Show line numbers  
syntax on           " Enable syntax highlighting  
set tabstop=4       " Set tab width to 4  
---

## **📘 vi vs vim (Quick Comparison)**

| Feature | `vi` | `vim` (Vi IMproved) |
| ----- | ----- | ----- |
| Syntax Highlighting | ❌ No | ✅ Yes |
| Undo levels | Single | Multiple |
| Plugin support | ❌ No | ✅ Yes |
| Help system | Minimal | Full `:help` command |
| User customization | Limited | Rich `.vimrc` config file |

---

---

# **📝 Nano – Simple Terminal Text Editor**

---

## **📌 What is `nano`?**

* `nano` is a **beginner-friendly**, **easy-to-use** text editor for the terminal.

* It works in **modeless** style: you can **type, edit, and save** without switching modes (unlike Vim).

* Great for **quick edits**, config files, or for those new to Linux.

---

## **📘 `$ whatis nano`**

nano (1) – simple text editor

---

## **✅ How to Use**

nano filename

* Opens `filename` in `nano`

* Creates the file if it doesn’t exist

---

## **⌨️ Basic nano Shortcuts (at the bottom of the screen)**

| Task | Shortcut |
| ----- | ----- |
| Save (write) file | `Ctrl + O` then Enter |
| Exit | `Ctrl + X` |
| Cut line | `Ctrl + K` |
| Paste line | `Ctrl + U` |
| Copy line | `Alt + 6` |
| Undo | `Alt + U` |
| Redo | `Alt + E` |
| Search text | `Ctrl + W` |
| Go to line number | `Ctrl + _` then enter number |
| Show help | `Ctrl + G` |

---

## **⚙️ Configuration**

* User config file: `~/.nanorc`

Example settings:

 set linenumbers  
set softwrap  
set tabsize 4

* 

---

# **🔁 Nano vs. Vim – Key Differences**

| Feature | `nano` | `vim` (Vi IMproved) |
| ----- | ----- | ----- |
| Ease of Use | ✅ Very beginner-friendly | ❌ Steep learning curve (initially) |
| Modes | ❌ None (modeless) | ✅ Yes (normal, insert, visual) |
| Commands | On-screen shortcuts | Keyboard commands (in modes) |
| Syntax Highlighting | Limited | ✅ Advanced |
| Undo/Redo | Basic (`Alt + U` / `Alt + E`) | ✅ Powerful (`u`, `Ctrl + r`) |
| Customization | Minimal (`.nanorc`) | Extensive (`.vimrc`) |
| Speed & Power | Good for simple tasks | ✅ Excellent for programming |
| Plugin Support | ❌ None | ✅ Yes (with plugin managers) |
| Best for | Quick edits, config files | Complex coding, scripting |

---

### **🧠 When to Use What?**

* **Use `nano`** if you're editing config files, logs, or doing a quick change and want a no-hassle interface.

* **Use `vim`** if you're coding, doing power-user work, or need powerful editing features like macros, search-replace, etc.

---

---

## **🐱 `cat` – Concatenate and Display File Content**

### **✅ Purpose:**

* View file content

* Combine multiple files

* Create new files (in simple cases)

### **🔹 Basic Syntax:**

cat filename

### **🔹 Common Uses:**

| Task | Command |
| ----- | ----- |
| View file content | `cat file.txt` |
| View multiple files | `cat file1.txt file2.txt` |
| Create a new file (quickly) | `cat > new.txt` (then type, Ctrl+D to save) |
| Append file content | `cat file1 >> file2` |

---

## **🗑️ `rm` – Remove/Delete Files and Directories**

### **✅ Purpose:**

* Permanently deletes files or directories

### **🔹 Basic Syntax:**

rm filename

### **🔹 Common Uses:**

| Task | Command |
| ----- | ----- |
| Delete a file | `rm file.txt` |
| Delete multiple files | `rm file1.txt file2.txt` |
| Force delete (no prompt) | `rm -f file.txt` |
| Delete an empty directory | `rmdir mydir` |
| Delete directory \+ contents | `rm -r mydir/` |
| Force delete directory | `rm -rf mydir/` |

⚠️ **Warning**: `rm` permanently deletes — use carefully, especially with `-rf`

---

---

## **🔹 What is `#!` (Shebang)?**

* The **first line** of a script: `#! interpreter_path`

* Tells the OS **which shell** (or interpreter) to use to execute the script

Example:

 \#\!/bin/bash

* 

---

## **🔍 Shebang Variants and Their Purpose**

| Shebang Line | Uses Which Shell | Path Points To | Shell Type |
| ----- | ----- | ----- | ----- |
| `#!/bin/bash` | **Bash (Bourne Again Shell)** | `/bin/bash` | Full-featured shell (most common on Linux) |
| `#!/bin/dash` | **Dash (Debian Almquist Shell)** | `/bin/dash` | Lightweight, POSIX-compliant, fast |
| `#!/bin/ksh` | **Korn Shell (ksh)** | `/bin/ksh` | Advanced shell, scripting friendly |
| `#!/bin/sh` | **POSIX shell (linked)** | Often linked to `bash` or `dash` | Legacy-compatible (portable) |

---

## **🔁 Linkage Between Them (Linux Example):**

### **On most modern Debian/Ubuntu systems:**

* `/bin/sh` → **symbolic link to `/bin/dash`** (for performance)

* `/bin/bash` → standalone full Bash shell

* `/bin/dash` → minimalist POSIX-compliant shell

* `/bin/ksh` → may need to be installed separately

🔧 You can check this with:

ls \-l /bin/sh

---

## **⚙️ Differences in Behavior**

| Feature | `/bin/bash` | `/bin/sh` (dash) | `/bin/dash` | `/bin/ksh` |
| ----- | ----- | ----- | ----- | ----- |
| Speed | Moderate | ✅ Fast | ✅ Fast | Fast |
| Bash-only features | ✅ Yes | ❌ No | ❌ No | ❌ No |
| POSIX-compliant | Mostly | ✅ Yes | ✅ Yes | ✅ Yes |
| Arrays, `[[ ]]`, etc. | ✅ Yes | ❌ No | ❌ No | Partial/Yes |
| Script portability | ❌ Low | ✅ High | ✅ High | ✅ High |

---

## **🧠 When to Use Which:**

| Use Case | Recommended Shebang |
| ----- | ----- |
| Advanced scripting (arrays, regex) | `#!/bin/bash` |
| Fast, POSIX-compliant init scripts | `#!/bin/dash` or `#!/bin/sh` |
| Legacy or system-wide compatibility | `#!/bin/sh` |
| Older systems or ksh-specific features | `#!/bin/ksh` |

---

---

## **🕘 `history` – Show Command History**

### **✅ Purpose:**

* Displays a list of previously executed shell commands in the terminal

* Helps you recall or reuse past commands

---

## **🔹 Basic Usage:**

history

* Lists all past commands with line numbers (most recent at the bottom)

---

## **🔧 Common Variations:**

| Command | Description |
| ----- | ----- |
| `history` | Show entire command history |
| `history 10` | Show last 10 commands |
| `!n` | Run command number `n` from history |
| `!-1` | Run the **last** command again |
| `!!` | Shortcut for `!-1` (repeat last command) |
| `!string` | Run **most recent** command starting with `string` |
| `!sudo` | Run the last command that started with `sudo` |
| `history -c` | ❗ Clear the history (in current session) |
| `history -w` | Write current history to `~/.bash_history` |

---

## **📁 Where Is History Stored?**

Bash stores history in:

 \~/.bash\_history

*   
* You can view or edit it with `cat`, `nano`, or `vim`

---

## **🔁 Useful Shortcuts:**

| Shortcut | Action |
| ----- | ----- |
| `Ctrl + r` | Reverse search through history, To **search and reuse** past commands interactively: (Ctrl \+ r) Then type part of the command  — it finds matches instantly\! |
| `↑ / ↓` | Navigate through history one by one |
| `!!` | Repeat previous command |

---

---

## **🧼 `clear` – Clear Terminal Screen**

### **✅ Purpose:**

* Clears all previous output from the terminal window

### **🔹 Usage:**

clear

* Just type and hit Enter — screen looks fresh, but command history is still accessible (via `↑` arrow or `Ctrl + r`).

---

## **📍 `pwd` – Print Working Directory**

### **✅ Purpose:**

* Shows the **current directory** you’re in

### **🔹 Usage:**

pwd

Output will be something like:

 /home/username/projects

---

---

## **🧠 System Monitoring Commands**

---

### **📦 `free` – Show Memory Usage**

free

* Displays RAM & swap usage in bytes

* Columns: total, used, free, shared, buff/cache, available

---

### **📦 `free -m`, `free -g`**

free \-m    \# in megabytes    
free \-g    \# in gigabytes  

---

### **🧮 `nproc` – Number of Processing Units**

nproc

* Shows the number of **logical CPU cores** available

* Example output: `8`

* Useful for parallel tasks or compilation optimization (e.g., `make -j$(nproc)`)

---

### **💾 `df -h` – Disk Free (Human-readable)**

df \-h

* Displays available and used disk space **per mounted filesystem**

* `-h` \= human-readable (MB/GB)

* Columns: Filesystem, Size, Used, Avail, Use%, Mounted on

---

### **📊 `top` – Real-time System Monitor**

top

* Shows live summary of CPU, memory usage, running processes

* Default columns:

  * PID, USER, %CPU, %MEM, TIME+, COMMAND

* Press `q` to quit

* Press `M` (uppercase) to sort by memory usage

* Press `P` to sort by CPU usage

---

## **⚡ Summary Table**

| Command | Purpose | Common Flag | Output Units |
| ----- | ----- | ----- | ----- |
| `free` | Memory usage | `-m`, `-g` | MB/GB |
| `nproc` | Number of CPU cores | None | Integer |
| `df` | Disk usage per filesystem | `-h` | MB/GB |
| `top` | Live process & system monitoring | (interactive) | Real-time display |

---

### **🐛 `set -x` – Debug Bash Scripts (Print Commands Before Execution)**

---

## **✅ Purpose:**

* Enables **debugging mode** in Bash

* Prints each command **and its arguments** to the terminal **before it executes**

---

## **🧪 Usage:**

set \-x  
\# your commands  
set \+x

* `set -x` → turns **on** command tracing

* `set +x` → turns **off** command tracing

---

## **🔍 Example:**

\#\!/bin/bash  
set \-x  
a=5  
b=10  
c=$((a \+ b))  
echo "Sum is $c"  
set \+x

**Output:**

\+ a=5  
\+ b=10  
\+ c=15  
\+ echo 'Sum is 15'  
Sum is 15

---

## **🧠 Why Use It?**

* Helps debug **complex scripts** by showing step-by-step execution

* Especially useful inside `if`, `for`, or `while` blocks

* Works in both interactive shell and scripts

---

---

### **🧠 `ps -ef` — View All Running Processes**

The `ps` command is used to **display information about active processes** on the system.

---

### **✅ Command:**

ps \-ef

### **🔹 Breakdown:**

* `-e` → Show **all processes** (not just those owned by current user)

* `-f` → **Full-format listing** (more detailed info)

---

### **📋 Output Columns:**

| Column | Meaning |
| ----- | ----- |
| UID | User who owns the process |
| PID | Process ID |
| PPID | Parent Process ID |
| C | CPU utilization |
| STIME | Start time of the process |
| TTY | Terminal associated (if any) |
| TIME | Total CPU time the process has used |
| CMD | Command that started the process |

---

### **🛠 Example:**

ps \-ef | grep firefox

Finds all running `firefox` processes.

---

---

## **🔗 `|` Pipe Command in Linux**

### **✅ Purpose:**

The **pipe (`|`)** is used to **connect two commands**, sending the **output of the first command** as the **input to the second**.

---

### **🧠 Syntax:**

command1 | command2

* Think of it as: “Take the result of command1 and **pipe** it into command2.”

---

### **📋 Real Examples & Explanations:**

### **1\. `ls -l | less`**

🔹 **Lists files in long format and scrolls the output.**

* `ls -l` → Lists files with permissions, size, owner, date, etc.

* `less` → Opens output in a scrollable viewer (up/down with arrow keys).

✅ Useful when there are **many files** and the output overflows the terminal.

---

### **2\. `ps -ef | grep bash`**

🔹 **Searches for running `bash` processes.**

* `ps -ef` → Shows **all processes** with full details.

* `grep bash` → Filters lines that contain “bash”.

✅ Helps you find if `bash` (or any other process) is currently running.

---

### **3\. `cat file.txt | wc -l`**

🔹 **Counts how many lines are in `file.txt`.**

* `cat file.txt` → Outputs the content of the file.

* `wc -l` → Counts the number of lines.

✅ A cleaner and more readable way than using `wc -l file.txt`.

---

### **4\. `dmesg | tail`**

🔹 **Shows the last few kernel/system log messages.**

* `dmesg` → Displays kernel ring buffer messages (boot, hardware, drivers).

* `tail` → Shows only the **last 10 lines** by default.

✅ Useful for debugging **hardware or boot issues**.

---

### **5\. `find . -type f | wc -l`**

🔹 **Counts all regular files in the current directory and subdirectories.**

* `find . -type f` → Finds all files (not directories) starting from `.` (current dir).

* `wc -l` → Counts the number of lines in the output \= number of files.

✅ Helps quickly find how many files exist recursively.

---

### **🧰 Common Use Cases:**

* **Filtering**: e.g., `grep`, `awk`, `cut`

* **Pagination**: e.g., `less`, `more`

* **Counting**: e.g., `wc`

* **Sorting**: e.g., `sort`, `uniq`

* **Chaining logic**: combine multiple steps without temporary files

---

### **💡 Tips:**

* Pipes only work with **stdout to stdin** (standard output/input).

You can **chain multiple pipes**:

 cat file.txt | grep "error" | sort | uniq \-c

---

---

## **🔁 “*date | echo”* command**

A **pipe (`|`)** connects the **output of one command (stdout)** to the **input of another command (stdin)**.

For example:

ls | less

* `ls` sends its output to the pipe

* `less` reads that output from the pipe and displays it interactively

This works because `less` reads from **standard input** (stdin).

---

## **🔤 What does `echo` do?**

echo something

* `echo` simply prints whatever **arguments** you pass to it.

* It **does not read** from standard input (stdin).

* It **does not care** what is coming through the pipe.

So when you run:

date | echo

### **Here's what happens internally:**

1. `date` → produces something like `Sat Aug 2 16:32:58 +06 2025`

2. That output is sent into the pipe `|`

3. **`echo` ignores it — because `echo` doesn't read from stdin**

So the result is just:

 (an empty line)

4. 

⚠️ The output of `date` is effectively **discarded**.

---

## **✅ So what should you use instead?**

### **✅ If you want to use the output of `date`, use:**

#### **1\. `cat` (which reads from stdin):**

date | cat

✔ This will output the current date using the pipe.

#### **2\. Store it in a variable:**

d=$(date)

echo "Current date is: $d"

---

## **🧠 Summary Table:**

| Command | Reads from stdin? | Works with pipes as input? |
| ----- | ----- | ----- |
| `echo` | ❌ No | ❌ No effect from pipe input |
| `cat` | ✅ Yes | ✅ Yes |
| `less` | ✅ Yes | ✅ Yes |
| `grep` | ✅ Yes | ✅ Yes |
| `awk`, `sort` | ✅ Yes | ✅ Yes |

---

---

