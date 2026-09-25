# Linux Cron Job SOP

---

## Author Table

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Palak Upadhyay | 26-08-2026 | 1.0 | Palak Upadhyay | 31-08-2026 | Aryan Mishra | Aditya raj singh | Abhishek/Manish |
| Palak Upadhyay | 26-08-2026 | 1.1 | Palak Upadhyay | 12-09-2026 | Aryan Mishra | Aditya raj singh | - |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Cron](#2-what-is-cron)
3. [Why Use Cron](#3-why-use-cron)
4. [Features of Cron](#4-features-of-cron)
5. [Types of Cron Jobs](#5-types-of-cron-jobs)
6. [How Cron Works](#6-how-cron-works)
7. [Prerequisites](#7-prerequisites)
8. [How to Create a Cron Job](#8-how-to-create-a-cron-job)
9. [How to Manage Cron Jobs](#9-how-to-manage-cron-jobs)
10. [How to Check Logs](#10-how-to-check-logs)
11. [Troubleshooting Cron Jobs](#11-troubleshooting-cron-jobs)
12. [Cron Syntax Reference](#12-cron-syntax-reference)
13. [Best Practices for DevOps](#13-best-practices-for-devops)
14. [Conclusion](#14-conclusion)
15. [Contact Information](#15-contact-information)
16. [References](#16-references)

---

## 1. Introduction

This SOP guides automated task scheduling using Cron on Linux/Ubuntu servers. It covers job creation, monitoring, and troubleshooting.

These standard procedures ensure reliable job execution and help prevent silent failures.


---

## 2. What is Cron

Cron is a time-based job scheduler in Linux that automatically runs commands or scripts at a set time or interval.

It runs in the background using the `crond` service and does not need manual intervention.


---

## 3. Why Use Cron

Cron is used to automate regular tasks like backups, system updates, log cleanup, and server checks.

It saves time, reduces manual work and errors, and ensures tasks run automatically at the required time. It can also schedule heavy tasks during low-traffic hours.



---

## 4. Prerequisites

| Prerequisite | Minimum Requirement |
| :--- | :--- |
| **Operating System** | Ubuntu  / Linux server with terminal access. |
| **Privileges** | Standard user account; `sudo` rights for system-level configurations. |
| **Active Service** | Cron daemon service (`cron`) installed and active (`systemctl status cron`). |
| **Target Script** | Tested executable command or script with execution permissions (`chmod +x`). |

## 5. Features of Cron

| Feature | Description |
| :--- | :--- |
| **Granular Time Scheduling** | Supports precise scheduling across minute, hour, day of the month, month, and day of the week. |
| **Daemon-Driven Automation** | Runs autonomously in the background via the `cron` daemon without needing user login sessions. |
| **Multi-User Isolation** | Provides isolated user crontabs alongside system-wide crontabs for administrative automation. |
| **Automated Output Redirection** | Easily redirects execution output, stdout, and error streams directly to custom log files. |
| **Lightweight and Native** | Built directly into Linux distributions with zero external runtime or framework dependencies. |

---

## 6. Types of Cron Jobs

| Type | Managed Via | Scope & Permissions | Config Location |
| :--- | :--- | :--- | :--- |
| **User-Level** | `crontab -e` | Runs under individual user privileges without root access. | `/var/spool/cron/crontabs/<user>` |
| **System-Level** | `/etc/cron.d/` or `/etc/crontab` | System-wide automation running under specified user (e.g., `root`). | `/etc/crontab`, `/etc/cron.d/` |

---

## 7. How Cron Works

<img width="1120" height="520" alt="cron_workflow_diagram" src="https://github.com/user-attachments/assets/17d648d6-d913-48a3-89e8-41dd590df4ab" />


---

## 8. How to Create a Cron Job

### Comparison: User-Level vs System-Level

| Feature | User-Level (`crontab -e`) | System-Level (`/etc/cron.d/`) |
| :--- | :--- | :--- |
| **Execution User** | Implicitly runs as logged-in user (`palak`). | Explicit user declaration required (e.g., `root`). |
| **Syntax** | `* * * * * <command>` | `* * * * * <username> <command>` |
| **Config Location** | `/var/spool/cron/crontabs/` | `/etc/cron.d/` |
| **Log Output** | `~/cron_test.log` | `/var/log/system_cron.log` |

---

### Part A: User-Level Cron Job

1. **Open crontab editor for the current user:**
   ```bash
   crontab -e
   ```

2. **Add the scheduled test task:**
   ```text
   * * * * * echo "User job at: $(date)" >> ~/cron_test.log 2>&1
   ```

3. **Save and exit the editor (`Ctrl+O`, `Enter`, `Ctrl+X`).**

4. **Verify the log output after 2 minutes:**
   ```bash
   cat ~/cron_test.log
   ```

---

### Part B: System-Level Cron Job

1. **Create a system cron file in `/etc/cron.d/`:**
   ```bash
   sudo nano /etc/cron.d/system-test-cron
   ```

2. **Add the schedule with explicit user declaration (`root`):**
   ```text
   * * * * * root echo "System job executed at: $(date)" >> /var/log/system_cron.log 2>&1
   ```

3. **Save and exit the editor (`Ctrl+O`, `Enter`, `Ctrl+X`).**

4. **Verify system log output after 2 minutes:**
   ```bash
   sudo cat /var/log/system_cron.log
   ```

---

### Part C: Pre-Configured Periodic Directories

For standard recurring intervals, place executable scripts directly into system cron folders:

```bash
sudo cp cleanup.sh /etc/cron.daily/
sudo chmod +x /etc/cron.daily/cleanup.sh
```

| Directory | Execution Schedule |
| :--- | :--- |
| `/etc/cron.hourly/` | Runs once every hour. |
| `/etc/cron.daily/` | Runs once every day at system off-peak time. |
| `/etc/cron.weekly/` | Runs once per week. |
| `/etc/cron.monthly/` | Runs once on the first day of each month. |

---

## 9. How to Manage Cron Jobs

| Action | Command | Purpose |
| :--- | :--- | :--- |
| **List Active Jobs** | `crontab -l` | Displays all configured cron jobs for current user. |
| **Delete All Jobs** | `crontab -r` | Removes the current user's entire crontab file. |
| **Verify Deletion** | `crontab -l` | Confirms output: `no crontab for user`. |

---

## 10. How to Check Logs

1. **Static Log View:** Inspect historical execution entries from user log:
   ```bash
   cat ~/cron_test.log
   ```

2. **Live Log Stream:** Monitor real-time task execution output (`Ctrl+C` to exit):
   ```bash
   tail -f ~/cron_test.log
   ```

3. **Daemon Syslog Audit:** Verify system daemon triggers and execution status:
   ```bash
   sudo grep CRON /var/log/syslog | tail -n 10
   ```

---

## 11. Troubleshooting Cron Jobs

| Issue | Cause | Fix |
| :--- | :--- | :--- |
| **Cron Service Inactive** | Daemon is stopped. | Run `sudo systemctl restart cron`. |
| **Permission Denied** | Script lacks execution bit. | Run `chmod +x /path/to/script.sh`. |
| **Command Not Found** | Minimal shell path in cron. | Use absolute paths (e.g., `/usr/bin/python3`). |
| **Silent Job Failure** | Errors not redirected. | Append `>> /path/to/log 2>&1` to command line. |
| **Environment Mismatch** | Missing shell variables. | Test in clean shell: `env -i /path/to/script.sh`. |

---

## 12. Cron Syntax Reference

```text
*  *  *  *  *   <command-to-execute>
│  │  │  │  │
│  │  │  │  └─── Day of Week (0 - 6, 0 = Sunday)
│  │  │  └────── Month of Year (1 - 12)
│  │  └───────── Day of Month (1 - 31)
│  └──────────── Hour of Day (0 - 23)
└─────────────── Minute of Hour (0 - 59)
```

| Operator | Syntax | Meaning | Example |
| :--- | :--- | :--- | :--- |
| **`*`** | Asterisk | Every value | `* * * * *` (Every minute) |
| **`,`** | Comma | Value list | `15,45 * * * *` (At minutes 15 and 45) |
| **`-`** | Hyphen | Range | `0 9-17 * * *` (Hourly between 9 AM and 5 PM) |
| **`*/n`** | Slash | Step interval | `*/10 * * * *` (Every 10 minutes) |

---

## 13. Best Practices for DevOps

* Avoid running cron jobs as the root user; use dedicated service accounts to adhere to the principle of least privilege.
* Always specify absolute paths for all commands, scripts, interpreters, and configuration files.
* Use file locking utilities like `flock` to prevent concurrent or overlapping execution of long-running scheduled tasks.
* Explicitly redirect both standard output and standard error (`>> /path/to/log 2>&1`) to prevent silent failures.
* Verify system timezone configurations using `timedatectl` to ensure cron jobs execute at the expected local time.

---

## 14. Conclusion

This SOP standardizes automated job scheduling and log monitoring across Linux environments using the native Cron daemon.
By enforcing absolute binary paths, explicit stream redirection (`2>&1`), and least-privilege service accounts, operational risks and silent job failures are eliminated.
Following these structured procedures ensures reliable, consistent, and maintainable background automation across all production and development workflows.

---

## 15. Contact Information

| Name | Email Address |
| :--- | :--- |
| Palak Upadhyay | [palak.upadhyay.snaatak@opstree.com](mailto:palak.upadhyay.snaatak@opstree.com) |

---

## 16. References

| Description | Reference Link |
| :--- | :--- |
| Online cron schedule expression tester and editor | [Crontab Guru](https://crontab.guru/) |
| Official Ubuntu community documentation for cron service | [Ubuntu Cron Guide](https://help.ubuntu.com/community/CronHowto) |
| Linux manual page for the cron background daemon | [Linux Cron Manual](https://man7.org/linux/man-pages/man8/cron.8.html) |
