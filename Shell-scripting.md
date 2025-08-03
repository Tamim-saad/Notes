### **🔐** `chmod` **– Change Mode**

- **Full form:** `chmod` stands for **"change mode"**

- **Purpose:** Modifies **file/directory permissions** in Linux/Unix systems

- **Permissions apply to:**

  - `u` → user (owner)

  - `g` → group

  - `o` → others

  - `a` → all (`u`, `g`, `o`)

***


### **🔤 Symbolic Mode Examples:**

|                  |                                                                             |
| :--------------: | :-------------------------------------------------------------------------: |
|    **Command**   |                                 **Meaning**                                 |
|  `chmod +x file` |  Adds **execute** permission to **user, group, and others** (same as `a+x`) |
|  `chmod =x file` | Sets permission to **only execute** for **all** (`ugo`), removes read/write |
| `chmod u+x file` |             Adds **execute** permission to **user (owner)** only            |
| `chmod g+r file` |                  Adds **read** permission to **group** only                 |

***


### **🔢 Numeric (Octal) Mode:**

Each permission is represented by a **3-digit number**:

- `r = 4`, `w = 2`, `x = 1

  `

- Format: `USER GROUP OTHERS

  `

|                   |                                                                          |
| :---------------: | :----------------------------------------------------------------------: |
|    **Command**    |                                **Meaning**                               |
|  `chmod 100 file` | Gives **execute** to user, no permissions for group/others (`--x------`) |
| `chmod +100 file` |           Adds **execute** permission to **user (owner)** only           |

***


### **💡 Notes:**

- `chmod +x` → shorthand for `chmod a+x

  `

- `chmod =x` → removes all permissions except execute

- Numeric mode is strict: `chmod 755 file` → `rwxr-xr-x

  `

***

***


### **📂** `ls -ltr` **– List Files in Detail, Sorted by Time**

- **Full form:** `ls` stands for **"list directory contents"**

- **Purpose:** Displays files/directories with details, sorted by **modification time (oldest first)**

***


### **🔤 Flag Breakdown:**

|          |                                                                       |
| :------: | :-------------------------------------------------------------------: |
| **Flag** |                              **Meaning**                              |
|   `-l`   | Long listing format — shows file permissions, owner, size, time, name |
|   `-t`   |      Sort by **modification time** (most recent first by default)     |
|   `-r`   |          Reverse the order — shows **oldest modified first**          |

***


### **🧾 What** `ls -ltr` **Displays:**

-rw-r--r--  1 user group  1234 Aug  2 12:34 example.txt

|               |                                 |
| :-----------: | :-----------------------------: |
|   **Field**   |         **Description**         |
|  `-rw-r--r--` |         File permissions        |
|      `1`      |       Number of hard links      |
|     `user`    |            File owner           |
|    `group`    |           Group owner           |
|     `1234`    |       File size (in bytes)      |
| `Aug 2 12:34` | Last modification date and time |
| `example.txt` |            File name            |

***


### **✅ Summary:**

`ls -ltr` lists files with **detailed info**, sorted by **modification time (oldest first)**.

***

***


### **📁** `ls -d */` **– List All Directories in Current Folder**

#### **🔹 Purpose:**

- Lists only **directories**, **not files**

- `*/` is a **glob pattern** matching all names ending in `/` (i.e., directories)

***


### **✅ Usage:**

ls -d \*/

|          |                                                      |
| :------: | :--------------------------------------------------: |
| **Part** |                      **Meaning**                     |
|   `ls`   |              List files and directories              |
|   `-d`   | List the **name** of the directory, not its contents |
|   `*/`   |       Match all **directories** in current path      |

***


### **📌 Output:**

If you have:

file1.txt  dirA/  dirB/

Then:

ls -d \*/

Returns:

dirA/  dirB/

***


### **🧠 Why use this?**

- You want a **clean list of just directories**

- Without `-d`, `ls */` would show the **contents inside** each directory

***

***


### **📌** `whatis` **– One-Line Command Summary**

#### **🔹 Purpose:**

- Shows a **brief, one-line description** of a command

- It’s like a quick version of `man

  `

***


### **✅ Basic Syntax:**

whatis \[command\_name]


#### **📌 Example:**

whatis ls

**Output:**

ls (1)               - list directory contents

***


### **🔤 Breakdown of Output:**

|             |                                  |
| :---------: | :------------------------------: |
|  **Field**  |          **Description**         |
|     `ls`    |           Command name           |
|    `(1)`    |  Section of the manual (`man 1`) |
| Description | Short explanation of the command |

***


### **🧠 Use Cases:**

- Quickly check what a command does

- Confirm if a command exists

- See the relevant man section

***


### **🔧 Notes:**

- If it shows **nothing**, update the manual database:

sudo mandb

***


### **🔁 Related Commands:**

|               |                                        |
| :-----------: | :------------------------------------: |
|  **Command**  |               **Purpose**              |
|    `man ls`   |        Full manual page for `ls`       |
|  `whatis ls`  |            One-line summary            |
|  `man -f ls`  |           Same as `whatis ls`          |
| `man -k list` | Search all man pages containing "list" |

