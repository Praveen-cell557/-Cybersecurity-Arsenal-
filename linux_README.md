# 🐧 LINUX COMMANDS

## ⚡ THE CYBERSECURITY FIELD GUIDE

<p align="center">

<img src="https://img.shields.io/badge/LINUX-COMMANDS-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux">

<img src="https://img.shields.io/badge/SYSTEM-ADMINISTRATION-111111?style=for-the-badge&logo=gnubash&logoColor=white" alt="System Administration">

<img src="https://img.shields.io/badge-NETWORKING-2563EB?style=for-the-badge&logo=linux&logoColor=white" alt="Networking">

<img src="https://img.shields.io/badge/FORENSICS-8B5CF6?style=for-the-badge&logo=linux&logoColor=white" alt="Forensics">

</p>

<p align="center">
<b>🐧 Learn Linux through commands, real-world scenarios, system administration, networking, digital forensics, and security.</b>
</p>

---

# 🧠 LINUX IN ONE LINE

> **Linux is not just an operating system — it is a way of understanding what is happening underneath the system.**

From files and permissions to processes, networking, users, services, logs, and security, the Linux command line gives you direct visibility into the machine.

```text
                 🐧 LINUX
                    │
       ┌────────────┼────────────┐
       │            │            │
     📂 FILES     ⚙️ PROCESSES   🌐 NETWORK
       │            │            │
       ├────────────┼────────────┤
       │            │            │
    🔐 ACCESS     👤 USERS      📜 LOGS
       │            │            │
       └────────────┼────────────┘
                    │
              🧠 ANALYSIS
                    │
              🛡️ SECURITY
                    │
              🧪 FORENSICS
```

---

# 🚀 WHAT YOU CAN DO WITH LINUX

| 🧩 Area            | 🔥 What Linux Lets You Understand               |
| ------------------ | ----------------------------------------------- |
| 📂 **Files**       | Navigate, search, inspect, copy and manage data |
| 🔐 **Permissions** | Understand who can read, write or execute       |
| 👤 **Users**       | Identify accounts, groups and privileges        |
| ⚙️ **Processes**   | See what is running on the system               |
| 🛠️ **Services**   | Understand background services                  |
| 🌐 **Networking**  | Inspect interfaces, routes and connections      |
| 📜 **Logs**        | Investigate system and authentication activity  |
| 💾 **Storage**     | Understand disks, partitions and usage          |
| 📦 **Packages**    | Install and manage software                     |
| 🧠 **Bash**        | Automate repetitive tasks                       |
| 🔎 **Search**      | Find files, strings and patterns                |
| 🧪 **Forensics**   | Examine files, metadata and system activity     |
| 🛡️ **Security**   | Review security-relevant configurations         |

---

# 🗺️ THE LINUX COMMAND MAP

```text
                    LINUX
                      │
        ┌─────────────┼─────────────┐
        │             │             │
      FILES         USERS        NETWORK
        │             │             │
   Permissions     Groups       Interfaces
   Ownership       Sudo         Routes
   Search          Sessions     Connections
        │             │             │
        └─────────────┼─────────────┘
                      │
                  PROCESSES
                      │
                  SERVICES
                      │
                    LOGS
                      │
                  FORENSICS
                      │
                  SECURITY
```

---

# 📂 01 — NAVIGATION & FILE MANAGEMENT

> **First rule of Linux: know where you are and know what you're touching.**

