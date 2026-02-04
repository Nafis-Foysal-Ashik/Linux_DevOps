# Linux & DevOps Study Notes

This repository contains comprehensive study notes on Linux fundamentals, file management, system monitoring, and networking tools essential for DevOps. These notes cover architecture, permissions, user management, and advanced command-line tools.

## 1. Linux Core Concepts & Architecture

**Linux** is an open-source operating system where "everything is a file".
* [cite_start]**Architecture Layers**: Hardware → Kernel → Shell → Application [cite: 1, 13-15].
* **Kernel**: The core that communicates with hardware and manages resources. [cite_start]It is secure by design; normal apps cannot change system files directly[cite: 15, 11].
* [cite_start]**Shell**: The user interface (CLI) that interprets commands (like `mkdir`) and sends them to the kernel for execution[cite: 14, 21, 31].
* **Linux vs. Windows**: Linux is open-source (GPL) and file-based. [cite_start]Windows is commercial and uses drive letters[cite: 11].

---

## 2. File & Folder Management

### Navigation & Listing
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ls`** | [cite_start]Lists files and folders in the current directory[cite: 45]. | `ls` |
| **`ls -l`** | [cite_start]Lists files with detailed info (permissions, owner, size, time)[cite: 132]. | `ls -l` |
| **`ls -ltr`** | [cite_start]Lists details sorted by modification time in reverse order (oldest to newest)[cite: 135]. | `ls -ltr` |
| **`lsblk`** | [cite_start]Lists information about all available block devices (disk partitions)[cite: 609]. | `lsblk` |
| **`pwd`** | [cite_start]Prints the current working directory path[cite: 47]. | `pwd` |

### Creation & Deletion
| Command | Description | Example |
| :--- | :--- | :--- |
| **`touch`** | [cite_start]Creates a new empty file[cite: 50]. | `touch newfile.txt` |
| **`mkdir`** | [cite_start]Creates a new folder (directory)[cite: 32]. | `mkdir myfolder` |
| **`rm`** | [cite_start]Removes (deletes) a file[cite: 53]. | `rm filename.txt` |
| **`rmdir`** | [cite_start]Removes a folder (must be empty)[cite: 52]. | `rmdir myfolder` |
| **`rm -rf`** | [cite_start]Forcefully removes a directory and its contents (implied for non-empty folders)[cite: 250]. | `sudo rm -rf /home/user/dir` |

### Manipulation
| Command | Description | Example |
| :--- | :--- | :--- |
| **`cp`** | [cite_start]Copies a file or folder from source to destination[cite: 103]. | `cp source.txt destination.txt` |
| **`mv`** | [cite_start]Moves a file/folder to a new location or renames it[cite: 106]. | `mv oldname.txt newname.txt` |
| **`ln -s`** | Creates a "soft link" (shortcut). [cite_start]If the source is deleted, the link breaks[cite: 122]. | `ln -s /path/to/file linkname` |
| **`ln`** | Creates a "hard link". [cite_start]If the source is deleted, the file data remains accessible via the link[cite: 147]. | `ln /path/to/file linkname` |

---

## 3. File Content & Text Processing

### Viewing Content
| Command | Description | Example |
| :--- | :--- | :--- |
| **`cat`** | [cite_start]Displays the full content of a file[cite: 56]. | `cat filename.txt` |
| **`head`** | [cite_start]Displays the first few lines of a file[cite: 67]. | `head filename.txt` |
| **`tail`** | [cite_start]Displays the last few lines of a file[cite: 69]. | `tail filename.txt` |
| **`tail -f`** | [cite_start]Follows the end of a file in real-time (useful for monitoring logs)[cite: 70]. | `tail -f /var/log/syslog` |
| **`less`** | Views large file content page-by-page. (Use arrows to scroll, `q` to quit) [cite_start][cite: 75]. | `less largefile.txt` |
| **`more`** | [cite_start]Similar to `less`, views content one page at a time (Space for next page)[cite: 76]. | `more largefile.txt` |
| **`cal`** | [cite_start]Displays a calendar in the terminal[cite: 56]. | `cal` |
| **`zcat`** | [cite_start]Views the content of a compressed (zip) file without unzipping[cite: 61]. | `zcat archive.zip` |

### Editing & Writing
| Command | Description | Example |
| :--- | :--- | :--- |
| **`echo`** | [cite_start]Prints text to the terminal or writes to a file using redirection (`>`)[cite: 60]. | `echo "Hello World" > file.txt` |
| **`nano`** | Simple terminal text editor. [cite_start]Use `Ctrl+X` to exit[cite: 83]. | `nano file.txt` |
| **`vim`** | Advanced text editor. [cite_start]Press `i` to insert, `:wq` to save and quit[cite: 169]. | `vim file.txt` |
| **`tee`** | [cite_start]Reads from standard input and writes to both standard output and files[cite: 163]. | `echo "hello" | tee file.txt` |

### Advanced Processing (awk, sed, grep)
| Command | Description | Example |
| :--- | :--- | :--- |
| **`wc`** | [cite_start]Counts lines, words, and characters in a file[cite: 115]. | `wc filename.txt` |
| **`cut`** | [cite_start]Extracts specific sections (bytes/columns) from lines of files[cite: 156]. | `cut -b 1-4 filename` |
| **`sort`** | [cite_start]Sorts the contents of a text file alphabetically[cite: 168]. | `sort filename.txt` |
| **`grep`** | [cite_start]Searches for a specific pattern/word inside a file[cite: 592]. | `grep "INFO" logfile.txt` |
| **`grep -i`** | [cite_start]Search ignoring case (case-insensitive)[cite: 599]. | `grep -i "error" logfile.txt` |
| **`grep -c`** | [cite_start]Counts the occurrences of a pattern in a file[cite: 608]. | `grep -c "INFO" logfile.txt` |
| **`awk`** | [cite_start]Scans and processes files, useful for structured data (printing specific columns)[cite: 565]. | `awk '{print $1}' filename` |
| **`sed`** | [cite_start]Stream editor for filtering and transforming text (e.g., find and replace)[cite: 574]. | `sed 's/LOG/INFO/g' file.txt` |

---

## 4. User & Group Management

### User Actions
| Command | Description | Example |
| :--- | :--- | :--- |
| **`sudo`** | [cite_start]Executes a command with superuser (admin) privileges[cite: 216]. | `sudo apt update` |
| **`who`** | [cite_start]Shows who is currently logged into the system[cite: 211]. | `who` |
| **`whoami`** | [cite_start]Displays the current effective username[cite: 212]. | `whoami` |
| **`su`** | [cite_start]Switches to another user account[cite: 239]. | `su username` |
| **`useradd`** | [cite_start]Creates a new user[cite: 234]. | `sudo useradd -m newuser` |
| **`passwd`** | [cite_start]Sets or changes a user's password[cite: 237]. | `sudo passwd newuser` |
| **`userdel`** | [cite_start]Deletes a user account[cite: 246]. | `sudo userdel newuser` |
| **`cat /etc/passwd`**| [cite_start]Lists all users defined on the system[cite: 255]. | `cat /etc/passwd` |

### Group Actions
| Command | Description | Example |
| :--- | :--- | :--- |
| **`groupadd`** | [cite_start]Creates a new group[cite: 264]. | `sudo groupadd devops` |
| **`groupdel`** | [cite_start]Deletes an existing group[cite: 273]. | `sudo groupdel devops` |
| **`gpasswd -a`** | [cite_start]Adds a user to a group[cite: 259]. | `sudo gpasswd -a user group` |
| **`gpasswd -M`** | [cite_start]Adds multiple users to a group at once[cite: 265]. | `sudo gpasswd -M u1,u2 group` |
| **`cat /etc/group`** | [cite_start]Lists all groups defined on the system[cite: 258]. | `cat /etc/group` |
| **`getent group`** | [cite_start]Displays details of a specific group[cite: 276]. | `getent group sudo` |

---

## 5. Permissions & Ownership
[cite_start]Permissions are represented as Read (**r**=4), Write (**w**=2), Execute (**x**=1)[cite: 289].

| Command | Description | Example |
| :--- | :--- | :--- |
| **`chmod`** | [cite_start]Changes file permissions[cite: 304]. | `chmod 755 script.sh` |
| **`chmod 777`** | [cite_start]Gives full read, write, and execute permissions to everyone[cite: 309]. | `chmod 777 file.txt` |
| **`chmod +x`** | [cite_start]Adds execution permission for all users[cite: 311]. | `chmod +x script.sh` |
| **`chmod -x`** | [cite_start]Removes execution permission for all users[cite: 312]. | `chmod -x script.sh` |
| **`chmod -w`** | [cite_start]Removes write permission for "others"[cite: 317]. | `chmod o-w file.txt` |
| **`chown`** | [cite_start]Changes the owner of a file or folder[cite: 341]. | `sudo chown user file.txt` |
| **`chgrp`** | [cite_start]Changes the group ownership of a file[cite: 346]. | `sudo chgrp group file.txt` |
| **`umask`** | [cite_start]Sets default permissions for newly created files/folders[cite: 326]. | `umask 0022` |

---

## 6. System Monitoring & Resources

| Command | Description | Example |
| :--- | :--- | :--- |
| **`top`** | [cite_start]Displays real-time system performance, CPU, RAM, and processes[cite: 187]. | `top` |
| **`kill`** | [cite_start]Terminates a process (usually via PID)[cite: 188]. | `kill 1234` |
| **`df -h`** | [cite_start]Shows disk space usage in human-readable format[cite: 173]. | `df -h` |
| **`du`** | [cite_start]Shows disk usage (size) of files and folders[cite: 174]. | `du foldername` |
| **`du -sh`** | [cite_start]Shows summary of disk usage for a specific directory in human-readable form[cite: 183]. | `du -sh Downloads/` |
| **`free`** | [cite_start]Displays amount of free and used memory[cite: 193]. | `free` |
| **`free -h`** | [cite_start]Displays memory details in human-readable (GB/MB) format[cite: 202]. | `free -h` |
| **`vmstat`** | [cite_start]Reports virtual memory, swap, disk, and CPU activity[cite: 208]. | `vmstat 2` |
| **`nohup`** | [cite_start]Runs a command in the background that keeps running even if the terminal closes[cite: 199]. | `nohup command &` |
| **`shutdown`** | [cite_start]Shuts down the system[cite: 217]. | `sudo shutdown now` |
| **`reboot`** | [cite_start]Restarts the system[cite: 218]. | `sudo reboot` |

---

## 7. Networking Tools (DevOps Focused)

### Connectivity & Diagnostics
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ping`** | [cite_start]Checks network connectivity to a host[cite: 373]. | `ping google.com` |
| **`ping -i`** | [cite_start]Sets the time interval between pings[cite: 386]. | `ping -i 2 google.com` |
| **`ping -w`** | [cite_start]Sets a deadline (timeout) in seconds for the ping command[cite: 396]. | `ping -w 5 google.com` |
| **`telnet`** | [cite_start]Checks raw TCP connectivity to a specific port[cite: 470]. | `telnet google.com 80` |
| **`traceroute`** | [cite_start]Shows the path (hops) packets take to a destination[cite: 427]. | `traceroute google.com` |
| **`tracepath`** | [cite_start]Similar to traceroute, shows MTU (Max Transmission Unit)[cite: 443]. | `tracepath google.com` |
| **`mtr`** | [cite_start]Combines `ping` and `traceroute` for real-time diagnostics[cite: 447]. | `mtr google.com` |
| **`ifplugstatus`** | [cite_start]Checks if the network cable is plugged in[cite: 529]. | `ifplugstatus` |