***

***


### **📘** `man` **– Manual Pages**

#### **🔹 Purpose:**

- Displays the **manual (help/documentation)** for a given Linux command

- Great for understanding **usage, flags, and options** of a command

***


### **✅ Basic Syntax:**

man \[command\_name]


#### **📌 Example:**

man ls

→ Shows the manual page for the `ls` command

***


### **📚 Manual Sections:**

Linux manuals are divided into **sections**:

|             |                                  |
| :---------: | :------------------------------: |
| **Section** |           **Contents**           |
|      1      | User commands (e.g., `ls`, `cd`) |
|      2      |           System calls           |
|      3      |         Library functions        |
|      4      |           Device files           |
|      5      |           File formats           |
|      6      |      Games and screensavers      |
|      7      |           Miscellaneous          |
|      8      |  System administration commands  |


#### **Example:**

man 5 crontab

→ Opens section 5 (file format) of `crontab`

***


### **🔸 Controls While Reading:**

|           |                                   |
| :-------: | :-------------------------------: |
|  **Key**  |             **Action**            |
| `Up/Down` |        Scroll line by line        |
|  `Space`  |             Next page             |
|    `q`    |            Quit manual            |
|  `/text`  | Search for "text" in the man page |
|    `n`    |      Go to next search match      |

***


### **🧠 Tip:**

If unsure what a command does, try:

man \<command>

To find where a command is documented (all sections):

man -f printf     # same as \`whatis printf\`

man -k network    # search all man pages with "network" keyword

***

***


### **📌** `touch` **– Update File Timestamps or Create Empty Files**

#### **🔹 Purpose:**

- Creates **empty files** if they don’t exist

- Updates the **access and modification time** of existing files

***


### **✅ Basic Syntax:**

touch filename

- Creates the file `filename` if it doesn’t exist

- If it exists, updates its **modified** and **access** time to the current time

***


### **🧪 Example:**

touch test.txt

- Creates `test.txt` if missing

- Updates timestamp if it already exists

***


### **📘** `$ whatis touch` **Output:**

touch (1)           - change file timestamps

|             |                                        |
| :---------: | :------------------------------------: |
|   **Part**  |             **Explanation**            |
| `touch (1)` | Section 1 of the manual — user command |
| Description | Short explanation: modifies file times |

🔸 Unlike `mkdir`, there is **no** `touch (2)` because `touch` is not a system call — it uses underlying system calls like `utime()` or `open()` internally.

***


### **📚 Manual Page:**

View the full man page:

man touch

***


### **🧠 Common Use Cases:**

|                                  |                                     |
| :------------------------------: | :---------------------------------: |
|            **Command**           |           **Description**           |
|         `touch file.txt`         |     Create or update `file.txt`     |
|        `touch file1 file2`       |     Create/update multiple files    |
| `touch -t 202508021530 file.txt` | Set custom timestamp (YYYYMMDDhhmm) |

***

***


# **📝 Vim – Vi IMproved (Linux Text Editor)**

***


## **📌 What is Vim?**

- `vim` stands for **Vi IMproved**

- An enhanced version of the classic `vi` text editor

- Used to **create and edit text/code files** in the terminal

- Popular among programmers for its **speed**, **power**, and **customizability**

***


## **✅ How to Install Vim**

### **🔸 Ubuntu/Debian:**

sudo apt update

sudo apt install vim

***


## **🖥️ How to Use**

vim filename

- Opens `filename` for editing

- Creates the file if it doesn’t exist

***


## **🔤** `$ whatis vim`

vim (1) – Vi IMproved, a programmers text editor

***


## **🎮 Modes in Vim**

|              |                            |                      |
| :----------: | :------------------------: | :------------------: |
|   **Mode**   |         **Purpose**        |  **Enter Mode With** |
|    Normal    |   Navigate & run commands  |         `Esc`        |
|    Insert    |         Insert text        |     `i`, `a`, `o`    |
|    Visual    | Select and manipulate text | `v`, `V`, `Ctrl + v` |
| Command-line |  Save, quit, search, etc.  | `:` (in normal mode) |

***


## **🧠 Essential Vim Commands**

|                                                           |                   |
| :-------------------------------------------------------: | :---------------: |
|                          **Task**                         |    **Command**    |
|                     Enter insert mode                     |        `i`        |
|                         Save file                         |        `:w`       |
|                          Quit Vim                         |        `:q`       |
|                       Save and quit                       |   `:wq` or `ZZ`   |
|                    Quit without saving                    |       `:q!`       |
|                    Delete current line                    |        `dd`       |
|                            Undo                           |        `u`        |
|                            Redo                           |     `Ctrl + r`    |
|                      Search for text                      |      `/text`      |
|                     Move to next match                    |        `n`        |
|                   Move to previous match                  |        `N`        |
|                      Copy (yank) line                     |        `yy`       |
|                           Paste                           |        `p`        |
| Cut (delete) wordEnable syntax highlighting (if disabled) | `dw``:syntax on`  |