| Command                             | What It Does                       | 🔎 Real-World Use             |
| ----------------------------------- | ---------------------------------- | ----------------------------- |
| `pwd`                               | Shows current directory            | Know your current location    |
| `ls -la`                            | Lists files including hidden files | Discover hidden configuration |
| `ls -lah`                           | Detailed human-readable listing    | Inspect file sizes            |
| `cd -`                              | Returns to previous directory      | Fast navigation               |
| `cp -r src dst`                     | Copies directories                 | Data backup                   |
| `mv src dst`                        | Moves or renames files             | File management               |
| `rm -rf dir/`                       | Removes directory recursively      | ⚠️ Destructive operation      |
| `mkdir -p a/b/c`                    | Creates nested directories         | Build directory structures    |
| `touch file.txt`                    | Creates file / updates timestamp   | File creation and testing     |
| `ln -s target link`                 | Creates symbolic link              | Link management               |
| `tree -L 2`                         | Displays directory tree            | Filesystem overview           |
| `stat file`                         | Shows file metadata                | 🧪 Timestamp investigation    |
| `file suspicious.bin`               | Identifies file type               | 🔍 File triage                |
| `readlink -f file`                  | Resolves symlink path              | Path investigation            |
| `basename /path/file.txt`           | Extracts filename                  | Shell scripting               |
| `dirname /path/file.txt`            | Extracts directory                 | Shell scripting               |
| `find / -name "*.conf" 2>/dev/null` | Searches for files                 | Configuration discovery       |
| `locate filename`                   | Fast indexed file search           | Rapid file discovery          |

### 💡 Real-World Scenario

```bash
pwd
ls -lah
find /var/log -type f 2>/dev/null
```

**Situation:** You are investigating a Linux machine and need to identify your location and available log files before continuing.

---

# 🔐 02 — PERMISSIONS & OWNERSHIP

> **Linux security begins with permissions.**

```text
             FILE
              │
      ┌───────┼───────┐
      ↓       ↓       ↓
    OWNER   GROUP   OTHERS
      │       │       │
     rwx     rwx     rwx
```

| Command                                | Purpose                    | Security Use            |
| -------------------------------------- | -------------------------- | ----------------------- |
| `chmod 755 file`                       | Changes permissions        | Access-control review   |
| `chmod +x script.sh`                   | Makes script executable    | Script management       |
| `chown user:group file`                | Changes ownership          | Ownership investigation |
| `umask 022`                            | Sets default permissions   | Permission hardening    |
| `getfacl file`                         | Shows ACLs                 | Detailed access review  |
| `setfacl -m u:user:rwx file`           | Adds ACL permission        | Controlled access       |
| `chattr +i file`                       | Makes file immutable       | File protection         |
| `lsattr file`                          | Shows file attributes      | Forensic analysis       |
| `find / -perm -2000 2>/dev/null`       | Finds SGID files           | Security enumeration    |
| `find / -writable -type d 2>/dev/null` | Finds writable directories | Configuration review    |

### 🧩 Permission Numbers

```text
4 = READ
2 = WRITE
1 = EXECUTE

7 = rwx
6 = rw-
5 = r-x
4 = r--
3 = -wx
2 = -w-
1 = --x
0 = ---
```

---

# 🔎 03 — FILE SEARCH & TEXT PROCESSING

> **When the system contains thousands of files, search becomes power.**

| Command                            | Purpose                   | 🔥 Use             |
| ---------------------------------- | ------------------------- | ------------------ |
| `grep -rn "pattern" .`             | Recursive search          | Log investigation  |
| `grep -i "error" log.txt`          | Case-insensitive search   | Error analysis     |
| `grep -v "pattern" file`           | Excludes matches          | Data filtering     |
| `grep -E "regex" file`             | Regex search              | Pattern analysis   |
| `awk '{print $1}' file`            | Extracts field            | Data processing    |
| `awk -F: '{print $1}' /etc/passwd` | Extracts usernames        | Account analysis   |
| `sed 's/old/new/g' file`           | Replaces text             | Text processing    |
| `sort -u file`                     | Sorts/removes duplicates  | Data cleanup       |
| `uniq -c`                          | Counts repeated lines     | Frequency analysis |
| `cut -d',' -f2 file.csv`           | Extracts CSV field        | Data analysis      |
| `wc -l file`                       | Counts lines              | Log statistics     |
| `diff file1 file2`                 | Compares files            | Integrity checking |
| `xxd file`                         | Hex dump                  | Binary analysis    |
| `strings binary`                   | Extracts readable strings | File triage        |
| `head -n 20 file`                  | Shows beginning           | File inspection    |
| `tail -f log`                      | Follows live log          | 🛡️ Monitoring     |
| `base64 -d file`                   | Decodes Base64            | Data analysis      |
| `jq '.key' data.json`              | Parses JSON               | Log/API analysis   |

