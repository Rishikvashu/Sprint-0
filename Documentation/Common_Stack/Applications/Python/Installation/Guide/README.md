# Python Installation Document

<p align="left">
  <img width="240" height="110" alt="Python" src="https://upload.wikimedia.org/wikipedia/commons/f/f8/Python_logo_and_wordmark.svg" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- | --------------- |
| Shivam Tomar | 24-08-2026 | v1.1 | Shivam Tomar | 02-09-2026 | Team | Ishaan | Anuj Jain | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Operating System and Package Setup](#4-operating-system-and-package-setup)
5. [Python Environment Setup](#5-python-environment-setup)
6. [Python Installation on Different Operating Systems](#6-python-installation-on-different-operating-systems)
7. [Validation Checklist](#7-validation-checklist)
8. [Troubleshooting](#8-troubleshooting)
9. [Best Practices](#9-best-practices)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

# 1. Introduction

This document provides a standardized procedure for installing and verifying Python 3 on Ubuntu-based environments.

Python is a high-level, interpreted programming language widely used for software development, automation, scripting, data analysis, and AI/ML applications.

---

# 2. Purpose

The purpose of this Document is to provide a consistent Python setup procedure for Ubuntu-based development and application environments.

It helps ensure that:

- Python 3 is available.
- pip is available for package installation.
- Virtual environments can be created.
- Project dependencies can be isolated.
- The active Python and pip paths can be verified.

---

# 3. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| Operating System | Ubuntu-based environment |
| Access | Terminal / SSH access |
| Permissions | `sudo` access for package installation |
| Package Manager | `apt` |
| Internet Access | Required for downloading packages |
| Project Directory | Required when creating a project virtual environment |

## Verify Prerequisites

```bash
lsb_release -a
```

<p align="left">
  <img width="766" height="140" alt="image" src="https://github.com/user-attachments/assets/0fe5c420-6b63-4a6e-ac67-d5a9951de4d4" />
</p>

---

# 4. Operating System and Package Setup

## Step 1: Update Package Information

```bash
sudo apt update
```

## Step 2: Upgrade Installed Packages

```bash
sudo apt upgrade -y
```

<p align="left">
  <img width="558" height="220" alt="image" src="https://github.com/user-attachments/assets/4f70f90b-587d-437c-91e4-bd66f6621ae1" />
</p>

---

# 5. Python Environment Setup

## Step 1: Install Python 3

```bash
sudo apt install -y python3
```


<p align="left">
  <img width="561" height="211" alt="image" src="https://github.com/user-attachments/assets/76b998bd-f5d4-462f-b22c-ec326c1ba3ea" />
</p>

---

## Step 2: Install pip

```bash
sudo apt install -y python3-pip
```

### Verification

```bash
pip3 --version
which pip3
```

<p align="left">
  <img width="561" height="228" alt="image" src="https://github.com/user-attachments/assets/c603ec03-bbc7-4d51-825b-33e11c8de777" />
</p>

---

## Step 3: Install Virtual Environment Support

```bash
sudo apt install -y python3-venv
```

<p align="left">
  <img width="563" height="140" alt="image" src="https://github.com/user-attachments/assets/2f61d137-dd72-413c-8db9-be7512999625" />
</p>
---

## Step 4: Create a Virtual Environment

Inside the Python project directory:

```bash
cd <PROJECT_DIRECTORY>
python3 -m venv .venv
```

This creates an isolated `.venv` environment inside the project.

---

## Step 5: Activate the Virtual Environment

```bash
source .venv/bin/activate
```

<p align="left">
  <img width="556" height="82" alt="image" src="https://github.com/user-attachments/assets/223d4e83-4642-470a-a5a4-584649e98a05" />
</p>

---

# 6. Python Installation on Different Operating Systems

| **Operating System** | **Package Manager** | **Installation Command** |
| -------------------- | ------------------- | ------------------------ |
| **Ubuntu / Debian** | `apt` | `sudo apt update && sudo apt install -y python3 python3-pip python3-venv` |
| **RHEL / CentOS / Rocky / Fedora** | `dnf` / `yum` | `sudo dnf install -y python3 python3-pip` |
| **Alpine Linux** | `apk` | `apk add --no-cache python3 py3-pip` |
| **Arch Linux** | `pacman` | `sudo pacman -S python python-pip` |
| **macOS** | `Homebrew` | `brew install python` |
| **Windows** | `winget` / `choco` | `winget install Python.Python.3.12` *(or `choco install python`)* |

---

# 7. Validation Checklist

| **Component** | **Verification Command** | **Expected Result** |
| ------------- | ------------------------ | ------------------- |
| **Python 3 Binary** | `python3 --version` | Displays installed Python 3.x version |
| **Python Path** | `which python3` | Resolves to system binary (e.g., `/usr/bin/python3`) |
| **pip Package Manager** | `pip3 --version` | Displays pip version and corresponding Python engine |
| **venv Module** | `python3 -m venv --help` | Displays usage instructions without module errors |
| **Virtual Environment Activation** | `source .venv/bin/activate` | Active shell prompt is prefixed with `(.venv)` |
| **Isolated Environment Path** | `which python` | Points inside the project environment (`.../.venv/bin/python`) |

---

# 8. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| --------- | --------- | ------------ |
| `python3: command not found` | Python 3 package is not installed | Run `sudo apt update && sudo apt install -y python3` |
| `pip3: command not found` | pip package is not installed | Run `sudo apt install -y python3-pip` |
| `No module named venv` | Virtual environment package is missing | Run `sudo apt install -y python3-venv` |
| `externally-managed-environment` error | Installing packages globally on modern Linux releases | Create and activate a virtual environment (`python3 -m venv .venv && source .venv/bin/activate`) before running `pip install` |
| Virtual environment prompt `(.venv)` not showing | Activation script was not sourced | Ensure that use `source .venv/bin/activate` instead of executing it directly |
| `source: .venv/bin/activate: No such file or directory` | Environment has not been created or path is incorrect | Verify you are in the project root directory and execute `python3 -m venv .venv` |

---

# 9. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| **Always Isolate Dependencies** | Never install project dependencies globally. Always create and use a project-level virtual environment (`.venv`). |
| **Never Run `sudo pip`** | Avoid running `pip` with `sudo` as it risks breaking system-level Python packages managed by `apt`. |
| **Version Control Exclusions** | Always add `.venv/`, `__pycache__/`, and `*.pyc` to your `.gitignore` file to prevent committing local dependencies and bytecode. |
| **Pin & Export Dependencies** | Maintain a `requirements.txt` or `pyproject.toml` file (`pip freeze > requirements.txt`) to ensure reproducible builds across environments. |
| **Security Auditing** | Regularly scan project dependencies for vulnerabilities using tools such as `pip-audit` or `safety`. |

---

# 10. Conclusion

This Document provides a standardized approach to installing and verifying Python 3 on Ubuntu-based environments.

The setup is complete when Python, pip, virtual-environment support, and the project `.venv` pass the verification checks described in this Document.

---

# 11. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Shivam Tomar | [shivam.tomar.snaatak@mygurukulam.co](mailto:shivam.tomar.snaatak@mygurukulam.co) |

---

# 12. References

| **Topic** | **Link** |
| --------- | -------- |
| Python Official Website | [python.org](https://www.python.org/) |
| Python Linux Downloads | [python.org/downloads/source/](https://www.python.org/downloads/source/) |
| Ubuntu Package Management | [ubuntu.com/server/docs/package-management](https://ubuntu.com/server/docs/package-management) |
