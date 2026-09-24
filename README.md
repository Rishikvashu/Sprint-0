# COMMON STACK | Operating System | Ubuntu | Concepts


<p align="center">
  <img width="150" alt="Ubuntu Icon" src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Ubuntu_logo_orange.png?utm_source=commons.wikimedia.org&utm_campaign=index&utm_content=original" />
</p>

---

# Author Table

| **Author**    | **Created On** | **Version**  | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ------------- | -------------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Anshul kotiya | 24-08-2026     | 1.2 | 16-09-2026         |  Shubham Rathi  |  Shreya/Nikita  | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ubuntu](#2-what-is-ubuntu)

   * [2.1 What is Operating System](#21-what-is-operating-system)
   * [2.2 What is Linux](#22-what-is-linux)
   * [2.3 How Ubuntu Works](#23-how-ubuntu-works)
3. [Why Ubuntu is Required](#3-why-ubuntu-is-required)
4. [Ubuntu Concepts Workflow](#4-ubuntu-concepts-workflow)
5. [Software Management](#5-software-management)
   * [5.1 Package Manager](#51-package-manager)
   * [5.1.1 APT (Advanced Package Tool)](#511-apt-advanced-package-tool)
   * [5.1.2 dpkg](#512-dpkg)
  
6. [Service Management](#6-service-management)

   * [6.1 What is a Service?](#61-what-is-a-service)
   * [6.2 What is systemd?](#62-what-is-systemd)
   * [6.3 What is systemctl?](#63-what-is-systemctl)
   * [6.4 Service Logs](#64-service-logs)   
7. [Recommendation / Conclusion](#7-recommendation--conclusion)
8. [Contact Information](#8-contact-information)
9. [References](#9-references)

---

# 1. Introduction

This document provides an overview of Ubuntu concepts required for the Project. It explains what an Operating System is, what Ubuntu is, why Ubuntu is required, and the basic concepts of software management and services.

---

# 2. What is ubuntu

Ubuntu is an open-source linux distribution developed and maintained by canonical. 

It provides the Linux kernel along with system utilities, libraries, package management tools, and other components required to operate a complete operating system.

Ubuntu is available in different editions, including Desktop and Server:

- Ubuntu Desktop – Designed for personal computers and laptops, with a graphical user interface for everyday use.
- Ubuntu Server – A lightweight edition without a heavy graphical interface, commonly used for hosting applications, services, APIs, databases, and other server workloads.

## 2.1 what is operating System

An Operating System (OS) is system software that manages the computer's hardware and provides a platform for applications to run.

It acts as an interface between the user, applications, and hardware.

## 2.2 What is Linux

Linux is an open-source operating system kernel. It is the core component that communicates with hardware and manages system resources.

Different operating systems are built around the Linux kernel. These are called Linux distributions.

Examples of Linux distributions include:

- Ubuntu
- Red Hat Enterprise Linux (RHEL)
- CentOS
- Debian

## 2.3 How Ubuntu works

Ubuntu acts as an operating environment between application and the underlying hardware.

The basic working flow is:

     Applications
          ↓
    system Utilities & Libraries      [tools and program which help to manage system ]
          ↓  
    Ubuntu Operating System
          ↓
     Linux Kernel
          ↓
       Hardware

The Linux kernel is responsible for managing hardware and System resource. Ubuntu Provide the utilies and tools that allow users and application to interact with the kernel.
Therefore, Ubuntu provide a complete environment for running application,controlling services and managing system resource.

---

### 3 Why Ubuntu is Required

Ubuntu is required to provide a stable, secure, and manageable Linux-based operating system for application and infrastructure workloads.

| **Reason**              | **Description**                                                                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Software Management** | Provides the `apt` package manager to install, update, upgrade, and remove required software packages.                                      |
| **Service Management**  | Uses `systemd` and `systemctl` to manage application and infrastructure services.                                                           |
| **Server Environment**  | Ubuntu Server provides a lightweight operating environment suitable for servers and cloud instances.                                        |
| **Security**            | Provides regular security updates and system-level security mechanisms.                                                                     |
| **Stability**           | Provides a reliable environment for continuously running applications and services.                                                         |
| **Open Source**         | Ubuntu is open-source, making it suitable for development and server environments without requiring proprietary operating-system licensing. |

---

# 4. Ubuntu Concepts Workflow

Ubuntu provides built-in mechanisms to manage software packages and system services. These mechanisms help administrators install required software, manage dependencies, configure services, and verify the system state.

The overall Ubuntu management workflow can be divided into two major areas:

1. Software Management - Managing software packages and their dependencies.

2. Service Management - Managing the lifecycle of service running on the system.

```
The general workflow is:

Identify Requirement
        ↓
Identify Software/Service
        ↓
Software Management
        ↓
Installation/configuration
        ↓
service Management
        ↓
   Verification
        ↓
Update & Maintenance
```

# 5. Software Management

Software management is the process of installing, updating, upgrading, and removing software on an Ubuntu system.

Ubuntu uses a package management system to make software management easier.

## 5.1 Package Manager

A Package manager is a tool used to install, update, upgrade, and remove software package.

Instead of manually downloading software and finding all the files required to run it, a package manager can find the required package, download it, install it and manage its dependencies.

Ubuntu provide multiple tools for software management.

| **Tool** | **Purpose**                                           |
| -------- | ----------------------------------------------------- |
| APT      | Manages software packages from configured repositoies |
| dpkg     | perform low-level management of .deb packages         |

Ubuntu mainly uses APT for software managemment.

### 5.1.1 APT [Advanced Package Tool]

It is a primary package management tool used in ubuntu to manage software package.

APT allow us to install required software without manually downloading and managing all the files needed by the software.

#### Example :
```
sudo apt update 
sudo apt install nginx
```
### Commom APT Operation

| **command**      | **Description**                            |
| ---------------- | ------------------------------------------ |
| sudo apt update  | update information about available package |
| sudo apt install | Install a software package                 |
| sudo apt upgrade | upgrades installed packages                |
| sudo apt remove  | removes a software package                 |

### 5.1.2 dpkg

- 'dpkg' is low-level package management tool used by Debian-based distributions, including ubuntu.
- It is used to install, remove, inspect, and manage individual '.deb' packages.
- Unlike APT, 'dpkg' work directly with a '.deb' package file that is already availabled on the system.

#### Example :
```
sudo dpkg -i nginx-package.deb
```

---

# 6 Service Management:

## 6.1 What is a Service?

A service is a background process that performs a specific task on an Ubuntu system. Services usually run continuously without requiring direct interaction from the user.

Common examples:
- _Nginx_ – Web server
- _SSH_ – Remote server access
- _MySQL_ – Database server
- _Apache_ – Web server

Services can be started, stopped, restarted, and monitored according to system requirements.

On Ubuntu, services are commonly managed using systemd and the systemctl command.

### 6.2 What is systemd?

systemd is the system and service manager used by Ubuntu. It is responsible for initializing the system during boot and managing services and other system processes while the system is running.

It can:

- Start services during system boot.
- Stop and restart services.
- Monitor the state of services.
- Manage service dependencies.
- Start services automatically when configured.
- Collect and manage system logs through journald.


### 6.3 What is systemctl?

`systemctl` is a command-line utility used to communicate with and control the systemd system and service manager.

It allows administrators to manage services without directly interacting with the internal systemd processes.

| **Operation**                   | **systemctl Command**          | **Purpose**                                                              |
| ------------------------------- | ------------------------------ | ------------------------------------------------------------------------ |
| **Start a service**             | `sudo systemctl start nginx`   | Starts the Nginx service.                                                |
| **Stop a service**              | `sudo systemctl stop nginx`    | Stops the Nginx service.                                                 |
| **Restart a service**           | `sudo systemctl restart nginx` | Restarts the Nginx service.                                              |
| **Check service status**        | `sudo systemctl status nginx`  | Displays the current status of the Nginx service.                        |
| **Enable service**              | `sudo systemctl enable nginx`  | Configures Nginx to start automatically at system boot.                  |
| **Disable service**             | `sudo systemctl disable nginx` | Prevents Nginx from starting automatically at system boot.               |
| **Check if service is active**  | `systemctl is-active nginx`    | Checks whether the service is currently running.                         |
| **Check if service is enabled** | `systemctl is-enabled nginx`   | Checks whether the service is configured to start automatically at boot. |




For example, to check the status of the Nginx service:
```
sudo systemctl status nginx
```
Here, systemctl sends the requested operation to systemd, which manages the Nginx service.

_In simple terms:_

| Component | Purpose                         |
| --------- | ------------------------------- |
| systemd   | Manages the system and services |
| systemctl | Command used to control systemd |

### 6.4 Service Logs 

| Topic                        | Command / Step                                  | Description                                                                                                    |
| ---------------------------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **View Service Logs**        | `sudo journalctl -u nginx`                      | Displays logs for the specified service. The `-u` option specifies the service whose logs should be displayed. |
| **View Recent Service Logs** | `sudo journalctl -u nginx --since "1 hour ago"` | Displays logs generated by the service during the last hour.                                                   |


---

# 7. Recommendation / Conclusion

Ubuntu provides a stable and manageable environment for applications and infrastructure. APT and dpkg simplify software management, while systemd, systemctl, and journalctl help manage and troubleshoot services. Overall, Ubuntu is recommended for its reliability, security, ease of management, and strong support for development and DevOps workloads.

---

# 8. Contact Information

| **Name**      | **Email** |
| ------------- | --------- |
| Anshul kotiya |  anshul.kotiya.snaatak@mygurukulam.co         |

---

# 9. References

| Topic                       | Reference                                                                                                 |
| --------------------------- | --------------------------------------------------------------------------------------------------------- |
| Ubuntu  package management    | [Ubuntu](https://www.compilenrun.com/docs/os/ubuntu/ubuntu-package-management/)                                                 |