### Network Information
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ip a`** | [cite_start]Displays all network interfaces and IP addresses[cite: 417]. | `ip a` |
| **`ip neigh`** | [cite_start]Shows the neighbor table (ARP cache)[cite: 519]. | `ip neigh` |
| **`ip route`** | [cite_start]Shows the routing table and gateway info[cite: 560]. | `ip route` |
| **`netstat`** | [cite_start]Shows network connections and listening ports[cite: 406]. | `netstat -tuln` |
| **`nmap`** | [cite_start]Scans a server for open ports and system details[cite: 550]. | `nmap -v facebook.com` |

### DNS & Web
| Command | Description | Example |
| :--- | :--- | :--- |
| **`nslookup`** | [cite_start]Queries DNS to find the IP address of a domain[cite: 452]. | `nslookup google.com` |
| **`dig`** | [cite_start]Performs a detailed DNS lookup (shows Query time, TTL)[cite: 491]. | `dig google.com` |
| **`whois`** | [cite_start]Retrieves domain registration info (owner, expiry)[cite: 512]. | `whois google.com` |
| **`cat /etc/hosts`**| [cite_start]Displays local static IP-to-hostname mappings[cite: 488]. | `cat /etc/hosts` |
| **`curl`** | [cite_start]Transfers data from a server (HTTP GET/POST)[cite: 536]. | `curl https://google.com` |
| **`wget`** | [cite_start]Downloads files from the internet[cite: 546]. | `wget https://example.com/file.zip` |

---

## 8. Package & Archive Management

| Command | Description | Example |
| :--- | :--- | :--- |
| **`apt install`** | [cite_start]Installs a software package[cite: 219]. | `sudo apt install docker.io` |
| **`apt remove`** | [cite_start]Uninstalls a software package[cite: 230]. | `sudo apt remove docker.io` |
| **`which`** | [cite_start]Locates the execution path of a program[cite: 213]. | `which python` |
| **`zip`** | [cite_start]Compresses files into a zip archive[cite: 361]. | `zip archive.zip file1 file2` |
| **`unzip`** | [cite_start]Extracts files from a zip archive[cite: 371]. | `unzip archive.zip` |:wq

