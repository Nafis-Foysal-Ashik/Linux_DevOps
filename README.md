# Linux & DevOps Study Notes

This repository contains comprehensive study notes on Linux fundamentals, file management, system monitoring, and networking tools essential for DevOps. These notes cover architecture, permissions, user management, and advanced command-line tools.

## 1. Linux Core Concepts & Architecture

**Linux** is an open-source operating system where "everything is a file".
* **Architecture Layers**: Hardware → Kernel → Shell → Application.
* **Kernel**: The core that communicates with hardware and manages resources. It is secure by design; normal apps cannot change system files directly.
* **Shell**: The user interface (CLI) that interprets commands (like `mkdir`) and sends them to the kernel for execution.
* **Linux vs. Windows**: Linux is open-source (GPL) and file-based. Windows is commercial and uses drive letters.

---

## 2. File & Folder Management

### Navigation & Listing
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ls`** | Lists files and folders in the current directory. | `ls` |
| **`ls -l`** | Lists files with detailed info (permissions, owner, size, time). | `ls -l` |
| **`ls -ltr`** | Lists details sorted by modification time in reverse order (oldest to newest). | `ls -ltr` |
| **`lsblk`** | Lists information about all available block devices (disk partitions). | `lsblk` |
| **`pwd`** | Prints the current working directory path. | `pwd` |

### Creation & Deletion
| Command | Description | Example |
| :--- | :--- | :--- |
| **`touch`** | Creates a new empty file. | `touch newfile.txt` |
| **`mkdir`** | Creates a new folder (directory). | `mkdir myfolder` |
| **`rm`** | Removes (deletes) a file. | `rm filename.txt` |
| **`rmdir`** | Removes a folder (must be empty). | `rmdir myfolder` |
| **`rm -rf`** | Forcefully removes a directory and its contents (implied for non-empty folders). | `sudo rm -rf /home/user/dir` |

### Manipulation
| Command | Description | Example |
| :--- | :--- | :--- |
| **`cp`** | Copies a file or folder from source to destination. | `cp source.txt destination.txt` |
| **`mv`** | Moves a file/folder to a new location or renames it. | `mv oldname.txt newname.txt` |
| **`ln -s`** | Creates a "soft link" (shortcut). If the source is deleted, the link breaks. | `ln -s /path/to/file linkname` |
| **`ln`** | Creates a "hard link". If the source is deleted, the file data remains accessible via the link. | `ln /path/to/file linkname` |

---

## 3. File Content & Text Processing

### Viewing Content
| Command | Description | Example |
| :--- | :--- | :--- |
| **`cat`** | Displays the full content of a file. | `cat filename.txt` |
| **`head`** | Displays the first few lines of a file. | `head filename.txt` |
| **`tail`** | Displays the last few lines of a file. | `tail filename.txt` |
| **`tail -f`** | Follows the end of a file in real-time (useful for monitoring logs). | `tail -f /var/log/syslog` |
| **`less`** | Views large file content page-by-page. (Use arrows to scroll, `q` to quit). | `less largefile.txt` |
| **`more`** | Similar to `less`, views content one page at a time (Space for next page). | `more largefile.txt` |
| **`cal`** | Displays a calendar in the terminal. | `cal` |
| **`zcat`** | Views the content of a compressed (zip) file without unzipping. | `zcat archive.zip` |

### Editing & Writing
| Command | Description | Example |
| :--- | :--- | :--- |
| **`echo`** | Prints text to the terminal or writes to a file using redirection (`>`). | `echo "Hello World" > file.txt` |
| **`nano`** | Simple terminal text editor. Use `Ctrl+X` to exit. | `nano file.txt` |
| **`vim`** | Advanced text editor. Press `i` to insert, `:wq` to save and quit. | `vim file.txt` |
| **`tee`** | Reads from standard input and writes to both standard output and files. | `echo "hello" | tee file.txt` |

### Advanced Processing (awk, sed, grep)
| Command | Description | Example |
| :--- | :--- | :--- |
| **`wc`** | Counts lines, words, and characters in a file. | `wc filename.txt` |
| **`cut`** | Extracts specific sections (bytes/columns) from lines of files. | `cut -b 1-4 filename` |
| **`sort`** | Sorts the contents of a text file alphabetically. | `sort filename.txt` |
| **`grep`** | Searches for a specific pattern/word inside a file. | `grep "INFO" logfile.txt` |
| **`grep -i`** | Search ignoring case (case-insensitive). | `grep -i "error" logfile.txt` |
| **`grep -c`** | Counts the occurrences of a pattern in a file. | `grep -c "INFO" logfile.txt` |
| **`awk`** | Scans and processes files, useful for structured data (printing specific columns). | `awk '{print $1}' filename` |
| **`sed`** | Stream editor for filtering and transforming text (e.g., find and replace). | `sed 's/LOG/INFO/g' file.txt` |

---

## 4. User & Group Management

### User Actions
| Command | Description | Example |
| :--- | :--- | :--- |
| **`sudo`** | Executes a command with superuser (admin) privileges. | `sudo apt update` |
| **`who`** | Shows who is currently logged into the system. | `who` |
| **`whoami`** | Displays the current effective username. | `whoami` |
| **`su`** | Switches to another user account. | `su username` |
| **`useradd`** | Creates a new user. | `sudo useradd -m newuser` |
| **`passwd`** | Sets or changes a user's password. | `sudo passwd newuser` |
| **`userdel`** | Deletes a user account. | `sudo userdel newuser` |
| **`cat /etc/passwd`**| Lists all users defined on the system. | `cat /etc/passwd` |

### Group Actions
| Command | Description | Example |
| :--- | :--- | :--- |
| **`groupadd`** | Creates a new group. | `sudo groupadd devops` |
| **`groupdel`** | Deletes an existing group. | `sudo groupdel devops` |
| **`gpasswd -a`** | Adds a user to a group. | `sudo gpasswd -a user group` |
| **`gpasswd -M`** | Adds multiple users to a group at once. | `sudo gpasswd -M u1,u2 group` |
| **`cat /etc/group`** | Lists all groups defined on the system. | `cat /etc/group` |
| **`getent group`** | Displays details of a specific group. | `getent group sudo` |

---

## 5. Permissions & Ownership
Permissions are represented as Read (**r**=4), Write (**w**=2), Execute (**x**=1).

| Command | Description | Example |
| :--- | :--- | :--- |
| **`chmod`** | Changes file permissions. | `chmod 755 script.sh` |
| **`chmod 777`** | Gives full read, write, and execute permissions to everyone. | `chmod 777 file.txt` |
| **`chmod +x`** | Adds execution permission for all users. | `chmod +x script.sh` |
| **`chmod -x`** | Removes execution permission for all users. | `chmod -x script.sh` |
| **`chmod -w`** | Removes write permission for "others". | `chmod o-w file.txt` |
| **`chown`** | Changes the owner of a file or folder. | `sudo chown user file.txt` |
| **`chgrp`** | Changes the group ownership of a file. | `sudo chgrp group file.txt` |
| **`umask`** | Sets default permissions for newly created files/folders. | `umask 0022` |

---

## 6. System Monitoring & Resources

| Command | Description | Example |
| :--- | :--- | :--- |
| **`top`** | Displays real-time system performance, CPU, RAM, and processes. | `top` |
| **`kill`** | Terminates a process (usually via PID). | `kill 1234` |
| **`df -h`** | Shows disk space usage in human-readable format. | `df -h` |
| **`du`** | Shows disk usage (size) of files and folders. | `du foldername` |
| **`du -sh`** | Shows summary of disk usage for a specific directory in human-readable form. | `du -sh Downloads/` |
| **`free`** | Displays amount of free and used memory. | `free` |
| **`free -h`** | Displays memory details in human-readable (GB/MB) format. | `free -h` |
| **`vmstat`** | Reports virtual memory, swap, disk, and CPU activity. | `vmstat 2` |
| **`nohup`** | Runs a command in the background that keeps running even if the terminal closes. | `nohup command &` |
| **`shutdown`** | Shuts down the system. | `sudo shutdown now` |
| **`reboot`** | Restarts the system. | `sudo reboot` |

---

## 7. Networking Tools (DevOps Focused)

### Connectivity & Diagnostics
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ping`** | Checks network connectivity to a host. | `ping google.com` |
| **`ping -i`** | Sets the time interval between pings. | `ping -i 2 google.com` |
| **`ping -w`** | Sets a deadline (timeout) in seconds for the ping command. | `ping -w 5 google.com` |
| **`telnet`** | Checks raw TCP connectivity to a specific port. | `telnet google.com 80` |
| **`traceroute`** | Shows the path (hops) packets take to a destination. | `traceroute google.com` |
| **`tracepath`** | Similar to traceroute, shows MTU (Max Transmission Unit). | `tracepath google.com` |
| **`mtr`** | Combines `ping` and `traceroute` for real-time diagnostics. | `mtr google.com` |
| **`ifplugstatus`** | Checks if the network cable is plugged in. | `ifplugstatus` |

