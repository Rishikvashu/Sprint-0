# Common Stack | Ansible | Role | Introduction

<p align="center">
<img width="1439" height="540" alt="image" src="https://github.com/user-attachments/assets/bd465073-26c3-4e31-ac9f-1499d897b643" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Maqbool Alam | 27-08-2026 | 1.0 | Maqbool Alam | 11-09-2026 | Rajnish Sharma  | Pritam/Komal | Abhishek/Manish Nautiyal |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Role](#2-what-is-ansible-role)
3. [Why Ansible Roles are Required](#3-why-ansible-roles-are-required)
4. [Key Features of Ansible Roles](#4-key-features-of-ansible-roles)
5. [Ansible Role Structure](#5-ansible-role-structure)
6. [How Ansible Roles Work](#6-how-ansible-roles-work)
7. [Advantages and Disadvantages](#7-advantages-and-disadvantages)
8. [Best Practices](#8-best-practices)
9. [Recommendation / Conclusion](#9-recommendation--conclusion)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

# 1. Introduction

An **Ansible Role** is a standardized way of organizing and reusing Ansible automation.

Instead of keeping all tasks, variables, templates, handlers, files, and other configuration inside a single large playbook, roles divide automation into reusable and maintainable components.

For example, an infrastructure project can have separate roles for:

```text
roles/
├── common/
├── nginx/
├── python/
├── golang/
├── docker/
└── monitoring/
```

Each role can be responsible for one specific technology or operational responsibility.

Ansible Roles are particularly useful in environments where the same configuration needs to be applied consistently across multiple servers or environments.

---

# 2. What is Ansible Role

An **Ansible Role** is a predefined directory structure that groups all the components required to perform a particular automation task.

A role can contain:

- Tasks
- Variables
- Default values
- Handlers
- Templates
- Files
- Metadata
- Operating-system-specific configuration

For example, a role named `nginx` may contain everything required to install and configure Nginx.

A playbook can then simply call the role:

```yaml
---
- name: Configure Web Servers
  hosts: webservers
  become: true

  roles:
    - nginx
```

The playbook does not need to contain every installation and configuration step itself.

---

# 3. Why Ansible Roles are Required

As infrastructure automation grows, maintaining everything inside a single playbook becomes difficult.

For example, a large playbook may contain:

```text
Install Nginx
Configure Nginx
Install Python
Configure Python
Install Go
Configure Go
Create Users
Configure SSH
Configure Firewall
Configure Monitoring
```

This creates several problems:

- Difficult to maintain.
- Difficult to reuse.
- Difficult to test.
- Difficult to understand.
- Changes to one technology can affect unrelated automation.
- Duplicate tasks may exist across multiple playbooks.

Roles solve this problem by separating automation into logical, reusable components.

For example:

```text
common role
    |
    +-- users
    +-- packages
    +-- security

nginx role
    |
    +-- installation
    +-- configuration
    +-- service

python role
    |
    +-- installation
    +-- virtual environment
    +-- configuration
```

This makes infrastructure automation more modular and scalable.

---

# 4. Key Features of Ansible Roles

## 4.1 Reusability

A role can be used by multiple playbooks.

Example:

```yaml
roles:
  - nginx
```

The same role can be reused for development, staging, and production servers.

---

## 4.2 Modularity

Each role can represent a specific responsibility.

For example:

```text
nginx
docker
python
golang
postgresql
redis
```

This keeps automation separated into manageable components.

---

## 4.3 Standard Directory Structure

Ansible roles follow a predictable directory structure.

This makes it easier for engineers to understand where tasks, variables, templates, and files are located.

---

## 4.4 Variables

Roles can expose configurable values.

For example:

```yaml
nginx_port: 80
nginx_worker_processes: auto
```

Different environments can provide different values without changing the role itself.

---

## 4.5 Defaults

A role can provide default configuration values.

Example:

```text
roles/nginx/defaults/main.yml
```

```yaml
nginx_port: 80
```

These values can be overridden when required.

---

## 4.6 Templates

Roles can contain Jinja2 templates for dynamically generating configuration files.

Example:

```text
roles/nginx/templates/nginx.conf.j2
```

The template can use variables:

```jinja2
listen {{ nginx_port }};
```

---

## 4.7 Handlers

Handlers are used for actions that should occur when configuration changes.

For example:

```yaml
notify:
  - Restart nginx
```

Handler:

```yaml
- name: Restart nginx
  ansible.builtin.service:
    name: nginx
    state: restarted
```

This avoids unnecessarily restarting services when nothing has changed.

---

## 4.8 File Management

Roles can contain static files that need to be deployed to target servers.

Example:

```text
roles/nginx/files/
```

---

## 4.9 Dependencies

A role can define dependencies on other roles.

For example:

```text
application
   |
   +-- common
   |
   +-- python
   |
   +-- nginx
```

This allows related automation to be composed into larger solutions.

---

## 4.10 Idempotency

Ansible tasks are designed to be **idempotent**.

Running the same role multiple times should normally result in the desired final state without unnecessarily repeating changes.

For example:

```yaml
- name: Install nginx
  ansible.builtin.apt:
    name: nginx
    state: present
```

If Nginx is already installed, Ansible does not need to reinstall it.

---

# 5. Ansible Role Structure

A typical role structure is:

```text
roles
│   └── nginx
│       ├── defaults
│       │   └── main.yml
│       ├── files
│       │   └── README.txt
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── README.md
│       ├── tasks
│       │   ├── install.yml
│       │   └── main.yml
│       ├── templates
│       │   ├── index.html.j2
│       │   └── nginx.conf.j2
│       ├── tests
│       │   ├── inventory
│       │   └── test.yml
│       └── vars
│           └── main.yml


```
<img width="1083" height="475" alt="image" src="https://github.com/user-attachments/assets/9a334470-2564-4a09-9c14-48cf0ed9b472" />


### Directory Responsibilities

| **Directory** | **Purpose** |
| -------------- | ----------- |
| `tasks/` | Main automation tasks |
| `defaults/` | Default variables that are easy to override |
| `vars/` | Role variables with higher precedence |
| `handlers/` | Handlers such as service restart/reload |
| `templates/` | Jinja2 configuration templates |
| `files/` | Static files copied to managed hosts |
| `meta/` | Role metadata and dependencies |
| `tests/` | Role testing files |

The standard role structure allows engineers to quickly locate a particular part of the automation.

---

# 6. How Ansible Roles Work

<img width="1064" height="595" alt="screen2" src="https://github.com/user-attachments/assets/72b71f6c-3f87-4389-8a18-9c711eebd65a" />

Example:

```yaml
---
- name: Configure Application Server
  hosts: application
  become: true

  roles:
    - common
    - python
    - nginx
```
**
Ansible loads the specified roles and executes their tasks against the selected hosts.

A role can therefore encapsulate the complete lifecycle of a component.**

---

# 7. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| -------------- | ----------------- |
| Reusable automation | Initial structure requires planning |
| Modular infrastructure | Poorly designed roles can become complex |
| Easier maintenance | Role dependencies can become difficult to manage |
| Consistent server configuration | Requires understanding of Ansible conventions |
| Environment-specific variables | Excessive abstraction can make debugging harder |
| Easier collaboration | Versioning role changes requires discipline |

---

# 8. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Keep roles focused | One role should generally have one clear responsibility |
| Use meaningful names | Role and variable names should clearly describe their purpose |
| Put overridable values in defaults | Use `defaults/main.yml` for values that users commonly change |
| Avoid hard-coded values | Use variables for environment-specific configuration |
| Use handlers for service changes | Restart or reload services only when required |
| Keep tasks modular | Split large task files when they become difficult to maintain |
| Use idempotent modules | Prefer Ansible modules over unnecessary shell commands |
| Version-control roles | Store roles and playbooks in Git |
| Test roles | Validate roles against supported operating systems and configurations |
| Document variables | Explain important role variables and their expected values |

---

# 9. Recommendation / Conclusion

Ansible Roles are recommended for infrastructure environments where automation needs to be **reusable, modular, maintainable, and scalable**.

Instead of creating large monolithic playbooks, infrastructure should be divided into logical roles such as:

```text
common
nginx
python
golang
docker
postgresql
redis
monitoring
```

Each role should have a clear responsibility and expose configurable variables where required.

A well-designed role structure makes it easier to reuse the same automation across multiple servers and environments while maintaining consistent configuration.

---

# 10. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Maqbool Alam | maqbul.alam.snaatak@mygurukulam.co |

---

# 11. References

| **Topic** | **Description** | **Link** |
| --------- | --------------- | -------- |
| Ansible Roles | Official documentation for Ansible role organization and reuse | https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html |
| Ansible Playbooks | Documentation for defining automation workflows | https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html |
| Ansible Galaxy | Tooling for creating and sharing Ansible roles | https://docs.ansible.com/ansible/latest/galaxy/user_guide.html |
| Jinja2 Templates | Template syntax used by Ansible | https://jinja.palletsprojects.com/ |
| Ansible Handlers | Documentation on handlers and notify | https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html |
| Ansible Variables | Variable precedence and usage | https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html |