---

# 🌐 04 — NETWORKING

> **A Linux machine is a node. Networking tells you what it can see and where it can communicate.**

### 🟢 Interfaces & Routes

```bash
ip a
ip route
arp -a
```

| Command    | Purpose                      |
| ---------- | ---------------------------- |
| `ip a`     | Network interfaces           |
| `ifconfig` | Legacy interface information |
| `ip route` | Routing table                |
| `arp -a`   | ARP cache                    |

### 🔵 Connections

```bash
ss -tulnp
netstat -tulnp
```

| Command                | Purpose                       |
| ---------------------- | ----------------------------- |
| `ss -tulnp`            | Listening ports and processes |
| `netstat -tulnp`       | Legacy connection information |
| `nmap -sV -sC target`  | Service/version discovery     |
| `nmap -p- target`      | Full TCP port scan            |
| `nmap -sU target`      | UDP scanning                  |
| `nc -zv target 1-1000` | Port connectivity testing     |

### 🌍 DNS / Web

```bash
dig domain.com
dig -x IP
nslookup domain.com
curl -I url
```

### 🛰️ Traffic

```bash
tcpdump -i eth0 -w capture.pcap
tcpdump -i eth0 port 80
```

> [!WARNING]
> Network scanning and traffic capture should only be performed on networks where you have authorization.

---

# ⚙️ 05 — PROCESSES & SYSTEM MANAGEMENT

> **If you don't know what is running, you don't fully understand the machine.**

| Command                                | Purpose                        |
| -------------------------------------- | ------------------------------ |
| `ps aux`                               | View running processes         |
| `ps -ef --forest`                      | View process hierarchy         |
| `top`                                  | Live process monitoring        |
| `htop`                                 | Interactive process monitoring |
| `kill -9 PID`                          | Force terminate process        |
| `killall processname`                  | Terminate by process name      |
| `pkill -f pattern`                     | Terminate matching process     |
| `systemctl status service`             | Check service status           |
| `systemctl start/stop/restart service` | Manage services                |
| `systemctl enable service`             | Enable service at boot         |
| `journalctl -xe`                       | Inspect systemd logs           |
| `uptime`                               | System uptime/load             |
| `uname -a`                             | Kernel/system information      |
| `lscpu`                                | CPU information                |
| `free -h`                              | Memory usage                   |
| `crontab -l`                           | User scheduled tasks           |
| `cat /etc/crontab`                     | System-wide cron configuration |

---

# 👤 06 — USERS & GROUPS

> **Identity → Privilege → Access**

```bash
whoami
id
who
w
last
```

| Command           | What It Shows           |
| ----------------- | ----------------------- |
| `whoami`          | Current user            |
| `id`              | UID, GID and groups     |
| `who`             | Logged-in users         |
| `w`               | User/session activity   |
| `last`            | Login history           |
| `groups user`     | User groups             |
| `cat /etc/passwd` | System users            |
| `sudo -l`         | Current sudo privileges |
| `visudo`          | Safe sudoers editing    |

> 🔐 `/etc/shadow` contains sensitive authentication information and should only be accessed within authorized administrative or forensic workflows.

---

# 📦 07 — PACKAGE MANAGEMENT

| Linux Family       | Commands              |
| ------------------ | --------------------- |
| 🟢 Debian / Ubuntu | `apt` · `dpkg`        |
| 🔵 RHEL / CentOS   | `yum` · `dnf` · `rpm` |
| 🟣 Arch            | `pacman`              |
| ⚪ Universal        | `snap` · `flatpak`    |

### Example

```bash
apt update
apt upgrade
apt install package
dpkg -l
```

