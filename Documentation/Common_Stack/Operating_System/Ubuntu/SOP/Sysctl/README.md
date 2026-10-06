#  Ubuntu Sysctl Documentation

<img width="150" height="150" alt="ubuntu-logo" src="https://cdn.simpleicons.org/ubuntu/E95420" />

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Rani Jha | 24-08-2026 | v1.0 | Rani Jha | 05-09-2026 | Ishaan | Anuj Jain | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [Viewing Kernel Parameters](#3-viewing-kernel-parameters)
4. [Applying Kernel Parameter Changes](#4-applying-kernel-parameter-changes)
5. [Persisting Kernel Parameter Changes](#5-persisting-kernel-parameter-changes)
6. [Validation](#6-validation)
7. [Use Cases](#7-use-cases)
8. [Troubleshooting](#8-troubleshooting)
9. [Best Practices](#9-best-practices)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

## 1. Introduction

This document explains the role of sysctl in viewing, applying, and persisting Linux kernel parameter changes on Ubuntu for performance and security tuning.

**sysctl** is a command-line utility used to view and modify Linux kernel parameters at runtime, allowing administrators to tune system behavior such as networking, memory management, and security settings without rebooting the system.

---


# 2. Prerequisites

| **Prerequisite** | **Details** |
| :--- | :--- |
| Operating System | Ubuntu system |
| Access | Terminal or SSH access |
| Required Command | `sysctl` |
| Permissions | `sudo` or root access for changes |
| Configuration | `/etc/sysctl.conf` or `/etc/sysctl.d/` |
| Knowledge | Basic Linux command-line knowledge |

## Check sysctl

```bash
sysctl --version
```

<img width="306" height="137" alt="check systemctl availability" src="https://github.com/user-attachments/assets/56250fae-32d6-4c59-bbb4-0dc436dfad3f" />


## Check sudo access

```bash
sudo -v
```

If the command completes successfully, the user has valid sudo credentials.

---

# 3. Viewing Kernel Parameters

Viewing parameters means checking the current kernel settings without changing them.

## Step 1: View All Kernel Parameters

Run:

```bash
sysctl -a
```
This displays available kernel parameters and their current values.

<img width="1106" height="996" alt="2 All kernal parameters" src="https://github.com/user-attachments/assets/b7d2bd55-ade1-41a6-be0e-48e189504c72" />

## Step 2: View a Specific Parameter

To check one parameter:

```bash
sysctl vm.swappiness
```
<img width="700" height="85" alt="image" src="https://github.com/user-attachments/assets/eb2ce1c1-a0f6-4433-84f3-ad3558b30fbd" />


To check IP forwarding:

```bash
sysctl net.ipv4.ip_forward
```
<img width="702" height="257" alt="3  specific kernal parameter" src="https://github.com/user-attachments/assets/34642e7f-7df8-4d6f-8180-b8fcd1e1113c" />

## Step 3: Read a Parameter from `/proc/sys`

Kernel parameters can also be read directly from `/proc/sys`.

Example:

```bash
cat /proc/sys/vm/swappiness
```

<img width="871" height="257" alt="4  Read kernal parameter" src="https://github.com/user-attachments/assets/bae92b74-ac4e-4b72-b337-9143553fd610" />

---

# 4. Applying Kernel Parameter Changes

Applying a parameter means changing its current value.

## Step 1: Change a Parameter Temporarily

Use `sysctl -w` to change a parameter at runtime.

Example:

```bash
sudo sysctl -w vm.swappiness=10
```
<img width="461" height="120" alt="5  change kernal parameter" src="https://github.com/user-attachments/assets/3d3cc00c-572e-44ee-b0f5-808f48a8481b" />

The new value is applied immediately.

## Step 2: Change a Networking Parameter

For example, to enable IPv4 forwarding:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Verify:

```bash
sysctl net.ipv4.ip_forward
```
<img width="497" height="120" alt="6  Apply network parameter" src="https://github.com/user-attachments/assets/f87abac0-3868-45c6-a100-a74250ee6af2" />

---

# 5. Persisting Kernel Parameter Changes

Persisting a parameter means saving the change so that it remains active after a system reboot.

## Step 1: Back Up the Configuration

Before changing `/etc/sysctl.conf`, create a backup:

```bash
sudo cp /etc/sysctl.conf /etc/sysctl.conf.bak
```
Verify:
```bash
ls -l /etc/sysctl.conf*
```
<img width="588" height="215" alt="7  before chnages creating a backup" src="https://github.com/user-attachments/assets/70711b68-d7b0-4218-a84a-abf84f4055c3" />


## Step 2: Edit `/etc/sysctl.conf`

Open the file:

```bash
sudo nano /etc/sysctl.conf
```
Add the required settings.


## Step 3: Apply `/etc/sysctl.conf`

Run:

```bash
sudo sysctl -p
```

This loads the settings from `/etc/sysctl.conf`.


## Step 4: Verify the Persistent Configuration

Check the file:

```bash
cat /etc/sysctl.d/99-custom.conf
```

Then check the active values:

```bash
sysctl vm.swappiness
sysctl net.ipv4.ip_forward
```


# 6. Validation

Validation confirms that the required kernel parameter changes were applied correctly.

```

## Validate IP Forwarding

```bash
sysctl net.ipv4.ip_forward

```

## Validate Configuration

For `/etc/sysctl.conf`:

```bash
grep -v '^#' /etc/sysctl.conf | grep -v '^$'

```
<img width="1001" height="340" alt="8 validation" src="https://github.com/user-attachments/assets/5c96acef-20cf-49d0-b516-cd2a3ba63ada" />

# 7. Use Cases

| **Scenario** | **Commands / Actions** |
| :--- | :--- |
| View all kernel parameters | `sysctl -a` |
| Check a specific parameter | `sysctl <parameter>` |
| Change a parameter temporarily | `sudo sysctl -w <parameter>=<value>` |

---

# 8. Troubleshooting

| **Issue** | **Possible Cause** | **Solution** |
| :--- | :--- | :--- |
| Permission denied | User does not have required privileges | Use `sudo` or root access |
| Change disappears after reboot | Change was only applied at runtime | Save it in `/etc/sysctl.conf` or `/etc/sysctl.d/` |
| `sysctl -p` shows an error | Invalid configuration or unsupported parameter | Check the parameter and configuration syntax |

---

# 9. Best Practices

| **Best Practice** | **Description** |
| :--- | :--- |
| Check before changing | Always check the current value before modifying a parameter. |
| Take a backup | Back up configuration files before making changes. |
| Test first | Test runtime changes before making them persistent. |
| Use suitable values | Select values based on system and application requirements. |
| Use custom configuration | Keep custom settings organized under `/etc/sysctl.d/` where appropriate. |

---

# 10. Conclusion

This documentation helped in understanding how sysctl is used to view, apply, and persist kernel parameter changes in Ubuntu. It provides a quick reference for managing kernel settings effectively for system performance, security, and stability.

---

# 11. Contact Information

| **Name** | **Email** |
| :--- | :--- |
| Rani Kumari | [rani.kumari.snaatak@mygurukulam.co](mailto:rani.kumari.snaatak@mygurukulam.co) |

---

# 12. References

| **Topic**            | **Link**                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| **systemctl Manual** | [systemctl Documentation](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html) |
| **systemd Manual**   | [systemd Documentation](https://www.freedesktop.org/software/systemd/man/latest/systemd.html)     |

---

