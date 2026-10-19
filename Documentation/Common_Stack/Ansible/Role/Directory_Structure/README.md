# Ansible Role Directory Structure DOC

---

## Author Table

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Palak Upadhyay | 08-09-2026 | 1.0 | Palak Upadhyay | 19-09-2026 | Aryan Mishra | Aditya raj singh | - |
| Palak Upadhyay | 20-09-2026 | 1.1 | Palak Upadhyay | 20-09-2026 | Aryan Mishra | Aditya raj Singh | - |
---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Role](#2-what-is-ansible-role)
3. [Why Use Ansible Role Directory Structure](#3-why-use-ansible-role-directory-structure)
4. [Features of Ansible Roles](#4-features-of-ansible-roles)
5. [Standard Directory Layout](#5-standard-directory-layout)
6. [Ansible Role Execution Workflow](#6-ansible-role-execution-workflow)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

## 1. Introduction

This Standard Operating Procedure (SOP) defines the standardized directory structure and organizational best practices for Ansible Roles.
Structuring Ansible Playbooks into modular roles ensures high reusability, easy maintenance, and scalable configuration management across complex enterprise infrastructure.

---

## 2. What is Ansible Role

An Ansible Role is a self-contained, modular unit of automation that bundles tasks, variables, handlers, templates, and files into a standardized directory layout.
It allows developers to organize automation logic into independent components that can be shared and reused across multiple playbooks and inventory environments.

---

## 3. Why Use Ansible Role Directory Structure

Manual playbook creation often results in monolithic, unmaintainable files. Using a standardized Ansible Role Directory Structure provides:

* **Modularity:** Separates configuration data, tasks, and templates into clean, dedicated directories.
* **Reusability:** Roles can be shared across multiple playbooks, teams, and server environments.
* **Maintainability:** Simplifies troubleshooting and debugging by isolating specific automation concerns.
* **Scalability:** Enables seamless management of large-scale, multi-tier cloud infrastructure.

---

## 4. Features of Ansible Roles

| Feature | Description |
| :--- | :--- |
| **Modular Architecture** | Breaks complex automation into self-contained, independent components. |
| **Automatic Discovery** | Automatically detects and loads tasks, variables, and handlers without manual path imports. |
| **High Reusability** | Enables sharing and reusing roles across diverse server environments and repositories. |
| **Variable Precedence** | Provides clear, layered variable scoping from defaults to specific environment overrides. |
| **Lifecycle Handlers** | Triggers reactive system events like service restarts only when configurations change. |

---

## 5. Standard Directory Layout

<img width="1050" height="680" alt="ansible_directory_structure" src="https://github.com/user-attachments/assets/10fca5ba-0b38-4f43-8147-87e128ce9b14" />


### Directory Breakdown

| Directory | Purpose |
| :--- | :--- |
| **`defaults/`** | Default configuration values that can be easily overridden. |
| **`vars/`** | Role-internal variables that carry higher priority. |
| **`tasks/`** | Main sequential list of automation actions executed by the role. |
| **`handlers/`** | Conditional actions triggered by task notifications (e.g., restarting a service). |
| **`templates/`** | Dynamic Jinja2 configuration templates populated at runtime. |
| **`files/`** | Static files transferred directly to target servers without modification. |
| **`meta/`** | Role metadata, dependencies, and author information. |

---

## 6. Ansible Role Execution Workflow

<img width="1350" height="160" alt="ansible_workflow" src="https://github.com/user-attachments/assets/af78902e-72a5-4503-bb34-fa048b01d352" />


### Workflow Explanation

1. **Check Dependencies:** Ansible reads `meta/main.yml` to see if any prerequisite roles must run first.
2. **Load Variables:** Ansible loads default settings from `defaults/` and internal variables from `vars/`.
3. **Execute Tasks:** Ansible runs the step-by-step instructions defined in `tasks/main.yml`.
4. **Apply Templates & Files:** Tasks automatically pull dynamic files from `templates/` and static assets from `files/`.
5. **Trigger Handlers:** If any task reports a change, Ansible triggers the handlers (like restarting a service) in `handlers/main.yml`.

---

## 7. Best Practices

* Use `ansible-galaxy role init <role_name>` to automatically generate standard role scaffolding.
* Keep user-configurable parameters in `defaults/main.yml` to allow straightforward environment overrides.
* Break large automation routines into smaller modular task files and include them inside `tasks/main.yml`.
* Document all required input variables and provide example playbook snippets inside `README.md`.
* Ensure task idempotency by writing actions that only make changes when current server state differs.

---

## 8. Conclusion

The Ansible Role Directory Structure establishes a clean and standardized framework for scalable Infrastructure as Code.
By isolating tasks, variables, handlers, and templates into dedicated folders, teams eliminate playbook clutter and accelerate automation.
Adhering to these SOP guidelines guarantees consistent server configurations, seamless role reusability, and reliable deployment execution.

---

## 9. Contact Information

| Name | Email Address |
| :--- | :--- |
| Palak Upadhyay | [palak.upadhyay.snaatak@opstree.com](mailto:palak.upadhyay.snaatak@opstree.com) |

---

## 10. References

| Description | Reference Link |
| :--- | :--- |
| Official comprehensive guide on creating, structuring, and reusing Ansible roles | [Ansible Roles Documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html) |
| Community repository and industry standard hub for discovering and sharing Ansible roles | [Ansible Galaxy](https://galaxy.ansible.com/) |