***


## **⚙️ Configuration File**

- **User config:** `~/.vimrc

  `

Can be used to set things like:\
\
&#x20;set number          " Show line numbers

syntax on           " Enable syntax highlighting

set tabstop=4       " Set tab width to 4

***


## **📘 vi vs vim (Quick Comparison)**

|                     |         |                           |
| :-----------------: | :-----: | :-----------------------: |
|     **Feature**     |   `vi`  |  `vim` **(Vi IMproved)**  |
| Syntax Highlighting |   ❌ No  |           ✅ Yes           |
|     Undo levels     |  Single |          Multiple         |
|    Plugin support   |   ❌ No  |           ✅ Yes           |
|     Help system     | Minimal |    Full `:help` command   |
|  User customization | Limited | Rich `.vimrc` config file |

***

***


# **📝 Nano – Simple Terminal Text Editor**

***


## **📌 What is** `nano`**?**

- `nano` is a **beginner-friendly**, **easy-to-use** text editor for the terminal.

- It works in **modeless** style: you can **type, edit, and save** without switching modes (unlike Vim).

- Great for **quick edits**, config files, or for those new to Linux.

***


## **📘** `$ whatis nano`

nano (1) – simple text editor

***


## **✅ How to Use**

nano filename

- Opens `filename` in `nano

  `

- Creates the file if it doesn’t exist

***


## **⌨️ Basic nano Shortcuts (at the bottom of the screen)**

|                   |                              |
| :---------------: | :--------------------------: |
|      **Task**     |         **Shortcut**         |
| Save (write) file |     `Ctrl + O` then Enter    |
|        Exit       |          `Ctrl + X`          |
|      Cut line     |          `Ctrl + K`          |
|     Paste line    |          `Ctrl + U`          |
|     Copy line     |           `Alt + 6`          |
|        Undo       |           `Alt + U`          |
|        Redo       |           `Alt + E`          |
|    Search text    |          `Ctrl + W`          |
| Go to line number | `Ctrl + _` then enter number |
|     Show help     |          `Ctrl + G`          |

***


## **⚙️ Configuration**

- User config file: `~/.nanorc

  `

Example settings:\
\
&#x20;set linenumbers

set softwrap

set tabsize 4

-

***


# **🔁 Nano vs. Vim – Key Differences**

|                     |                               |                                    |
| :-----------------: | :---------------------------: | :--------------------------------: |
|     **Feature**     |             `nano`            |       `vim` **(Vi IMproved)**      |
|     Ease of Use     |    ✅ Very beginner-friendly   | ❌ Steep learning curve (initially) |
|        Modes        |       ❌ None (modeless)       |   ✅ Yes (normal, insert, visual)   |
|       Commands      |      On-screen shortcuts      |    Keyboard commands (in modes)    |
| Syntax Highlighting |            Limited            |             ✅ Advanced             |
|      Undo/Redo      | Basic (`Alt + U` / `Alt + E`) |    ✅ Powerful (`u`, `Ctrl + r`)    |
|    Customization    |      Minimal (`.nanorc`)      |        Extensive (`.vimrc`)        |
|    Speed & Power    |     Good for simple tasks     |     ✅ Excellent for programming    |
|    Plugin Support   |             ❌ None            |    ✅ Yes (with plugin managers)    |
|       Best for      |   Quick edits, config files   |      Complex coding, scripting     |

***


### **🧠 When to Use What?**

- **Use** `nano` if you're editing config files, logs, or doing a quick change and want a no-hassle interface.

- **Use** `vim` if you're coding, doing power-user work, or need powerful editing features like macros, search-replace, etc.

***

***


## **🐱** `cat` **– Concatenate and Display File Content**

### **✅ Purpose:**

- View file content

- Combine multiple files

- Create new files (in simple cases)


### **🔹 Basic Syntax:**

cat filename


### **🔹 Common Uses:**

|                             |                                             |
| :-------------------------: | :-----------------------------------------: |
|           **Task**          |                 **Command**                 |
|      View file content      |                `cat file.txt`               |
|     View multiple files     |          `cat file1.txt file2.txt`          |
| Create a new file (quickly) | `cat > new.txt` (then type, Ctrl+D to save) |
|     Append file content     |             `cat file1 >> file2`            |

***


## **🗑️** `rm` **– Remove/Delete Files and Directories**

### **✅ Purpose:**

- Permanently deletes files or directories


### **🔹 Basic Syntax:**

rm filename


### **🔹 Common Uses:**

|                             |                          |
| :-------------------------: | :----------------------: |
|           **Task**          |        **Command**       |
|        Delete a file        |       `rm file.txt`      |
|    Delete multiple files    | `rm file1.txt file2.txt` |
|   Force delete (no prompt)  |     `rm -f file.txt`     |
|  Delete an empty directory  |       `rmdir mydir`      |
| Delete directory + contents |      `rm -r mydir/`      |
|    Force delete directory   |      `rm -rf mydir/`     |

⚠️ **Warning**: `rm` permanently deletes — use carefully, especially with `-rf`

***
