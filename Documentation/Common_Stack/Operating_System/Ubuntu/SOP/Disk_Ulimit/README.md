# SOP: Disk & Ulimit

<p align="center">
<img width="540" height="243" alt="image" src="https://github.com/user-attachments/assets/703a4f96-1ccd-42ea-bc52-cd6b0bec18f6" />
</p>


---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Maqbool Alam | 24-08-2026 | 1.1 | Maqbool Alam | 24-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Disk Usage and Mount Points](#4-disk-usage-and-mount-points)
5. [Ulimit Configuration](#5-ulimit-configuration)
6. [Process-Level Limits](#6-process-level-limits)
7. [Validation](#7-validation)
8. [Use Cases](#8-use-cases)
9. [Troubleshooting](#9-troubleshooting)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

This SOP provides a structured guide to checking and managing **disk usage, filesystem mount points, user limits, and process limits** on Linux/Ubuntu systems.

It covers disk-capacity checks, identification of mount points, filesystem usage, inode usage, persistent `ulimit` configuration, systemd process limits, and validation procedures.

The procedures are intended to help administrators maintain **system stability, reliability, performance, and operational consistency**.

---

# 2. Purpose

The purpose of this SOP is to provide a standardized procedure for:

- Checking filesystem and disk usage.
- Identifying mounted disks, partitions, and mount points.
- Identifying large files and directories consuming disk space.
- Checking inode utilization.
- Checking current user and shell resource limits.
- Configuring persistent user-level `ulimit` settings.
- Configuring limits for systemd-managed services.
- Validating disk and `ulimit` configurations.
- Troubleshooting disk-full and resource-limit issues.

These procedures help maintain **system stability, reliability, performance, and operational consistency**.

---

# 3. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Access | Ubuntu/Linux server with SSH or terminal access |
| Required Commands | `df`, `du`, `lsblk`, `findmnt`, `mount`, `ulimit`, `ps` |
| Permissions | `sudo/root` access for system-level configuration |
| Network | Not required for normal disk and ulimit operations |
| Configuration | Backup configuration files before making permanent changes |

> **NOTE**
> The exact `ulimit` values should be selected according to application requirements. Do not increase limits blindly.

---

# 4. Disk Usage and Mount Points

## Step 1: Check Overall Disk Usage

Use `df` to check filesystem capacity and available space.

```bash
df -h
```

Expected output:

<img width="1235" height="227" alt="screen1" src="https://github.com/user-attachments/assets/afb1a46b-c311-458f-8736-1d41dcbf571a" />

The important fields are:

- `Size` — Total filesystem capacity.
- `Used` — Space currently used.
- `Avail` — Available space.
- `Use%` — Percentage used.
- `Mounted on` — Mount point.

---

## Step 2: Check Filesystem Type

```bash
df -Th
```

Example:

<img width="1235" height="227" alt="screen2" src="https://github.com/user-attachments/assets/2fe1d5d6-3dbc-4cf7-b7c0-112f5594482d" />

This helps identify whether the filesystem is `ext4`, `xfs`, `btrfs`, etc.

---

## Step 3: List Disks, Partitions and Mount Points

```bash
lsblk
```

For filesystem information:

```bash
lsblk -f
```

For a more detailed view:

```bash
lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINTS,UUID
```

Example:

<img width="1235" height="912" alt="screen3" src="https://github.com/user-attachments/assets/96056e3e-e6ac-401d-b726-83a5d1577d8b" />
<img width="1235" height="912" alt="screen4" src="https://github.com/user-attachments/assets/49aad630-62a1-4f26-ae38-de63f4d3b176" />
<img width="1235" height="912" alt="screen5" src="https://github.com/user-attachments/assets/acea5389-d2e6-4477-b9e0-7917b165e867" />

---

## Step 4: Check Current Mount Points

```bash
findmnt
```
<img width="1235" height="912" alt="screen6" src="https://github.com/user-attachments/assets/773f8ac3-d0ae-417b-9ea9-a1713a4a4293" />

To check a specific mount point:

```bash
findmnt /
```
<img width="1235" height="120" alt="screen7" src="https://github.com/user-attachments/assets/48de8923-97d7-4ec7-b774-bda8f65477f0" />

To display mounts in a readable format:

```bash
mount | column -t
```
<img width="1859" height="917" alt="screen8" src="https://github.com/user-attachments/assets/bac59940-7286-4de3-8fd5-c63ce5d3d6eb" />

---

## Step 5: Identify Disk Usage by Directory

Run:

```bash
sudo du -xh --max-depth=1 / 2>/dev/null | sort -h
```

For example:

```text
2.1G    /opt
5.8G    /usr
12G     /home
35G     /var
65G     /
```

If `/var` is consuming significant space:

```bash
sudo du -xh --max-depth=1 /var 2>/dev/null | sort -h
```

For `/home`:

```bash
sudo du -xh --max-depth=1 /home 2>/dev/null | sort -h
```

<img width="1859" height="279" alt="screen9" src="https://github.com/user-attachments/assets/45ea060e-a761-4081-8745-1b2668a0ea09" />

---

## Step 6: Find Large Files

To find files larger than 1 GB:

```bash
sudo find / -xdev -type f -size +1G -exec ls -lh {} \; 2>/dev/null
```

<img width="1859" height="61" alt="screen10" src="https://github.com/user-attachments/assets/57c62fe7-916d-40ee-b83a-f8470e98145a" />


To find the largest files:

```bash
sudo find / -xdev -type f -printf '%s %p\n' 2>/dev/null \
  | sort -nr | head -20 \
  | numfmt --field=1 --to=iec
```

> **NOTE**
> Use `-xdev` when investigating a particular filesystem so that mounted filesystems are not unintentionally included.

---

## Step 7: Check Inode Usage

A filesystem can run out of inodes even when disk space is available.

```bash
df -i
```

Example:

<img width="1859" height="225" alt="screen11" src="https://github.com/user-attachments/assets/271c9fe4-8445-4436-b1ae-777644f9c301" />

If `IUse%` approaches 100%, investigate directories containing very large numbers of small files.

---

## Step 8: Check Open Deleted Files

A deleted file may continue consuming disk space if a running process still has it open.

```bash
sudo lsof +L1
```

If a large deleted file is found, identify the owning process:

```bash
sudo lsof +L1
```

Then restart the relevant application/service according to the application's operational procedure.

<img width="1859" height="974" alt="screen12" src="https://github.com/user-attachments/assets/d1a1883d-6cfb-421a-8202-a7054a94a0c3" />

---

## Step 9: Check Persistent Mount Configuration

Review `/etc/fstab`:

```bash
sudo cat /etc/fstab
```

Before applying changes:

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

After modifying `/etc/fstab`, validate the configuration:

```bash
sudo mount -a
```

<img width="1859" height="331" alt="screen13" src="https://github.com/user-attachments/assets/4a9a61de-eeed-4792-928c-bf5b319b5167" />

If the command returns no error, the filesystem entries were successfully parsed and mounted.

---

# 5. Ulimit Configuration

## Step 1: Check Current Shell Limits

Run:

```bash
ulimit -a
```

Example:

```text
core file size          (blocks, -c) 0
open files                      (-n) 1024
max user processes              (-u) 4096
stack size              (kbytes, -s) 8192
virtual memory          (kbytes, -v) unlimited
```

<img width="1859" height="331" alt="screen14" src="https://github.com/user-attachments/assets/1797fe4c-0c99-4763-b7c0-22897d2281b4" />

---

## Step 2: Check a Specific Limit

Open files:

```bash
ulimit -n
```

Maximum user processes:

```bash
ulimit -u
```

Core dump size:

```bash
ulimit -c
```

Stack size:

```bash
ulimit -s
```

<img width="1859" height="481" alt="screen15" src="https://github.com/user-attachments/assets/75fc2133-ea76-45bf-b7fa-996c860cd106" />

---

## Step 3: Temporarily Change a Limit

For the current shell session only:

```bash
ulimit -n 65535
```

Verify:

```bash
ulimit -n
```

Expected:

```text
65535
```

> **WARNING**
> Changes made using `ulimit` directly affect the current shell and processes started from it. They are not persistent across new login sessions.

---

## Step 4: Configure Persistent User Limits

Edit:

```bash
sudo nano /etc/security/limits.conf
```

Example:

```text
appuser soft nofile 65535
appuser hard nofile 65535

appuser soft nproc 16384
appuser hard nproc 16384
```

Where:

- `appuser` = target Linux user.
- `soft` = default limit applied to the session.
- `hard` = maximum limit that the user can request.
- `nofile` = maximum number of open file descriptors.
- `nproc` = maximum number of processes available to the user.

---

## Step 5: Use a Dedicated Limits Configuration File

Instead of modifying the main configuration, create a file under:

```bash
/etc/security/limits.d/
```

Example:

```bash
sudo nano /etc/security/limits.d/appuser.conf
```

Add:

```text
appuser soft nofile 65535
appuser hard nofile 65535
appuser soft nproc 16384
appuser hard nproc 16384
```

This approach keeps application-specific limits separate from the main configuration.

---

## Step 6: Verify PAM Limits Configuration

Check whether `pam_limits` is enabled:

```bash
grep -R "pam_limits.so" /etc/pam.d/
```

Expected configuration normally contains:

```text
session required pam_limits.so
```

The exact PAM files can vary depending on the distribution and login mechanism.

---

# 6. Process-Level Limits

## Step 1: Identify the Process

```bash
ps aux | grep <process-name>
```

Example:

```bash
ps aux | grep jenkins
```

<img width="1859" height="66" alt="screen16" src="https://github.com/user-attachments/assets/a64208d1-fe44-4925-bccd-e43b82e6deb3" />

---

## Step 2: Check Limits of a Running Process

Find the PID:

```bash
pgrep -f jenkins
```

Then:

```bash
cat /proc/<PID>/limits
```

Example:

```bash
cat /proc/1234/limits
```

<img width="1859" height="332" alt="screen17" src="https://github.com/user-attachments/assets/e3863141-2a18-41f6-bfe8-0caa9833c76f" />

Look for:

```text
Max open files            65535                65535                files
Max processes             16384                16384                processes
```


This is more reliable for troubleshooting than checking only the current interactive shell.

---

## Step 3: Configure Limits for systemd Services

For services managed by systemd, configure service-level limits rather than relying only on `/etc/security/limits.conf`.

Create an override:

```bash
sudo systemctl edit <service-name>
```

Example:

```bash
sudo systemctl edit jenkins
```

Add:

```ini
[Service]
LimitNOFILE=65535
LimitNPROC=16384
```

Save the configuration.

---

## Step 4: Reload systemd

```bash
sudo systemctl daemon-reload
```

Restart the service:

```bash
sudo systemctl restart <service-name>
```

Check status:

```bash
sudo systemctl status <service-name>
```

---

## Step 5: Verify systemd Limits

```bash
systemctl show <service-name> | grep -E 'LimitNOFILE|LimitNPROC'
```

Example:

<img width="1859" height="105" alt="screen18" src="https://github.com/user-attachments/assets/4535b25a-c289-4e52-bc99-44f800ff58e7" />

Then verify the actual process:

```bash
PID=$(systemctl show -p MainPID --value <service-name>)
cat /proc/$PID/limits
```

<img width="1859" height="356" alt="screen19" src="https://github.com/user-attachments/assets/24a8f959-651d-4b4d-bc35-f15fa0635a93" />


---

# 7. Validation

### Validate Disk Capacity

```bash
df -h
```

<img width="1859" height="231" alt="screen20" src="https://github.com/user-attachments/assets/5c5242c1-30c8-499d-af76-883e9a282dc7" />


**Expected:**

- Required filesystems are mounted.
- No filesystem is unexpectedly at or near 100%.
- Required mount points are present.

### Validate Mount Points

```bash
lsblk -f
findmnt
```

<img width="1859" height="914" alt="screen21" src="https://github.com/user-attachments/assets/74289d8b-d95d-4662-b27f-f65958280d40" />
<img width="1859" height="914" alt="screen22" src="https://github.com/user-attachments/assets/a36008a6-f1b0-45e6-bd64-3c8e1bf4f652" />


**Expected:**

- Required partitions have the expected filesystem.
- Required partitions are mounted at the expected locations.

### Validate Inodes

```bash
df -i
```

<img width="1859" height="231" alt="screen23" src="https://github.com/user-attachments/assets/76947a28-69cb-4f91-9c7f-312df87dde56" />


**Expected:**

- Inode usage is within the application's operational threshold.

### Validate User Limits

Log in as the target user and run:

```bash
ulimit -a
ulimit -n
ulimit -u
```

<img width="1859" height="231" alt="screen23" src="https://github.com/user-attachments/assets/a429b052-bf16-40a8-b3d7-921afbed28ee" />

### Validate Process Limits

```bash
cat /proc/<PID>/limits
```

<img width="1859" height="373" alt="screen25" src="https://github.com/user-attachments/assets/a0ec986e-1231-4dbc-90e1-46048cc7dfee" />


**Expected:**

The running process has the intended `Max open files` and `Max processes` values.

### Final Validation Checklist

| **Validation** | **Expected Result** |
| -------------- | ------------------- |
| Disk usage | Filesystems have sufficient free space |
| Mount points | Required disks are mounted correctly |
| Inodes | Inode utilization is within acceptable limits |
| Large files | Unexpected large files are identified |
| User `ulimit` | Required limits are configured |
| Process limits | Application processes have required limits |
| systemd limits | Service-level limits are correctly applied |
| Persistence | Configuration survives logout/reboot where required |

---

# 8. Use Cases

| **Scenario** | **Commands / Actions** |
| ------------ | ---------------------- |
| Disk is almost full | `df -h`, `du -xh`, `find` |
| Identify mounted disks | `lsblk -f`, `findmnt` |
| Identify inode exhaustion | `df -i` |
| Find deleted files consuming space | `sudo lsof +L1` |
| Application reports too many open files | Check `ulimit -n` and `/proc/<PID>/limits` |
| Application cannot create more processes | Check `ulimit -u` and process limits |
| Configure persistent user limits | `/etc/security/limits.d/*.conf` |
| Configure limits for systemd service | `systemctl edit <service>` |

---

# 9. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| --------- | --------- | ------------ |
| Disk usage is 100% | Filesystem has no free space | Use `du`, `find`, and `lsof +L1` to identify space consumers |
| Disk shows free space but files cannot be created | Inodes may be exhausted | Run `df -i` and remove unnecessary small files |
| Mounted disk is missing | Mount configuration or filesystem issue | Check `lsblk -f`, `findmnt`, and `/etc/fstab` |
| `ulimit` change disappears after logout | Change was made only in current shell | Configure `/etc/security/limits.d/` or the appropriate service configuration |
| Application still has old `nofile` limit | Existing process was not restarted | Restart the application/service and verify `/proc/<PID>/limits` |
| `/etc/security/limits.conf` has no effect on service | Application is managed by systemd | Configure `LimitNOFILE`/`LimitNPROC` using a systemd override |
| `mount -a` reports an error | Invalid `/etc/fstab` entry or filesystem problem | Review `/etc/fstab`, UUIDs, filesystem type, and mount options |
| Deleted files still consume disk | Process still has deleted file open | Identify the process with `lsof +L1` and restart it if appropriate |

---

# 10. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Monitor disk usage | Establish monitoring and alerts before filesystems reach critical utilization |
| Monitor inode usage | Disk capacity alone does not detect inode exhaustion |
| Use UUIDs in `/etc/fstab` | UUID-based mounting reduces dependency on changing device names |
| Back up configuration | Back up `/etc/fstab` and relevant limits configuration before changes |
| Use `/etc/security/limits.d/` | Keep application-specific user limits separate from the main `limits.conf` |
| Configure systemd services separately | Use systemd `Limit*` settings for systemd-managed applications |
| Validate after changes | Always verify both configuration and the actual running process |
| Avoid excessive limits | Set limits based on application requirements and available system resources |
| Document changes | Record the reason, value, date, and owner for production changes |
| Monitor before increasing limits | Confirm that the limit is actually the bottleneck before increasing it |

---

# 11. Conclusion

This SOP provides a standardized approach to **disk usage, filesystem mount management, user resource limits, and process-level limits** on Linux/Ubuntu systems.

Following these procedures helps administrators maintain **reliability, performance, security, and operational stability** while providing a consistent approach to configuration, validation, and troubleshooting.

---

# 12. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Maqbool Alam | maqbul.alam.snaatak@mygurukulam.co |

---

# 13. References

| **Topic** | **Description** | **Link** |
| --------- | --------------- | -------- |
| Linux `df` | Filesystem disk-space usage | https://man7.org/linux/man-pages/man1/df.1.html |
| Linux `du` | File and directory disk usage | https://man7.org/linux/man-pages/man1/du.1.html |
| Linux `lsblk` | Block-device information | https://man7.org/linux/man-pages/man8/lsblk.8.html |
| Linux `findmnt` | Mounted filesystem information | https://man7.org/linux/man-pages/man8/findmnt.8.html |
| Linux `ulimit` | Shell resource-limit management | https://man7.org/linux/man-pages/man1/ulimit.1p.html |
