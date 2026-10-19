# Ansible Playbook Continuous Delivery (CD) Documentation

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Vineet     | 28-08-2026     | 1.1         | Vineet              | 06-09-2026         | Aryan Mishra     |  Aditya Raj Singh                |              |
| Vineet     | 28-08-2026      | 1.2         | Vineet              | 11-09-2026         | Aryan Mishra      |Aditya Raj Singh    |         |
| Vineet     | 28-08-2026      | 1.3         | Vineet              | 16-09-2026         | Aryan Mishra      |Aditya Raj Singh    |         |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Playbook in CD](#2-what-is-ansible-playbook-in-cd)
3. [Why use Ansible in CD](#3-why-use-ansible-in-cd)
4. [Features](#4-features)
5. [Pre-requisites](#5-pre-requisites)
6. [Ansible Playbook CI Reference](#6-ansible-playbook-ci-reference)
7. [Ansible Playbook in CD Execution](#7-ansible-playbook-in-cd-execution)
8. [CD Workflow](#8-cd-workflow)
9. [Deployment Flow](#9-deployment-flow)
10. [Deployment Validation](#10-deployment-validation)
11. [Advantages and Disadvantages](#11-advantages-and-disadvantages)
12. [Best Practices](#12-best-practices)
13. [Conclusion](#13-conclusion)
14. [Contact Information](#14-contact-information)
15. [References](#15-references)

---

# 1. Introduction

This document explains the **Continuous Delivery (CD) workflow using Ansible Playbooks**. 

In a CD environment, Ansible Playbooks are used to automate application deployment, server configuration, and environment setup after the application successfully passes the required CI checks. The workflow covers how a build artifact moves from the CI pipeline, uses the Ansible Inventory, and executes deployment tasks on target servers, followed by deployment validation.

---
# 2. What is Ansible Playbook in CD

An **Ansible Playbook** is a YAML-based configuration file that defines a series of automated tasks to be executed on specified remote servers. 

In the context of Continuous Delivery (CD), the Playbook acts as the automation layer and execution engine between the **CD pipeline** (like Jenkins or GitLab CI) and the **target servers**. It ensures that the built artifacts (like `.jar` or `.war` files) are correctly deployed, services are restarted, and the environment is configured exactly as defined.

---
# 3. Why use Ansible in CD

Ansible is widely adopted in CD pipelines to:
* **Automate Repetitive Tasks:** Eliminates manual SSH logins and file transfers for deployment.
* **Ensure Consistency:** Deploys the exact same way across Dev, QA, Staging, and Production environments.
* **Reduce Human Error:** Replaces manual configuration with tested code.
* **Speed up Deliveries:** Deploys complex, multi-tier applications across multiple servers simultaneously in minutes.

---
# 4. Features

| Feature | Description |
|---|---|
| **Agentless Architecture** | Connects to target servers using SSH for Linux or WinRM for Windows without requiring extra software agents. |
| **Idempotency** | Can run the same playbook multiple times and only makes changes when the current state differs from the desired state. |
| **Human-Readable YAML** | Uses simple YAML syntax, making playbooks easy to read, review, and maintain. |
| **Modular Design (Roles)** | Allows complex deployments to be divided into reusable components called Ansible Roles. |
---
# 5. Pre-requisites

Before setting up an Ansible CD workflow, ensure the following are available:

| **Requirement** | **Purpose** |
|---|---|
| Control Node (Ubuntu/Linux) | The machine running the CD pipeline and executing the Playbook. |
| Ansible Installed | Required on the Control Node to run the commands. |
| Target Servers | The application servers (e.g., AWS EC2) where code will be deployed. |
| SSH Key Authentication | Passwordless SSH access from the Control Node to the Target Servers. |
| Python 3 | Required on target servers for Ansible modules to execute properly. |

---
# 6. Ansible Playbook CI Reference

The CI workflow for Ansible Playbooks, including build, testing, quality, and security checks, is documented separately in this link [Ansible Playbook CI Workflow Documentation](https://github.com/SnaatakKubeClan/Sprint-0/blob/SCRUM-47-VASHISHTHA--PRAKASH/Documentation/Common-Stack/Ansible/Playbook/CI/README.md).

---
# 7. Ansible Playbook in CD Execution

An **Ansible Playbook** is a YAML file that defines the tasks required to configure servers or deploy an application.

In a CD workflow, the Playbook acts as the automation layer between the **CD pipeline** and the **target servers**.

A typical Playbook execution command is:

```bash
ansible-playbook -i inventory.ini deploy.yml
```

Where:

* `inventory.ini` defines the target servers.
* `deploy.yml` contains the deployment tasks.
* Ansible connects to the target servers and executes the defined tasks.

---

# 8. CD Workflow

The typical Ansible-based CD workflow is:

<img width="262" height="862" alt="image" src="https://github.com/user-attachments/assets/3aeb8910-2b02-40ad-9eb3-d349b72ddc18" />


### Step 1: Developer Pushes Code

The developer commits and pushes application changes to the Git repository.

### Step 2: CI Pipeline

The CI pipeline validates the application by performing activities such as:

* Source code checkout
* Build
* Unit testing
* Code quality checks
* Security checks

### Step 3: Build Artifact

After successful CI validation, a deployable **build artifact** is generated.

The artifact is then made available for the CD process.

### Step 4: CD Pipeline Starts

The CD pipeline is triggered after successful CI completion.

Depending on the organization's process, deployment can be automatic or require an approval before production deployment.

### Step 5: Ansible Inventory

The Ansible Inventory defines the target servers where the application needs to be deployed.

Example:

```ini
[app_servers]

app01 ansible_host=192.168.1.10
app02 ansible_host=192.168.1.11
```

### Step 6: Ansible Playbook Execution

The CD pipeline executes the Ansible Playbook using the inventory:

```bash
ansible-playbook -i inventory.ini deploy.yml
```

Ansible connects to the target servers and executes the deployment tasks defined in the Playbook.

### Step 7: Application Deployment

The Playbook performs the required deployment activities, such as:

* Preparing the target server
* Creating required directories
* Copying application artifacts
* Updating configuration
* Managing application services
* Restarting services when required

### Step 8: Deployment Validation

After deployment, validation checks are performed to verify that:

* The application service is running.
* Required ports are available.
* Application health checks are successful.
* The deployed version is correct.

If validation succeeds, the deployment is considered successful.

---

# 9. Deployment Flow

The deployment portion of the CD workflow can be represented as:

<img width="262" height="862" alt="image" src="https://github.com/user-attachments/assets/4f5d6d57-d8a3-4521-8d41-30f4f896a395" />

### Steps Overview

1. CD Pipeline Triggers Deployment: The continuous deployment pipeline starts the deployment process.

2. Ansible Control Node: The Ansible control node executes the deployment tasks.

3. Read Configuration Files: Reads `inventory.ini` for server details and `deploy.yml` for deployment instructions.

4. Connect via SSH: Connects securely to the target servers using SSH.

5. Prepare Target Server: Prepares the target server and required directories for deployment.

6. Copy Artifacts & Update Config: Copies build artifacts and updates the required configuration files.

7. Restart Application Services: Restarts the application services to apply the new changes.
---

# 10. Deployment Validation

Deployment validation is the final stage of the workflow.

After Ansible completes the deployment, the CD pipeline can perform checks such as:

<img width="387" height="862" alt="image" src="https://github.com/user-attachments/assets/537b17a3-a15e-4b42-b0b8-d429206b63b0" />

### Validation Steps Overview

1. Start Deployment Validation: The validation process begins after the deployment is completed.

2. Check Service Status: Verifies whether the required services are running properly.

3. Check Required Ports: Ensures that all required network ports are open and listening.

4. Run Application Health Checks: Checks the application's health and internal status.

5. All Checks Passed?: Verifies whether all validation checks are successful.
   - Yes: Deployment is marked as SUCCESS.
   - No: Deployment is marked as FAILED.

---
# 11. Advantages and Disadvantages

| Advantages | Disadvantages |
|---|---|
| Simple Setup: No database or complex daemon setup is required—just Python and SSH. | Performance at Extreme Scale: Executing tasks across thousands of servers can be slower compared to agent-based tools. |
| Highly Extensible: Provides thousands of modules for cloud providers, databases, and network devices. | No State Management: Unlike Terraform, Ansible does not maintain a native state file for infrastructure. |
| Secure by Design: Uses SSH keys and Ansible Vault to protect sensitive passwords and tokens. | Debugging Complexity: Troubleshooting nested variables or syntax errors in large playbooks can be challenging. |

---

# 12. Best Practices

* Store Playbooks in Git: Keep deployment automation under version control.
* Use Separate Inventories: Maintain separate inventories for different environments.
* Use Variables: Keep environment-specific values separate from Playbook logic.
* Protect Secrets: Use Ansible Vault or an approved secret-management solution for sensitive data.
* Use Idempotent Tasks: Ensure repeated Playbook execution produces the desired state without unnecessary changes.
* Validate Deployment: Perform service and health checks after deployment.
* Test Before Production: Validate the Playbook in development or staging before production deployment.
* Use `--check` Where Appropriate: Preview potential changes before applying them.

---
# 13. Conclusion

Ansible Playbooks streamline the Continuous Delivery pipeline by providing an automated, consistent, and repeatable approach to application deployment. By leveraging idempotent tasks, dynamic inventories, and strict validation, teams can significantly reduce manual effort and deployment errors. Ultimately, integrating Ansible ensures a faster, reliable, and highly maintainable software delivery process across all environments.

---
# 14. Contact Information

| **Name** | **Email**                                                                                     |
| -------- | --------------------------------------------------------------------------------------------- |
| Vineet   | [vineet.shrivastava.snaatak@mygurukulam.co](mailto:vineet.shrivastava.snaatak@mygurukulam.co) |

---

# 15. References

| **Description**                                                              | **Reference**                                                                                                            |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Official documentation for Ansible automation and Playbooks.                 | [Ansible Documentation](https://docs.ansible.com/)                                                                       |
| Official reference for creating and executing Playbooks.                     | [Ansible Playbooks](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html)                         |
| Official documentation for defining and managing hosts and groups.           | [Ansible Inventory](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)                        |
| Official documentation for protecting sensitive data.                        | [Ansible Vault](https://docs.ansible.com/ansible/latest/vault_guide/index.html)                                          |
| Reference material for automated software delivery and deployment practices. | [Continuous Delivery](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd/continuous-delivery.html) |