---

# 🗜️ 08 — COMPRESSION & ARCHIVES

| Command                          | Purpose             |
| -------------------------------- | ------------------- |
| `tar -czvf archive.tar.gz dir/`  | Create archive      |
| `tar -xzvf archive.tar.gz`       | Extract archive     |
| `tar -cjvf archive.tar.bz2 dir/` | Create BZIP archive |
| `zip -r archive.zip dir/`        | Create ZIP          |
| `unzip archive.zip`              | Extract ZIP         |
| `gzip file`                      | Compress            |
| `gunzip file.gz`                 | Decompress          |
| `7z x archive.7z`                | Extract 7-Zip       |

---

# 💾 09 — DISK & STORAGE

| Command               | Purpose                |
| --------------------- | ---------------------- |
| `df -h`               | Disk usage             |
| `du -sh dir/`         | Directory size         |
| `lsblk`               | Block devices          |
| `fdisk -l`            | Partitions             |
| `mount /dev/sdX /mnt` | Mount device           |
| `umount /mnt`         | Unmount device         |
| `mkfs.ext4 /dev/sdX1` | Format filesystem      |
| `dd ...`              | Low-level data copying |

> [!CAUTION]
> Commands such as `mkfs` and `dd` can destroy data if used against the wrong device. Always verify the target in a lab or authorized environment.

---

# 📜 10 — LOGGING & MONITORING

> **Logs are the story of what happened.**

| Log / Command               | Purpose                                       |
| --------------------------- | --------------------------------------------- |
| `/var/log/auth.log`         | Authentication activity                       |
| `/var/log/secure`           | Authentication activity on RHEL-based systems |
| `/var/log/syslog`           | General system events                         |
| `tail -f /var/log/auth.log` | Live authentication monitoring                |
| `dmesg`                     | Kernel messages                               |
| `journalctl -u sshd`        | SSH service logs                              |
| `lastb`                     | Failed login history                          |
| `auditctl -l`               | Audit rules                                   |

### 🕵️ Investigation Chain

```text
LOGIN
  ↓
PROCESS
  ↓
NETWORK
  ↓
FILE
  ↓
LOG
  ↓
TIMELINE
  ↓
FINDING
```

---

# 🧠 11 — BASH SCRIPTING

```bash
#!/bin/bash

NAME="Linux"

echo "Hello, $NAME"

for i in {1..5}; do
    echo "$i"
done

if [ -f "/etc/passwd" ]; then
    echo "File exists"
fi

greet() {
    echo "Hello $1"
}

greet "Security"
```

### ⚡ Why Bash Matters

```text
MANUAL COMMAND
      ↓
REPEAT
      ↓
SCRIPT
      ↓
AUTOMATION
      ↓
SCALE
```

---

# ⚡ 12 — USEFUL ONE-LINERS

### 🔎 Find SUID Files

```bash
find / -perm -u=s -type f 2>/dev/null
```

### 📂 Find World-Writable Files

```bash
find / -xdev -type f -perm -0002 2>/dev/null
```

### 📊 Find Large Files

```bash
find / -type f -exec du -h {} + 2>/dev/null | sort -rh | head -10
```

### 🌐 Monitor Listening Services

```bash
watch -n 2 'ss -tulnp'
```

### 🧪 Local HTTP Server

```bash
python3 -m http.server 8000
```

### 🔎 Search Bash History

```bash
grep -i "password" ~/.bash_history
```

### 🔑 Generate Random Data

```bash
openssl rand -base64 16
```

---

# 🎯 13 — SECURITY ENUMERATION

> **Enumeration is observation, not exploitation. Understand the system before drawing conclusions.**

