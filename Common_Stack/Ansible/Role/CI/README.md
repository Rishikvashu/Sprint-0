# Ansible Role CI Workflow

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/2/24/Ansible_logo.svg" alt="Ansible Logo" width="100"/>
</p>

---

## Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Rani Kumari | 31-08-2026 | 1.0 | Rani Kumari | 05-09-2026 | Ishaan | Anuj Jain | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Role CI](#2-what-is-ansible-role-ci)
3. [Why CI Workflow is Required for Ansible Roles](#3-why-ci-workflow-is-required-for-ansible-roles)
4. [Workflow Diagram](#4-workflow-diagram)
   - [Ansible Role CI Workflow](#ansible-role-ci-workflow)
5. [Different Tools for Ansible CI](#5-different-tools-for-ansible-ci)
6. [Advantages and Disadvantages](#7-advantages-and-disadvantages)
7. [Best Practices](#8-best-practices)
8. [Recommendation / Conclusion](#9-recommendation--conclusion)
9. [Contact Information](#10-contact-information)
10. [References](#11-references)

---

## 1. Introduction

This **documentation** explains the complete **Ansible Role CI workflow**, starting from code changes and YAML validation to performing best-practice checks, testing the Ansible Role, and validating the results.

It also covers the **Ansible Role CI structure**, tools, workflow, advantages and disadvantages, and best practices used to maintain reliable, consistent, and error-free infrastructure automation code.

---

## 2. What is Ansible Role

An **Ansible Role** is a standard folder format that groups related tasks, variables, files, and handlers together. It breaks large playbooks into small, manageable components.

### Ansible Role Directory Structure

| Directory | Purpose |
|-----------|---------|
| `tasks/` | Contains the main execution steps of the role, usually defined in `main.yml`. |
| `handlers/` | Contains actions triggered when changes occur, such as restarting a service. |
| `templates/` | Contains Jinja2 configuration templates (`.j2`). |
| `files/` | Contains static files and scripts that need to be copied to the target server. |
| `vars/` | Contains variables used by the role. |
| `defaults/` | Contains default variables that can be overridden when required. |
| `meta/` | Contains role information, metadata, and role dependencies. |

---

## 3. Why CI Workflow is Required for Ansible Roles

| Requirement | Description |
|--------------|--------------|
| Early Error Detection | Catches syntax mistakes, missing variables, and YAML spacing errors before running on live servers. |
| Verifies Idempotency | Guarantees that running the role multiple times produces zero unintended changes on servers. |
| Multi-OS Testing | Automatically tests roles against multiple Linux distributions (Ubuntu, Debian, CentOS, RHEL). |
| Automated Pull Request Checks | Blocks faulty code from being merged into main production branches. |
| Prevents Production Downtime | Ensures only thoroughly tested and validated automation scripts are deployed. |

---
## 4 Workflow Diagram
<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/315c3e41-dcd5-4559-88e3-b6855028b48f" />

# Ansible Role CI Workflow

The **Ansible Role CI workflow** validates automation code through a sequence of automated tests:
## Workflow Steps

### 4.1 Git Commit & PR
A developer pushes changes or opens a Pull Request (PR) in the code repository.

### 4.2 YAML Linting
`yamllint` checks all YAML files for correct formatting and indentation.

### 4.3 Ansible Best Practices Check
`ansible-lint` scans tasks, variables, and handlers to enforce Ansible coding best practices and security rules.

### 4.4 Syntax Verification
Ansible validates the playbook syntax:
```bash
ansible-playbook -i localhost, tests/test.yml --syntax-check
```

### 4.5 Molecule Container Testing
Molecule spins up an isolated Docker container and executes the role from start to finish.

### 4.6 Idempotency Verification
Molecule runs the role a second time to verify that zero changes occur (`changed=0`), confirming full idempotency.

---

## 5. Different Tools for Ansible CI

| **Tool** | **Category** | **Description** |
| :--- | :--- | :--- |
| **Molecule** | Role Testing Framework | Designed specifically to test Ansible roles in ephemeral Docker or VM instances. |
| **Ansible-lint** | Static Code Analyzer | Enforces standards, security checks, and best practices on Ansible playbooks and roles. |
| **Yamllint** | Linter | Validates YAML syntax, formatting, line length, and indentation rules. |
| **Testinfra** | Infrastructure Testing | Python/Pytest framework for verifying server state (e.g., ports open, packages installed). |

---

## 6. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| :--- | :--- |
| **Automated Quality Checks:** Catches code and syntax errors automatically on every commit. | **Setup Effort:** Requires initial configuration of Molecule scenarios and test playbooks. |
| **Guaranteed Idempotency:** Confirms roles can run repeatedly without breaking server configuration. | **Docker Dependency:** Running Molecule locally or in CI requires Docker or a container runtime. |
| **Multi-Platform Validation:** Easily test roles across multiple Linux distributions in parallel containers. | **Longer Pipeline Times:** Full integration testing in containers takes more time than simple linting. |
| **Safer Collaboration:** Ensures multiple team members follow consistent coding standards. | **Flaky Tests if Unpinned:** Docker base image updates can occasionally cause transient test failures. |

---

## 7. Best Practices

| Practice | Description |
|----------|--------------|
| Run Linters Locally | Use `pre-commit` hooks to run `yamllint` and `ansible-lint` before pushing code. |
| Always Test Idempotency | Ensure Molecule tests run with idempotence checks enabled. |
| Keep Roles Modular | Write small, single-purpose roles to keep test suites fast and simple. |
| Automate in GitHub Actions / Jenkins | Trigger the full CI workflow automatically on every Pull Request. |
| Fail Fast | Run fast static checks (`yamllint`, `ansible-lint`) before running heavier Molecule tests. |

---

## 8. Conclusion

This documentation provides a complete overview of the **Ansible Role CI workflow** and explains how different stages work together to validate and test automation before deployment.

By using a **CI workflow with Ansible Roles**, errors can be caught early, idempotency can be verified, and roles can be tested across multiple operating systems. This approach ensures only reliable, well-tested automation is merged and promoted toward production.

---

## 9. Contact Information

| **Name** | **Email** |
| :--- | :--- |
| Rani Kumari | [rani.kumari.snaatak@mygurukulam.co](mailto:rani.kumari.snaatak@mygurukulam.co) |

---

## 10. References

| **Topic**                      | **Link**                                                                    |
| ------------------------------ | --------------------------------------------------------------------------- |
| **Molecule Documentation**     | [Molecule Documentation](https://ansible.readthedocs.io/projects/molecule/) |
| **Ansible-lint Documentation** | [Ansible-lint Documentation](https://ansible.readthedocs.io/projects/lint/) |

