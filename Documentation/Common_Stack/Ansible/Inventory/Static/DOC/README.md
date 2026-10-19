# SOP: Configuration Management | Ubuntu Linux | Ansible Static Inventory Setup
<p align="center">
  <img width="100%" height="200" style="object-fit: cover; border-radius: 6px;" alt="Ansible Banner" src="https://wallpapercave.com/wp/wp11273112.jpg" />
</p>

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Anurag Maurya | 25-08-2026 | v1 | Anurag Maurya | 25-08-2026 | Divya M | Aayush Verma | Mahesh Kumar/Varun |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Static Inventory](#2-what-is-ansible-static-inventory)
3. [Why Ansible Static Inventory is Required](#3-why-ansible-static-inventory-is-required)
4. [Key Features of Ansible Static Inventory](#4-key-features-of-ansible-static-inventory)
5. [Prerequisites and System Requirements](#5-prerequisites-and-system-requirements)
6. [Ansible Static Inventory Setup and Verification](#6-ansible-static-inventory-setup-and-verification)
7. [Quick Commands](#7-quick-commands)
8. [Troubleshooting](#8-troubleshooting)
9. [Use Cases](#9-use-cases)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

Step-by-step Standard Operating Procedure (SOP) for setting up and managing an Ansible static inventory file on Ubuntu Linux. Written in simple, clear English for beginners to easily configure host groups and connection variables.

---

# 2. What is Ansible Static Inventory

An Ansible Static Inventory is a simple configuration file (usually written in INI or YAML format) that lists all remote server IP addresses, hostnames, and host groups managed by Ansible. It tells Ansible *where* to run playbooks and *how* to authenticate via SSH.

---

# 3. Why Ansible Static Inventory is Required

Ansible needs a central index of target machines before executing playbooks or ad-hoc commands:
- **Central Host Organization**: Group servers logically by role (e.g., `webservers`, `dbservers`, `staging`).
- **Connection Variable Management**: Assign specific SSH users, ports, and private key paths per host group.
- **Predictable Execution**: Ensure playbooks target exact, static IP addresses in controlled environments.

---

# 4. Key Features of Ansible Static Inventory

| **Feature** | **Description** |
| ----------- | --------------- |
| **INI & YAML Syntax** | Human-readable structure supporting simple INI groups and nested YAML configurations. |
| **Host Grouping** | Group servers into logical tiers (`[webservers]`, `[dbservers]`) for selective execution. |
| **Group Variables** | Assign variables across entire host groups using `[groupname:vars]`. |
| **Inventory Graphing** | Inspect hierarchy visualization using `ansible-inventory --graph`. |
| **Ad-Hoc Connectivity** | Test live SSH connections across all managed inventory nodes via `ansible all -m ping`. |

---

# 5. Prerequisites and System Requirements

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Version | Ubuntu 20.04/22.04/24.04 LTS |
| Control Node | Ansible CLI core (`ansible`, `ansible-inventory`) installed |
| Remote Hosts | Target Linux servers with SSH enabled |
| Access Rights | Non-root user with `sudo` privileges |
| SSH Key Pair | OpenSSH key generated (`~/.ssh/id_rsa.pub` copied to targets) |

> [!NOTE]
> IP addresses, usernames, and key paths shown in this guide are illustrative. Adapt IP addresses to match your actual network environment.

---

# 6. Ansible Static Inventory Setup and Verification

### Step 1: Verify Ansible Installation

Check that Ansible core package is installed on your control node.

```bash
ansible --version
```

Expected output:

```bash
ansible [core 2.16.3]
  config file = /etc/ansible/ansible.cfg
  python version = 3.12.3 (/usr/bin/python3)
```

*What this command does:* Reports installed Ansible version, config file path, and Python runtime version.

<details>
<summary>Click to view Terminal Screenshot: Ansible Version Check</summary>
<br>

![Ansible Version Terminal Screenshot](./assets/ansible_version.png)

</details>

---

### Step 2: Create Inventory Workspace Directory

Establish a dedicated project folder for your inventory files.

```bash
# Create directory structure
mkdir -p ~/ansible-demo/inventory

# Change directory into workspace
cd ~/ansible-demo/inventory
```

Expected output:

```bash
~/ansible-demo/inventory
```

*What this command sequence does:* Creates folder structure `~/ansible-demo/inventory` and switches shell context into it.

<details>
<summary>Click to view Terminal Screenshot: Create Inventory Directory</summary>
<br>

![Create Inventory Directory Terminal Screenshot](./assets/ansible_create_inventory.png)

</details>

---

### Step 3: Create INI Static Inventory File (`hosts.ini`)

Create `hosts.ini` and define server groups with connection variables.

```bash
cat << 'EOF' > ~/ansible-demo/inventory/hosts.ini
[webservers]
web1.example.com ansible_host=192.168.1.10
web2.example.com ansible_host=192.168.1.11

[dbservers]
db1.example.com ansible_host=192.168.1.20

[webservers:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa

[dbservers:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa

[all:vars]
ansible_python_interpreter=/usr/bin/python3
EOF
```

Expected output:

```bash
hosts.ini created successfully
```

*What this configuration does:* Groups web servers under `[webservers]` and database servers under `[dbservers]`, setting SSH user (`ubuntu`), private key path, and Python 3 interpreter path.

<details>
<summary>Click to view Terminal Screenshot: Create hosts.ini Inventory</summary>
<br>

![Ansible Hosts INI Terminal Screenshot](./assets/ansible_hosts_ini.png)

</details>

---

### Step 4: Validate Inventory Structure (`ansible-inventory --graph`)

Visualize host grouping and tree hierarchy.

```bash
ansible-inventory -i ~/ansible-demo/inventory/hosts.ini --graph
```

Expected output:

```ini
@all:
  |--@dbservers:
  |  |--db1.example.com
  |--@ungrouped:
  |--@webservers:
  |  |--web1.example.com
  |  |--web2.example.com
```

*What this command does:* Parses `hosts.ini` and prints an ASCII tree graph showing all parent groups, child groups, and assigned hostnames.

<details>
<summary>Click to view Terminal Screenshot: Graph Inventory Hierarchy</summary>
<br>

![Ansible Inventory Graph Terminal Screenshot](./assets/ansible_inventory_graph.png)

</details>

---

### Step 5: Test Connectivity via Ansible Ping (`ansible all -m ping`)

Verify SSH connectivity and authentication to managed target hosts.

```bash
ansible all -i ~/ansible-demo/inventory/hosts.ini -m ping
```

Expected output:

```bash
web1.example.com | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

*What this command does:* Executes Ansible's `ping` module across all hosts in `hosts.ini` to confirm SSH connection, user credentials, and Python availability.

<details>
<summary>Click to view Terminal Screenshot: Ansible Ping Connectivity</summary>
<br>

![Ansible Ping Connectivity Terminal Screenshot](./assets/ansible_ping_connectivity.png)

</details>

---

### Step 6: Export Inventory to JSON (`ansible-inventory --list`)

Inspect full inventory payload in JSON format.

```bash
ansible-inventory -i ~/ansible-demo/inventory/hosts.ini --list
```

Expected output:

```json
{
    "_meta": {
        "hostvars": {
            "web1.example.com": {
                "ansible_host": "192.168.1.10"
            }
        }
    }
}
```

*What this command does:* Exports internal inventory data structure into formatted JSON payload used by automated pipelines.

<details>
<summary>Click to view Terminal Screenshot: Export Inventory JSON</summary>
<br>

![Inventory JSON List Terminal Screenshot](./assets/ansible_inventory_list.png)

</details>

---

# 7. Quick Commands

| **Task** | **Command** | **Description** |
| -------- | ----------- | --------------- |
| View graph | `ansible-inventory -i hosts.ini --graph` | Show inventory hierarchy tree |
| Export JSON | `ansible-inventory -i hosts.ini --list` | Export inventory in JSON format |
| Ping all | `ansible all -i hosts.ini -m ping` | Test SSH connectivity across hosts |
| Ping group | `ansible webservers -i hosts.ini -m ping` | Ping specific host group |
| Run shell cmd | `ansible all -i hosts.ini -m shell -a "uptime"` | Run shell command across hosts |

---

# 8. Troubleshooting

| **Symptom / Error** | **Possible Root Cause** | **Resolution Step** |
| ------------------- | ----------------------- | ------------------- |
| `UNREACHABLE! Failed to connect` | SSH port blocked or incorrect IP | Check target IP address and verify port 22 is open (`nc -zv <IP> 22`). |
| `Permission denied (publickey)` | Incorrect SSH key path or permissions | Verify `ansible_ssh_private_key_file` path and ensure key permissions are `600`. |
| `Unable to parse /etc/ansible/hosts` | Syntax error in INI file | Check `hosts.ini` for bracket typos or invalid variable formatting. |
| `Python command not found` | Target host lacks Python 3 | Set `ansible_python_interpreter=/usr/bin/python3` in `[all:vars]`. |

---

# 9. Use Cases

1. **Multi-Server Deployment**: Organize production web and database servers to deploy playbooks selectively.
2. **Environment Separation**: Maintain separate static inventory files (`staging.ini`, `prod.ini`) for infrastructure safety.
3. **Ad-Hoc Health Checks**: Run quick commands across hundreds of servers (e.g., checking uptime or disk space) using one command.

---

# 10. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Use Version Control | Track inventory files in Git repository to log infrastructure changes. |
| Secure Secrets | Never hardcode passwords in `hosts.ini`; use SSH keys or Ansible Vault. |
| Group Logically | Group hosts by role (`[webservers]`, `[dbservers]`) rather than environment. |
| Test Connectivity | Run `ansible all -m ping` before executing playbooks to catch SSH issues early. |

---

# 11. Conclusion

Ansible Static Inventory files (`hosts.ini`) provide a simple, human-readable method for organizing remote servers, managing SSH connection variables, and targeting playbooks accurately across enterprise environments.

---

# 12. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Anurag Maurya | [anurag.maurya.snaatak@mygurukulam.co](mailto:anurag.maurya.snaatak@mygurukulam.co) |

---

# 13. References

| **Topic** | **Description** |
| --------- | --------------- |
| [Ansible Inventory Documentation](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html) | Official guide on managing Ansible inventories. |
| [Ansible Connection Variables](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html) | Guide on SSH variables and authentication. |