### Network Information
| Command | Description | Example |
| :--- | :--- | :--- |
| **`ip a`** | Displays all network interfaces and IP addresses. | `ip a` |
| **`ip neigh`** | Shows the neighbor table (ARP cache). | `ip neigh` |
| **`ip route`** | Shows the routing table and gateway info. | `ip route` |
| **`netstat`** | Shows network connections and listening ports. | `netstat -tuln` |
| **`nmap`** | Scans a server for open ports and system details. | `nmap -v facebook.com` |

### DNS & Web
| Command | Description | Example |
| :--- | :--- | :--- |
| **`nslookup`** | Queries DNS to find the IP address of a domain. | `nslookup google.com` |
| **`dig`** | Performs a detailed DNS lookup (shows Query time, TTL). | `dig google.com` |
| **`whois`** | Retrieves domain registration info (owner, expiry). | `whois google.com` |
| **`cat /etc/hosts`**| Displays local static IP-to-hostname mappings. | `cat /etc/hosts` |
| **`curl`** | Transfers data from a server (HTTP GET/POST). | `curl https://google.com` |
| **`wget`** | Downloads files from the internet. | `wget https://example.com/file.zip` |

---

## 8. Package & Archive Management

| Command | Description | Example |
| :--- | :--- | :--- |
| **`apt install`** | Installs a software package. | `sudo apt install docker.io` |
| **`apt remove`** | Uninstalls a software package. | `sudo apt remove docker.io` |
| **`which`** | Locates the execution path of a program. | `which python` |
| **`zip`** | Compresses files into a zip archive. | `zip archive.zip file1 file2` |
| **`unzip`** | Extracts files from a zip archive. | `unzip archive.zip` |
