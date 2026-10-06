# Logrotate Documentation

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Priyanshu | 25-08-2026 | 1.1 | Priyanshu | 27-08-2026 | Aryan Mishra |  |  |


---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Logrotate](#2-what-is-logrotate)
3. [Why Logrotate is Required](#3-why-logrotate-is-required)
4. [Logrotate Workflow](#4-logrotate-workflow)
   - [4.1 Workflow Diagram](#41-workflow-diagram)
5. [Logrotate Configuration](#5-logrotate-configuration)
6. [Different Strategies for Log Rotation](#6-different-strategies-for-log-rotation)
7. [Strategies Comparison](#7-strategies-comparison)
8. [Advantages and Disadvantages](#8-advantages-and-disadvantages)
9. [Best Practices](#9-best-practices)
10. [Troubleshooting](#10-troubleshooting)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

This document provides a structured guide to configuring and managing log rotation using logrotate on Ubuntu. It explains what logrotate is, why log management is essential for system stability, and provides a step-by-step guide for configuring rotation frequencies, retention policies, and automated execution. The primary goal of this document is to help understand automate log cleanup, prevent disk space exhaustion, and establish a standardized, reliable logging workflow.

---

# 2. What is Logrotate

logrotate is a Linux utility that manages the automatic rotation, compression, and eventual deletion of log files. It works by reading a global configuration file (`/etc/logrotate.conf`) together with any number of per-application drop-in files under `/etc/logrotate.d/`, each defining how a given set of log files should be handled:

- **How often** to rotate (`daily`, `weekly`, `monthly`, or by `size`/`maxsize`).
- **How many** rotated copies to keep (`rotate N`).
- **Whether to compress** rotated copies (`compress`, optionally with `delaycompress`).
- **What to run immediately after rotation** (a `postrotate` / `endscript` block, e.g. to signal an application to reopen its log handle).

---

# 3. Why Logrotate is Required

- Prevents **disk exhaustion** caused by unbounded log growth, which can otherwise degrade or crash services and hosts.
- Provides a **standardized procedure** for defining rotation frequency (daily/weekly/monthly/size-based) across application and system logs.
- Enforces **retention** policies, keeping only as many rotated copies as needed before automatic deletion.
- Reduces disk usage through **compression** of rotated log files.
- Improves **system stability, reliability, performance, and operational consistency** by removing the need for manual log cleanup.

---

# 4. Logrotate Workflow

The end-to-end workflow for enabling and operating log rotation on an Ubuntu host follows a repeatable path from initial setup through ongoing, automated execution:

## 4.1 Workflow Diagram

<details>

<summary>Click to Expand Workflow Diagram</summary>

<img width="1058" height="1077" alt="image" src="https://github.com/user-attachments/assets/0ae8536b-d28a-4d3b-ba00-50b386bbced2" />


</details>


### Explanation

1. **Check Installation** : Verify if the logrotate binary exists on the system before proceeding with deployment.
2. **Install Package** : Install the logrotate binary on the host, which automatically provisions and enables the systemd execution timer on modern Ubuntu systems.
3. **Review Global Defaults** : Review standard baseline settings such as weekly schedules and standard retention limits that application rules inherit unless overridden.
4. **Configure Application** : Create dedicated per-application configuration drop-in files to define custom rotation schedules, file retention limits, compression options, target file permissions, and post-rotation reload actions.
5. **Automate via Systemd** : Enable continuous daily automated background execution, ensuring any missed runs trigger immediately following a system reboot.
6. **Test (Force Run)** : Perform an immediate force rotation cycle to confirm file generation, compression, and post-rotation process signaling without waiting for the scheduled timer.



---

# 5. Logrotate Configuration

The example below shows a typical per-application drop-in file placed at `/etc/logrotate.d/myapp`, demonstrating how rotation frequency, retention, compression, permissions, and a post-rotation hook are declared together:

```
/var/log/myapp/*.log {
    daily
    rotate 14
    maxsize 100M
    compress
    delaycompress
    missingok
    notifempty
    dateext
    dateformat -%Y-%m-%d
    create 0640 myapp myapp
    sharedscripts
    postrotate
        systemctl reload myapp.service > /dev/null 2>&1 || true
    endscript
}
```

logrotate operates using a hierarchical configuration structure to maintain flexibility and organization across system and application components:

- **Global Configuration (`/etc/logrotate.conf`):** Defines global default parameters (such as overall rotation frequency, default retention count, and default log file creation settings).
- **Drop-in Directory (`/etc/logrotate.d/`):** Contains application-specific configuration files (e.g., `/etc/logrotate.d/nginx`, `/etc/logrotate.d/rsyslog`). Rules specified inside drop-in files take precedence over global settings in `/etc/logrotate.conf`.


---

# 6. Different Strategies for Log Rotation

| **Strategies** | **Description** |
| -------- | --------------- |
| `logrotate` | Standard Linux utility for rotating, compressing, and pruning plain-text log files via a global config plus per-application drop-in files. |
| `systemd-journald` | Systemd's own logging service; manages retention/rotation of its binary journal via `SystemMaxUse`/`RuntimeMaxUse` settings and `journalctl --vacuum-*` commands rather than plain text files. |
| `rotatelogs` | Piped-logging tool bundled with Apache HTTP Server; rotates logs by time interval or size as the web server writes to them, without needing a separate scheduler. |
| `cronolog` | Standalone tool that writes web/application server output directly into timestamped filenames using `strftime`-style templates, rotating as it writes. |

---

# 7. Strategies Comparison

| **Strategies** | **Main Purpose** | **Speed** | **Ease of Use** | **Best Use Case** |
| -------- | ---------------- | --------- | --------------- | ------------------ |
| `logrotate` | General-purpose rotation, compression, and retention for any text log file | Fast — lightweight, runs via `systemd` timer/cron | Easy — declarative config files | System-wide and per-application log management on Linux servers |
| `systemd-journald` | Rotation/retention for the systemd journal (binary logs) | Fast — built into systemd | Easy for journal logs; not applicable to plain text files | Systems that centralize logging through journald/systemd |
| `rotatelogs` | Rotates logs as Apache writes them | Fast — piped directly from `httpd` | Moderate — configured per Apache vhost, Apache-specific | Apache HTTP Server access/error logs |
| `cronolog` | Writes output directly into rotated, timestamped files | Fast — piped output | Moderate — requires `strftime` template knowledge | Web/app servers that pipe stdout directly to a log writer |

---

# 8. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| -------------- | ------------------ |
| Prevents disk exhaustion from unbounded log growth via scheduled rotation and retention | Combining `size` and time-based directives is a common misconfiguration that silently disables the intended schedule |
| Natively packaged for Ubuntu and integrated with `systemd` timers out of the box | Forcing rotation repeatedly within the same day can collide when `dateext` is combined with a date-only suffix |
| Highly configurable per application via drop-in files under `/etc/logrotate.d/`, without touching the global config | Only rotates plain-text log files — does not manage binary/structured logs such as the systemd journal |
| Supports gzip compression and custom `postrotate` hooks to reload applications cleanly | Requires careful tuning of `create`/`postrotate` per application to avoid breaking processes with open file descriptors |

---

# 9. Best Practices


1. Place application-specific configurations under `/etc/logrotate.d/` rather than modifying `/etc/logrotate.conf` to keep updates clean and maintainable.
2. Test configuration changes using the dry-run command (`logrotate -d`) to detect syntax errors and verify execution logic before deploying to production.
3. Use `maxsize` when combining size limits with time schedules (`daily`/`weekly`), as `size` completely overrides time-based schedules.
4. Apply `delaycompress` on active log files to defer compression by one cycle, preventing truncated data while processes maintain open file descriptors.
5. Define retention counts (`rotate N`) based on log volume and operational importance, assigning shorter retention to high-volume debug logs and longer retention to critical audit logs.

---

# 10. Troubleshooting

| **Symptom** | **Likely Cause** | **Resolution** |
| ----------- | ------------------ | -------------- |
| Log rotates but the application keeps writing to the old (now-rotated) file | No `postrotate`/signal step, or the app doesn't support reopening its log handle | Add a `postrotate` block that sends `HUP`/reload to the process, or use `copytruncate` if the app cannot reopen file handles. |
| Rotation runs at unexpected times or not at all | `size`/`maxsize` and time directives (`daily`/`weekly`) were mixed without understanding precedence | Recall that `size` overrides schedule-based directives entirely; use `maxsize` instead if you want both a fixed schedule and an early-rotation safety net. |
| Rotation didn't run while the host was powered off | `logrotate.timer` missed its scheduled window | Confirm `Persistent=true` is set on the timer (`systemctl cat logrotate.timer`) so the missed run executes on next boot. |
| Forced rotation with `-f` works but the scheduled timer never rotates | `logrotate.timer`/`.service` disabled or masked | Check `systemctl status logrotate.timer` and `systemctl list-timers | grep logrotate` to confirm the timer is enabled and active. |
| Duplicate rotated files pile up with clashing names | `dateext` combined with a date-only suffix, then forced multiple times in one day | Use a `dateformat` that includes finer granularity (e.g. hour) if forcing rotation more than once per day, or avoid repeated same-day forces in production. |

---

# 11. Conclusion

`logrotate` is recommended as the standard log-management tool for Ubuntu hosts in this stack. It ships natively in the Ubuntu package repositories, integrates directly with `systemd` timers (no extra agent required), and its per-application config model under `/etc/logrotate.d/` scales cleanly across services without touching shared global settings.


---

# 12. Contact Information

| **Name** | **Team** | **Email** |
| -------- | --------- | --------- |
| Priyanshu | Kubeclan | [priyanshu.banwala.snaatak@mygurukulam.co](mailto:priyanshu.banwala.snaatak@mygurukulam.co) |

---

# 13. References

| **Description** | **Topic** |
| --------- | --------------- |
| Official manual page covering all logrotate directives and command-line options. | [logrotate(8) man page](https://linux.die.net/man/8/logrotate) |
| Upstream source, release notes, and issue tracker for logrotate. | [logrotate GitHub repository](https://github.com/logrotate/logrotate) |
| Ubuntu-specific server administration documentation. | [Ubuntu Server Documentation](https://ubuntu.com/server/docs) |
| Reference for `logrotate.timer`/`systemd` unit inspection commands used in troubleshooting. | [systemd.timer(5) man page](https://www.freedesktop.org/software/systemd/man/systemd.timer.html) |

---
