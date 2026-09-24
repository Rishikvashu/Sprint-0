<p align="center">
  <img width="100%" height="200" style="object-fit: cover; border-radius: 6px;" alt="Ubuntu Banner" src="https://www.digitalcitizen.life/wp-content/uploads/2011/02/ubuntu.png" />
</p>

# SOP: System Administration | Ubuntu Linux | Common Commands

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Anurag Maurya | 25-08-2026 | v1 | Anurag Maurya | 25-08-2026 | Divya M | Aayush Verma | Mahesh Kumar/Varun |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ubuntu Linux](#2-what-is-ubuntu-linux)
3. [Why Ubuntu Linux is Required](#3-why-ubuntu-linux-is-required)
4. [Key Features of Ubuntu Linux](#4-key-features-of-ubuntu-linux)
5. [Prerequisites and System Requirements](#5-prerequisites-and-system-requirements)
6. [Ubuntu Commands Execution and Verification](#6-ubuntu-commands-execution-and-verification)
7. [Quick Commands](#7-quick-commands)
8. [Troubleshooting](#8-troubleshooting)
9. [Use Cases](#9-use-cases)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

Quick reference guide for common Ubuntu terminal commands used in daily server operations, system checks, file management, and package maintenance. Written in plain, simple English so beginners can comfortably manage Linux servers.

---

# 2. What is Ubuntu Linux

Ubuntu Linux is one of the most popular, open-source Linux operating systems used widely across web servers, cloud infrastructure, and software development environments. It provides a stable terminal shell environment where system administrators run commands to manage files, install software packages, monitor system memory, and configure network ports.

---

# 3. Why Ubuntu Linux is Required

Command-line proficiency in Ubuntu is essential for modern DevOps, system administration, and cloud management for three main reasons:
- **Server Stability**: Operating systems without graphical interfaces rely entirely on CLI commands for lightweight, fast, and secure server management.
- **Automation & Scripting**: Bash terminal commands can be chained into shell scripts to automate repetitive system tasks.
- **Resource Management**: Terminal tools allow real-time monitoring of CPU, RAM, disk space, and running processes to keep servers healthy.

---

# 4. Key Features of Ubuntu Linux

| **Feature** | **Description** |
| ----------- | --------------- |
| **APT Package Manager** | Easy installation, removal, and upgrading of software packages via `apt`. |
| **Systemd Service Control** | Centralized management of background system services using `systemctl`. |
| **POSIX File System** | Robust permissions architecture (`chmod`, `chown`) protecting files and directories. |
| **Resource Monitoring** | Built-in real-time tools (`top`, `ps`, `df`, `du`, `free`) to inspect system health. |
| **Networking Stack** | Powerful networking tools (`ss`, `ip`, `curl`) to monitor open ports and sockets. |

---

# 5. Prerequisites and System Requirements

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Access | Ubuntu 20.04/22.04/24.04 with SSH or terminal access |
| Required Packages | `coreutils`, `apt`, `systemd`, `procps`, `iproute2` |
| Required Commands | `ls`, `cd`, `pwd`, `cat`, `chmod`, `apt`, `systemctl`, `ps`, `df` |
| Permissions | User account with `sudo` access |
| Network | Connectivity for package downloads |
| Configuration | Standard bash or zsh shell |

> [!NOTE]
> Command output formatting, directory paths, and prompt names (such as `anurag@InfraNinja`) may vary slightly depending on your specific Linux distribution or system configuration.

---

# 6. Ubuntu Commands Execution and Verification

### Step 1: Inspect Directory Contents (`ls`)

Lists files and folders in a directory path.

```bash
ls -la /var/log
```

Expected output:

```bash
drwxr-xr-x  1 root root  4096 Aug 31 10:00 .
drwxr-xr-x  1 root root  4096 Aug 31 09:00 ..
-rw-r--r--  1 root root 12450 Aug 31 10:15 syslog
-rw-r-----  1 syslog adm 45210 Aug 31 10:15 auth.log
```

*What this command does:* Displays all files in `/var/log` (including hidden files starting with `.`) along with detailed permission strings, file ownership, file sizes in bytes, and last modification timestamps.

<details>
<summary>Click to view Terminal Screenshot: ls -la Directory Inspection</summary>
<br>

![ls -la Terminal Screenshot](./assets/ubuntu_ls_la.png)

</details>

---

### Step 2: Check Current Directory (`pwd`)

Prints your current working directory path.

```bash
pwd
```

Expected output:

```bash
/home/ubuntu
```

*What this command does:* Prints the absolute working directory path of your current shell session so you always know where you are operating in the filesystem before performing file edits or deletions.

<details>
<summary>Click to view Terminal Screenshot: pwd Working Directory Check</summary>
<br>

![pwd Terminal Screenshot](./assets/ubuntu_pwd.png)

</details>

---

### Step 3: Perform File & Directory Operations (`mkdir`, `cp`, `cat`)

Create folders, write content, and copy files safely.

```bash
# Create directory structure
mkdir -p /tmp/sop_demo/logs

# Create and write text into a file
echo "Server operational - initial log entry" > /tmp/sop_demo/app.log

# View file content
cat /tmp/sop_demo/app.log

# Copy file to backup folder
cp /tmp/sop_demo/app.log /tmp/sop_demo/logs/app.log.bak
```

Expected output:

```bash
Server operational - initial log entry
```

*What this command sequence does:* `mkdir -p` creates parent directories without throwing errors if they already exist; `echo >` writes string data into a file; `cat` reads file content to terminal stdout; `cp` duplicates the file into a backup location.

<details>
<summary>Click to view Terminal Screenshot: File & Directory Operations</summary>
<br>

![File Operations Terminal Screenshot](./assets/ubuntu_file_ops.png)

</details>

---

### Step 4: Manage File Permissions & Ownership (`chmod`, `chown`)

Adjust file read, write, and execute rights.

```bash
# Make script executable by owner
chmod 755 /tmp/sop_demo/app.log

# Change file permissions to read-only for group and others
chmod 644 /tmp/sop_demo/app.log

# Verify updated permissions
ls -l /tmp/sop_demo/app.log
```

Expected output:

```bash
-rw-r--r-- 1 ubuntu ubuntu 38 Aug 31 10:20 /tmp/sop_demo/app.log
```

*What this command sequence does:* `chmod 644` grants read & write rights (`6`) to the file owner, and read-only rights (`4`) to group members and other system users to enforce security best practices.

<details>
<summary>Click to view Terminal Screenshot: Permissions Management</summary>
<br>

![Permissions Management Terminal Screenshot](./assets/ubuntu_permissions.png)

</details>

---

### Step 5: Install & Update Packages (`apt`)

Update package index repositories and install utilities.

```bash
# Update local package index
sudo apt update -y

# Install utility package (e.g., curl)
sudo apt install -y curl
```

Expected output:

```bash
Hit:1 http://archive.ubuntu.com/ubuntu noble InRelease
Reading package lists... Done
curl is already the newest version (8.5.0-2ubuntu10.1).
```

*What this command sequence does:* `apt update` refreshes local repository metadata from Ubuntu mirrors; `apt install -y` automatically downloads, unpacks, and configures the target package without requiring manual interactive prompts.

<details>
<summary>Click to view Terminal Screenshot: APT Package Installation</summary>
<br>

![APT Package Installation Terminal Screenshot](./assets/ubuntu_apt_install.png)

</details>

---

### Step 6: Inspect Background Service Status (`systemctl`)

Check whether system services (like SSH, Nginx, Docker) are active.

```bash
# Check service status
sudo systemctl status ssh
```

Expected output:

```bash
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Sun 2026-08-31 09:00:00 UTC; 1h 30min ago
```

*What this command does:* Queries the Systemd init manager to report if the SSH daemon service is loaded, enabled at boot, and actively running without errors.

<details>
<summary>Click to view Terminal Screenshot: systemctl Service Status</summary>
<br>

![systemctl status Terminal Screenshot](./assets/ubuntu_systemctl_status.png)

</details>

---

### Step 7: Inspect Running Processes (`ps aux`)

Display a snapshot of all active processes on the system.

```bash
# List all running processes filtered by keyword
ps aux | grep sshd
```

Expected output:

```bash
root        1024  0.0  0.2  15800  4096 ?        Ss   09:00   0:00 sshd: /usr/sbin/sshd -D
```

*What this command sequence does:* `ps aux` prints process ID (PID), CPU usage percentage, memory consumption, running user, and exact command string for all active system processes; `grep sshd` filters out irrelevant processes.

<details>
<summary>Click to view Terminal Screenshot: Process Listing (ps aux)</summary>
<br>

![ps aux Process Listing Terminal Screenshot](./assets/ubuntu_ps_aux.png)

</details>

---

### Step 8: Monitor Real-Time System Resources (`top`)

Display dynamic real-time view of system CPU, RAM, and process activity.

```bash
# Launch interactive top monitor
top -b -n 1
```

Expected output:

```bash
top - 10:30:00 up 1:30, 1 user, load average: 0.08, 0.03, 0.01
Tasks: 110 total,   1 running, 109 sleeping
%Cpu(s):  1.5 us,  0.5 sy,  0.0 ni, 98.0 id
MiB Mem :   7950.0 total,   5120.0 free,   1830.0 used
```

*What this command sequence does:* Runs `top` in batch mode (`-b`) for a single iteration (`-n 1`) to capture an instant snapshot of CPU load average, total/used/free memory, and top active system processes.

<details>
<summary>Click to view Terminal Screenshot: Real-Time Resource Monitor (top)</summary>
<br>

![top Monitoring Terminal Screenshot](./assets/ubuntu_top_monitoring.png)

</details>

---

### Step 9: Check Disk Usage & Space (`df -h`)

Inspect free disk space across mounted filesystems.

```bash
df -h /
```

Expected output:

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   12G   36G  25% /
```

*What this command does:* Displays human-readable disk capacity (`-h`), showing total size in Gigabytes (G), used disk space, available free space, and disk usage percentage for the root filesystem `/`.

<details>
<summary>Click to view Terminal Screenshot: Disk Space Inspection (df -h)</summary>
<br>

![df -h Disk Space Terminal Screenshot](./assets/ubuntu_df_space.png)

</details>

---

### Step 10: Check Folder & Directory Size (`du -sh`)

Summarize disk space used by a folder and its subdirectories.

```bash
du -sh /var/log
```

Expected output:

```bash
142M    /var/log
```

*What this command does:* `du -sh` calculates and prints the total accumulated disk space consumed by `/var/log` in human-readable Megabytes (M) without listing individual files.

<details>
<summary>Click to view Terminal Screenshot: Directory Size Check (du -sh)</summary>
<br>

![Directory Size Terminal Screenshot](./assets/ubuntu_du_sh.png)

</details>

---

### Step 11: Inspect Free RAM & Swap Memory (`free -h`)

Check total, used, and available system RAM.

```bash
free -h
```

Expected output:

```bash
               total        used        free      shared  buff/cache   available
Mem:           7.8Gi       1.8Gi       5.0Gi       12Mi       1.0Gi       5.7Gi
Swap:          2.0Gi          0B       2.0Gi
```

*What this command does:* Reports physical RAM and swap space statistics in Gigabytes (`-h`), highlighting available memory available for launching new applications.

<details>
<summary>Click to view Terminal Screenshot: Memory Usage Check (free -h)</summary>
<br>

![Memory Usage Terminal Screenshot](./assets/ubuntu_free_h.png)

</details>

---

### Step 12: Inspect Open Network Ports & Sockets (`ss -tulpn`)

Display listening network ports and socket connections.

```bash
sudo ss -tulpn
```

Expected output:

```bash
Netid  State   Recv-Q  Send-Q   Local Address:Port   Peer Address:Port  Process
tcp    LISTEN  0       128            0.0.0.0:22          0.0.0.0:*      users:(("sshd",pid=1024,fd=3))
```

*What this command sequence does:* `-tulpn` lists listening (`l`) TCP (`t`) and UDP (`u`) sockets with process names (`p`) and numerical port addresses (`n`) to verify service bindings (such as SSH listening on port 22).

<details>
<summary>Click to view Terminal Screenshot: Open Ports & Sockets (ss -tulpn)</summary>
<br>

![Sockets Listing Terminal Screenshot](./assets/ubuntu_ss_ports.png)

</details>

---

# 7. Quick Commands

| **Task** | **Command** | **Description** |
| -------- | ----------- | --------------- |
| List files | `ls -la` | Show all files with details |
| Show path | `pwd` | Print current directory |
| File space | `df -h` | Show filesystem disk usage |
| Folder size | `du -sh <dir>` | Show folder size summary |
| Free memory | `free -h` | Show RAM and Swap usage |
| Process list | `ps aux` | List all running processes |
| Live monitor | `top` | Dynamic resource monitor |
| Service check | `sudo systemctl status <svc>` | Check background service status |
| Open ports | `sudo ss -tulpn` | Show active network ports |
| Install package | `sudo apt install -y <pkg>` | Install software package |

---

# 8. Troubleshooting

| **Symptom / Error** | **Possible Root Cause** | **Resolution Step** |
| ------------------- | ----------------------- | ------------------- |
| `Permission denied` | Command requires root/elevated privileges | Run command with `sudo` prefix or verify file ownership via `ls -l`. |
| `Command not found` | Package is not installed or missing from `PATH` | Install missing package via `sudo apt install <package_name>`. |
| `Could not get lock /var/lib/dpkg/lock` | Another `apt` process is currently running | Wait for ongoing background update to complete or reboot machine. |
| `No space left on device` | Disk partition is 100% full | Identify large files using `du -sh /*` and clear old log files or temp files. |
| `Service inactive (dead)` | Target service was stopped or crashed | Inspect service crash logs using `sudo journalctl -u <service_name> -n 50`. |

---

# 9. Use Cases

1. **Daily Server Health Audits**: L0 engineers check disk space (`df -h`), available memory (`free -h`), and running services (`systemctl`) during shift handovers.
2. **Package & Patch Maintenance**: Safely update system security patches using `apt update && apt upgrade`.
3. **Application Log Debugging**: Locate and inspect log files in `/var/log` using file navigation and text search tools.
4. **Port Binding Verification**: Ensure web servers (port 80/443) or SSH (port 22) are correctly listening on expected network sockets.

---

# 10. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Avoid `rm -rf /` | Always double-check working directory via `pwd` before running deletion commands (`rm -r`). |
| Use `df -h` before installs | Verify target disk partition has sufficient free capacity prior to initiating large software downloads. |
| Use relative permissions | Favor standard octal permissions (`644` for files, `755` for directories) to keep system secure. |
| Test commands dry-run | Test script commands interactively before placing them in automated crontabs or deployment scripts. |

---

# 11. Conclusion

Mastering basic Ubuntu terminal commands (`ls`, `pwd`, `apt`, `systemctl`, `df`, `free`, `ps`, `ss`) allows engineers to diagnose system issues quickly, keep Linux infrastructure operational, and manage servers efficiently.

---

# 12. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Anurag Maurya | [anurag.maurya.snaatak@mygurukulam.co](mailto:anurag.maurya.snaatak@mygurukulam.co) |

---

# 13. References

| **Topic** | **Description** |
| --------- | --------------- |
| [Ubuntu Official Documentation](https://ubuntu.com/server/docs) | Official Ubuntu server manual and CLI guide. |
| [Linux Man Pages](https://man7.org/linux/man-pages/) | Comprehensive reference manuals for standard Linux utilities. |
