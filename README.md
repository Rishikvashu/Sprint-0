## Common Stack | Operating System | Ubuntu | Services

<p align="center">
  <img width="550" alt="Ubuntu Icon" src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Ubuntu_logo_orange.png?utm_source=commons.wikimedia.org&utm_campaign=index&utm_content=original" />
</p>


---

##  Author Table

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Arjun | 24-08-2026 | v1.1    | Arjun           | 24-08-2026     |       Team      |      Rajnish sharma      | Pritam/Komal           |     Abhsihek/Manish Nautiyal       |

---


## Table of Contents

1. [Purpose](#1-purpose)
2. [What is systemctl?](#2-what-is-systemctl)
3. [Core systemctl Commands](#3-core-systemctl-commands)
   - [3.1 Start a Service](#31-start-a-service)
   - [3.2 Stop a Service](#32-stop-a-service)
   - [3.3 Restart a Service](#33-restart-a-service)
   - [3.4 Enable a Service](#34-enable-a-service)
   - [3.5 Disable a Service](#35-disable-a-service)
4. [Checking Service Status](#4-checking-service-status)
5. [Viewing Service Logs with journalctl](#5-viewing-service-logs-with-journalctl)
6. [Quick Reference](#6-quick-reference)
7. [Conclusion](#7-conclusion)

---

## 1. Purpose

This SOP explains how to manage Linux system services using the `systemctl` command. It is written for team members who are comfortable with basic Linux commands and want to learn how to start, stop, enable, disable, and check the status of services.

By the end of this document, you will be able to:

- Understand what `systemctl` is and when to use it
- Start and stop services immediately
- Enable and disable services so they persist across reboots
- Check the live status and logs of any service
- Troubleshoot services that fail to start or stop

> **  Note:** All commands are tested on Ubuntu 22.04 LTS.

---

## 2. What is systemctl?

`systemctl` is the main command-line tool for managing services on modern Linux systems that use **systemd** as their init system. It lets you control whether a service is running right now and whether it starts automatically when the server boots.

Some common things people use `systemctl` for:

- Starting a service manually after deploying a new version
- Stopping a service before making configuration changes
- Enabling a service so it auto-starts after every reboot
- Checking whether a service crashed and reading why
- Restarting services as part of deployment scripts

> **  Tip:** Think of `systemctl` as the remote control for every background process on your Linux server.

---

## 3. Core systemctl Commands

The basic syntax for all `systemctl` commands is:

```bash
sudo systemctl <action> <service-name>
```

---

## 3.1 Start a Service

Use this to immediately start a service that is currently stopped. This does **not** change whether it auto-starts on reboot.


### Start a service
```bash
sudo systemctl start nginx
```

<img width="808" height="495" alt="start" src="https://github.com/user-attachments/assets/41b998e7-4e59-461a-ad22-a06e15acec45" />


## 3.2 Stop a Service

Use this to immediately stop a running service. This does **not** prevent it from starting again on the next reboot.

## Stop a service
```bash
sudo systemctl stop nginx
```

<img width="808" height="364" alt="stop" src="https://github.com/user-attachments/assets/b727d87e-82c5-4753-b408-52babc01f666" />

## 3.3 Restart a Service

Restart stops and then starts a service in one step. Use this after changing a config file.

### Restart a service (stop + start)
```bash
sudo systemctl restart nginx
```
<img width="808" height="476" alt="restart" src="https://github.com/user-attachments/assets/44ffc73c-1485-4911-84ea-2108659fed2f" />


---

## 3.4 Enable a Service

Enabling a service creates a symlink so that systemd starts it automatically the next time the server boots. It does **not** start the service right now.

### Enable a service to start at boot
```bash
sudo systemctl enable nginx
```

### Enable and start in one command
```bash
sudo systemctl enable --now nginx
```

---

## 3.5 Disable a Service

Disabling removes the boot-time symlink, so the service will **not** start automatically on reboot. It does not stop the currently running service.

### Disable a service from starting at boot
```bash
sudo systemctl disable nginx
```
### Disable and stop in one command
```bash
sudo systemctl disable --now nginx
```
<img width="808" height="476" alt="disable" src="https://github.com/user-attachments/assets/29607e99-f24a-4a87-969a-67e3cf49d3f5" />



---

## 4. Checking Service Status

The `status` command is the single most useful `systemctl` command. It tells you whether a service is running, how long it has been running, and shows its recent log output all at once.
```bash
sudo systemctl status nginx
```
<img width="808" height="476" alt="status" src="https://github.com/user-attachments/assets/5fd6d304-3430-4998-86fc-7b5484450964" />


---

**Example output:**

```
● nginx.service - A high performance web server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled)
   Active: active (running) since Mon 2026-04-13 09:00:01 UTC
  Process: 1234 ExecStart=/usr/sbin/nginx
 Main PID: 1235 (nginx)
```

**Key things to look for in the output:**

| Field | What to Look For |
|-------|-----------------|
| `Active: active (running)` | Service is healthy and running |
| `Active: inactive (dead)` | Service is stopped — not running |
| `Active: failed` | Service crashed — check the logs below |
| `Loaded: ... enabled` | Service will start on next reboot |
| `Loaded: ... disabled` | Service will NOT start on next reboot |

---

## 5. Viewing Service Logs with journalctl

When a service fails or behaves unexpectedly, `journalctl` lets you read its detailed logs. Unlike reading raw log files, `journalctl` is structured and filterable.


### Show last 50 lines of logs for a service
```bash
journalctl -u nginx -n 50
```


### Watch logs live as they appear
```bash
journalctl -u nginx -f
```


### Logs from the last hour only
```bash
journalctl -u nginx --since '1 hour ago'
```


### Show only error messages
```bash
journalctl -u nginx -p err
```
---

## 6. Quick Reference

| Command | What it Does |
|---------|-------------|
| `sudo systemctl start <service>` | Start the service immediately |
| `sudo systemctl stop <service>` | Stop the service immediately |
| `sudo systemctl restart <service>` | Stop then start the service |
| `sudo systemctl reload <service>` | Reload config without stopping (if supported) |
| `sudo systemctl enable <service>` | Auto-start at boot (does not start now) |
| `sudo systemctl disable <service>` | Remove auto-start at boot (does not stop now) |
| `sudo systemctl enable --now <service>` | Enable AND start in one command |
| `sudo systemctl disable --now <service>` | Disable AND stop in one command |
| `sudo systemctl status <service>` | Show status, PID, uptime, and recent logs |
| `journalctl -u <service> -n 50` | Show last 50 log lines for a service |
| `journalctl -u <service> -f` | Watch service logs in real time |
| `sudo systemctl list-units --type=service` | List all active services |
| `sudo systemctl daemon-reload` | Reload systemd after editing a unit file |

---

## 7. Conclusion

`systemctl` is the standard way to manage services on any modern Ubuntu or RHEL-based Linux server. Once you understand the difference between `start`/`stop` (immediate) and `enable`/`disable` (boot-time), you will be able to confidently manage the full lifecycle of any service.

**Key things to remember:**

- Use `start` and `stop` to control services immediately
- Use `enable` and `disable` to control what happens after a reboot
- Use `enable --now` and `disable --now` to do both at once
- Always run `systemctl status` after making changes to confirm the result
- Always begin troubleshooting with journalctl -u <service> -n 50 to identify the root cause quickly.



## Contact Information

| Name           | Email ID |
|----------------|----------|
| Arjun Kumar  | arjun.kumar.snaatak@mygurukulam.co |



---
## Reference
| Resource | Where to Find It |
|----------|-----------------|
| systemd Documentation | `man systemctl` (run in terminal) |
| OT-Microservices Repository | https://github.com/OT-MICROSERVICES |


---