| Check           | Command                                 |
| --------------- | --------------------------------------- |
| 🖥️ OS          | `uname -a`                              |
| 🐧 Distribution | `cat /etc/os-release`                   |
| 🔐 Sudo         | `sudo -l`                               |
| 🧩 SUID         | `find / -perm -u=s -type f 2>/dev/null` |
| 🧩 SGID         | `find / -perm -g=s -type f 2>/dev/null` |
| 🔑 Capabilities | `getcap -r / 2>/dev/null`               |
| ⏰ Cron          | `find /etc/cron* -writable 2>/dev/null` |
| 🌎 Environment  | `env`                                   |
| 🛣️ PATH        | `echo $PATH`                            |

---

# 🧪 14 — DIGITAL FORENSICS FLOW

```text
                 🐧 LINUX SYSTEM
                       │
                       ▼
                🖥️ IDENTIFY HOST
                       │
                       ▼
                 👤 IDENTIFY USERS
                       │
                       ▼
                ⚙️ ANALYZE PROCESSES
                       │
                       ▼
                 🌐 CHECK NETWORK
                       │
                       ▼
                  📂 CHECK FILES
                       │
                       ▼
                🔐 CHECK PERMISSIONS
                       │
                       ▼
                   📜 CHECK LOGS
                       │
                       ▼
                  🕒 BUILD TIMELINE
                       │
                       ▼
                   📝 DOCUMENT
                       │
                       ▼
                    🛡️ FINDING
```

---

# 🧭 15 — LINUX LEARNING PATH

```text
                🐧 LINUX
                   │
                   ▼
             📂 FILESYSTEM
                   │
                   ▼
             🔐 PERMISSIONS
                   │
                   ▼
             👤 USERS & GROUPS
                   │
                   ▼
             ⚙️ PROCESSES
                   │
                   ▼
             🌐 NETWORKING
                   │
                   ▼
               📜 LOGS
                   │
                   ▼
             🧠 BASH SCRIPTING
                   │
                   ▼
             🧪 FORENSICS
                   │
                   ▼
             🛡️ SECURITY
```

---

# ⚡ THE 20 COMMANDS TO REMEMBER

|  # | Command      | Why It Matters                     |
| -: | ------------ | ---------------------------------- |
| 01 | `pwd`        | Where am I?                        |
| 02 | `ls -la`     | What is here?                      |
| 03 | `cd`         | Move around                        |
| 04 | `find`       | Find anything                      |
| 05 | `grep`       | Search anything                    |
| 06 | `cat`        | Read files                         |
| 07 | `less`       | Read large files                   |
| 08 | `stat`       | Inspect metadata                   |
| 09 | `chmod`      | Control permissions                |
| 10 | `chown`      | Control ownership                  |
| 11 | `whoami`     | Who am I?                          |
| 12 | `id`         | What access do I have?             |
| 13 | `ps`         | What's running?                    |
| 14 | `systemctl`  | What's running as a service?       |
| 15 | `ip`         | What's my network state?           |
| 16 | `ss`         | What's connected?                  |
| 17 | `df`         | How much storage exists?           |
| 18 | `journalctl` | What happened?                     |
| 19 | `sudo -l`    | What administrative access exists? |
| 20 | `bash`       | How can I automate it?             |

---

# 🚨 THE LINUX MINDSET

Don't just memorize:

```bash
ls
ps
ip
ss
grep
find
```

Understand the questions behind them:

```text
        WHERE AM I?
             ↓
        WHAT EXISTS?
             ↓
        WHO AM I?
             ↓
        WHAT CAN I ACCESS?
             ↓
        WHAT IS RUNNING?
             ↓
        WHO IS CONNECTED?
             ↓
        WHAT HAPPENED?
             ↓
        WHAT DOES THE EVIDENCE SHOW?
```

> **Linux becomes powerful when commands stop being memorized and start becoming questions.**

---

<p align="center">

<b>🐧 LINUX • 🔐 SECURITY • 🌐 NETWORKING • 📜 LOGS • 🧪 FORENSICS</b>

<br><br>

<b>⚡ LEARN THE COMMAND. UNDERSTAND THE SYSTEM. INVESTIGATE THE EVIDENCE. ⚡</b>

</p>
