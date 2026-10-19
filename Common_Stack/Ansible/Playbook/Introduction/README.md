# Ansible Playbook Introduction

<p align="left">
  <img width="240" height="110" alt="Ansible" src="https://upload.wikimedia.org/wikipedia/commons/2/24/Ansible_logo.svg" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- | --------------- |
| Shivam Tomar | 24-08-2026 | v1.1 | Shivam Tomar | 07-09-2026 | Team | Ishaan | Anuj Jain | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [What is an Ansible Playbook?](#3-what-is-an-ansible-playbook)
4. [Why Use Ansible Playbooks?](#4-why-use-ansible-playbooks)
5. [Comparison: Shell Scripts vs. Ad-hoc Commands vs. Playbooks](#5-comparison-shell-scripts-vs-ad-hoc-commands-vs-playbooks)
6. [Key Features & Benefits](#6-key-features--benefits)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

# 1. Introduction

This Document introduces Ansible Playbooks, explains their structure, key features, and benefits, and provides recommended best practices.

An **Ansible Playbook** is a declarative YAML file used to define automation blueprints for configuring systems, deploying applications, and orchestrating complex IT infrastructure workflows. Unlike individual ad-hoc commands, Playbooks allow multi-tier operations to be expressed as readable, repeatable, and version-controlled configuration as code.

---

# 2. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| **Operating System** | Linux/Unix-based control environment (e.g., Ubuntu) |
| **Access** | Terminal and SSH access to managed hosts |
| **Ansible** | Ansible installed on the control node |

---

# 3. What is an Ansible Playbook?

An Ansible Playbook organizes automation tasks into structured, reusable units that execute against targeted systems. 

**Execution Hierarchy:**
`Inventory` ➔ `Playbook` ➔ `Play` ➔ `Tasks` ➔ `Modules` ➔ `Managed Hosts`

### Core Components

* **Inventory:** Defines and groups target hosts against which the automation runs.
* **Play:** Maps a specific group of hosts to a designated list of tasks. A Playbook can contain multiple plays.
* **Tasks:** The ordered sequence of actions executed sequentially within a play.
* **Modules:** The pre-built execution units (e.g., `ansible.builtin.apt`, `ansible.builtin.service`) that perform the actual work on target systems.

### Practical Example

Below is a standard Playbook illustrating the relationship between the target **hosts**, the **tasks**, and the underlying **modules**:

```yaml
---
- name: Configure and launch Nginx web server
  hosts: webservers
  become: true

  tasks:
    - name: Install Nginx package
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: true

    - name: Ensure Nginx service is running and enabled
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true
```

---

# 4. Why Use Ansible Playbooks?

Ansible Playbooks eliminate the manual effort, configuration drift, and maintenance overhead associated with custom shell scripting and one-off ad-hoc commands.

### Key Reasons to Use Playbooks

* **Infrastructure as Code (IaC):** Document system configurations directly in code to review, audit, and track changes via Git.
* **Eliminate Configuration Drift:** Ensure consistent system state across development, staging, and production environments.
* **Multi-Tier Orchestration:** Coordinate complex workflows across different server groups (e.g., databases, web servers, load balancers) in a single execution.
* **Collaboration & Readability:** Human-readable YAML syntax allows developers, sysadmins, and DevOps engineers to collaborate easily without programming expertise.

---

# 5. Comparison: Shell Scripts vs. Ad-hoc Commands vs. Playbooks

Understanding when to transition from basic scripting or ad-hoc tasks to structured Playbooks is essential for scalable automation:

| **Parameter** | **Shell / Bash Scripts** | **Ansible Ad-hoc Commands** | **Ansible Playbooks** |
| ------------- | ------------------------ | --------------------------- | --------------------- |
| **Execution Approach** | Imperative (step-by-step commands) | Single-task execution | Declarative (defines desired end state) |
| **Idempotency** | Requires complex custom logic | Module-dependent | Built-in across native modules |
| **Multi-Host Management** | Manual SSH loops and error handling | Uses inventory for single commands | Native multi-tier, multi-host orchestration |
| **Reusability & Scale** | Low; tightly coupled to environment | Low; suitable only for quick one-liners | High; reusable via variables, handlers, and roles |

---

# 6. Key Features & Benefits

| **Feature / Benefit** | **Description** | **Practical Example** |
| --------------------- | --------------- | --------------------- |
| **Agentless** | No background agent or custom software is required on managed hosts. Ansible communicates over standard SSH/WinRM. | Connects directly using existing SSH keys without managing client daemons. |
| **YAML-based** | Uses human-readable YAML syntax, making Playbooks easy to read, write, and audit without programming experience. | Simple key-value structure (`name: nginx`, `state: present`). |
| **Idempotency** | Modules ensure a task only makes changes if the system is not already in the desired state, preventing unwanted side effects. | Running `state: present` multiple times installs the package once and makes no redundant changes on subsequent runs. |
| **Declarative Automation** | Focuses on defining the *desired end state* of the system rather than specifying the manual steps to get there. | Specify `state: started` instead of writing custom conditional shell scripts to check process status. |
| **Modular** | Offers thousands of built-in and community modules for operating systems, cloud providers, and network devices. | Use `ansible.builtin.copy` for files, `ansible.builtin.user` for user accounts, and `ansible.builtin.apt` for packages. |
| **Reusable** | Playbooks support reusable components such as variables, handlers, templates, and structured roles. | Define `{{ http_port }}` as a variable across environments rather than hardcoding port numbers. |
| **Configuration as Code** | Infrastructure and application setups are documented directly in code and version-controlled via Git. | Track changes, perform peer reviews, and rollback configuration states via standard Git workflows. |
| **Privilege Escalation** | Supports seamless privilege escalation (`become`) to execute administrative tasks safely. | Set `become: true` at the play or task level to run operations with `sudo` privileges. |
| **Execution Control** | Granular control over execution using conditionals (`when`), loops (`loop`), tags (`tags`), and dry-run check mode (`--check`). | Use `when: ansible_os_family == "Debian"` to run platform-specific tasks conditionally. |

---

# 7. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| **Use Fully Qualified Collection Names (FQCN)** | Always use full module names (e.g., `ansible.builtin.apt` instead of `apt`) to avoid module naming conflicts and ensure portability. |
| **Keep Tasks Idempotent** | Prefer native Ansible modules over raw `shell` or `command` modules whenever possible to maintain idempotency. |
| **Use Descriptive Task Names** | Give clear, meaningful names to all plays and tasks so execution logs and failure messages are easy to diagnose. |
| **Use Variables Instead of Hardcoding** | Externalize environment-specific settings (e.g., ports, usernames, file paths) into variables for flexibility across environments. |
| **Organize Automation with Roles** | Break down complex Playbooks into reusable roles with standard directory structures (`tasks`, `vars`, `handlers`, `templates`). |
| **Validate Before Execution** | Always run `ansible-playbook --syntax-check` and dry-run with `ansible-playbook --check` before applying changes to production. |

---

# 8. Conclusion

Ansible Playbooks provide a declarative, human-readable, and idempotent approach to IT automation. By defining infrastructure and application configurations as code in YAML, Playbooks empower DevOps teams to achieve consistent, repeatable, and scalable operations across enterprise environments.

---

# 9. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Shivam Tomar | [shivam.tomar.snaatak@mygurukulam.co](mailto:shivam.tomar.snaatak@mygurukulam.co) |

---

# 10. References

| **Topic** | **Link** |
| --------- | -------- |
| Ansible Official Website | [ansible.com](https://www.ansible.com/) |
| Ansible Playbook Documentation | [docs.ansible.com - Playbook Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html) |
| Ansible Built-in Modules Reference | [docs.ansible.com - Built-in Collection](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/) |
