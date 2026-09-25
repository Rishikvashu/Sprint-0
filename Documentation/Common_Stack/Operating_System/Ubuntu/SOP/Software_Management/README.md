# SOP: Ubuntu Software Management 
<p align="center">
<img width="522" height="228" alt="logo" src="https://github.com/user-attachments/assets/66b6fa00-7b2a-4a8f-ac30-1cb5df7c621c" />
</p>

---
| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Mansoor Alam | 26-08-2026 | 1.0 | Mansoor Alam | 26-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |


---

## Table of Contents

## Table of Contents

1. [Introduction](#introduction)
2. [Why Software Management?](#why-software-management)
3. [What is Software Management?](#what-is-software-management)
4. [Software Management Tools in Ubuntu](#software-management-tools-in-ubuntu)
5. [Package Installation Commands](#1-package-installation-commands)
6. [Package Update & Upgrade Commands](#2-package-update--upgrade-commands)
7. [Package Search Commands](#3-package-search-commands)
8. [Package Information Commands](#4-package-information-commands)
9. [Package Removal Commands](#5-package-removal-commands)
10. [DPKG Package Management Commands](#6-dpkg-package-management-commands)
11. [Use Cases: Installing Software by Adding Repository in Source](#use-cases-installing-software-by-adding-repository-in-source)
12. [Best Practices](#best-practices)
13. [Security Recommendations](#security-recommendations)
14. [Contacts](#contacts)
15. [References](#references)
---

## Introduction
This SOP outlines the process for installing, updating, and removing software on Ubuntu systems using the `apt` package manager. It ensures consistency, security, and efficiency in managing packages across Ubuntu environments.

---

### Why software management?
Software management ensures reliable, secure, and efficient operation of a system by handling software.

---

### What is software management?
Software management is the process of installing, updating, and removing applications and system tools on an operating system. In the Ubuntu, APT (Advanced Package Tool) command-line tool, allows users to efficiently manage software packages from trusted repositories.

---

### Software Management Tools in Ubuntu

Ubuntu mainly uses two important package management tools:

1. **APT (Advanced Package Tool)** - APT is a high-level package management tool that installs, updates, upgrades, and removes software while automatically handling dependencies.
2. **DPKG (Debian Package** - DPKG is a low-level package management tool that directly manages `.deb` packages.


# 1. Package Installation Commands

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `apt install` | `sudo apt install nginx` | Install a package from configured repositories |
| 2 | `apt install multiple` | `sudo apt install nginx git curl` | Install multiple packages at once |
| 3 | `apt install specific version` | `sudo apt install nginx=1.24.0-1ubuntu2` | Install a specific version of a package |
| 4 | `apt install --reinstall` | `sudo apt install --reinstall nginx` | Reinstall an already installed package |
| 5 | `apt install ./package.deb` | `sudo apt install ./nginx.deb` | Install a local `.deb` package and resolve dependencies |
| 6 | `dpkg -i` | `sudo dpkg -i nginx.deb` | Install a local `.deb` package directly |
| 7 | `apt download` | `apt download nginx` | Download a package without installing it |


<img width="1326" height="241" alt="img01" src="https://github.com/user-attachments/assets/3468aaaa-edf0-42a1-b550-5ffe0020ddc0" />

---

<img width="1290" height="356" alt="img2" src="https://github.com/user-attachments/assets/e0b33ab8-bed4-43c5-b054-181f8ff54d9e" />


# 2. Package Update & Upgrade Commands

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `apt update` | `sudo apt update` | Refresh package information from repositories |
| 2 | `apt upgrade` | `sudo apt upgrade` | Upgrade installed packages to newer versions |
| 3 | `apt full-upgrade` | `sudo apt full-upgrade` | Perform a complete upgrade; may install/remove packages to resolve dependencies |
| 4 | `apt list --upgradable` | `apt list --upgradable` | Show packages that have available updates |

<img width="1170" height="644" alt="img1" src="https://github.com/user-attachments/assets/f911622e-7923-46dd-a716-ac32cf7bc51b" />

---

# 3. Package Search Commands

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `apt search` | `apt search nginx` | Search for available packages |
| 2 | `apt list` | `apt list` | List available packages |
| 3 | `apt list --installed` | `apt list --installed` | List installed packages |
| 4 | `apt list --upgradable` | `apt list --upgradable` | List packages that can be upgraded |


<img width="945" height="547" alt="img4" src="https://github.com/user-attachments/assets/4387b3ce-161f-4dde-8b49-120aebca6db5" />

---

# 4. Package Information Commands

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `apt show` | `apt show nginx` | Display detailed information about a package |
| 2 | `apt policy` | `apt policy nginx` | Show installed, candidate, available versions and repository information |
| 3 | `dpkg -s` | `dpkg -s nginx` | Show installed package status and information |

<img width="1317" height="721" alt="img3" src="https://github.com/user-attachments/assets/4a7825c2-fdfa-44df-80f9-b90ded0a2415" />

---

# 5. Package Removal Commands

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `apt remove` | `sudo apt remove nginx` | Remove a package |
| 2 | `apt purge` | `sudo apt purge nginx` | Remove package and package-managed configuration files |
| 3 | `apt autoremove` | `sudo apt autoremove` | Remove unused automatically installed dependencies |

<img width="1323" height="339" alt="img5" src="https://github.com/user-attachments/assets/8f5b68f2-b5dd-41bc-8b7f-42f14b2e9b18" />

---

# 6. DPKG Package Management Commands

DPKG is the low-level package management tool for Debian-based systems.

| S.N | Command | Example | Purpose |
|---:|---|---|---|
| 1 | `dpkg -l` | `dpkg -l` | List installed packages |
| 2 | `dpkg -s` | `dpkg -s nginx` | Show package status |
| 3 | `dpkg -L` | `dpkg -L nginx` | List files installed by a package |
| 4 | `dpkg -S` | `dpkg -S /usr/sbin/nginx` | Find which package owns a file |
| 5 | `dpkg -i` | `sudo dpkg -i nginx.deb` | Install a `.deb` package |
| 6 | `dpkg -r` | `sudo dpkg -r nginx` | Remove a package |
| 7 | `dpkg -P` | `sudo dpkg -P nginx` | Purge a package |


<img width="1344" height="161" alt="img6" src="https://github.com/user-attachments/assets/225f8b8c-c7db-4261-8905-23173f48c1bc" />


---

## Use Cases: Installing Software by Adding Repository in Source

1.  **Installing Software Not in the Default Repositories:**
    * Many applications are not included in the default repositories of a Linux distribution.

2.  **Keeping Software Up-to-Date:**
    * Repositories provide a consistent way to update software.

3.  **Dependency Management:**
    * Software often depends on other software libraries.

4.  **Consistent Installation and Removal:**
    * Repositories provide a standardized way to install and remove software.

5.  **Security Updates:**
    * Repositories are used to distribute security patches.





## Best Practices

- Always run sudo apt update before installations or upgrades.

- Use apt show to verify software details.

- Regularly use autoremove and clean to optimize disk usage.

- Avoid using -y in scripts unless the outcome is known and tested.

---

## Security Recommendations

- Prefer software from official Ubuntu repositories.

- Verify third-party .deb files and PPAs before use.

- Regularly check for CVEs affecting installed software.


---

## Contacts

| Name            | Email Address                                 |
|-----------------|-----------------------------------------------|
|Mansoor Alam      |  mansoor.alam.snaatak@mygurukulam.co |

---

## References

| **Title**                              | **Link**                                                                                      |
|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Ubuntu Official Documentation          | [Visit](https://documentation.ubuntu.com/server/how-to/software/package-management/index.html)|
| Ubuntu Software Management Tutorial    | [Visit](https://documentation.ubuntu.com/server/tutorial/managing-software/)                  |
