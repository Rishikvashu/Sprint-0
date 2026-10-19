# Comman Stack | Ansible | Playbook | SOP

<p align="center">
  <img width="240" height="110" alt="Ansible" src="https://upload.wikimedia.org/wikipedia/commons/2/24/Ansible_logo.svg" />
</p>

---

# Author Table

| **Author**    | **Created On** | **Version** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ------------- | -------------- | ------------ | ------------------ | --------------- | --------------- | --------------- |
| Anshul Kotiya | 31-08-2026     | 1.1   | 07-09-2026         | Shubham Rathi   | Shreya / Nikita | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [What is an Ansible Playbook](#3-what-is-an-ansible-playbook)
4. [Prerequisites](#4-prerequisites)
5. [Required Inputs](#5-required-inputs)
6. [Playbook Structure](#6-playbook-structure)
7. [Practical Playbook Execution](#7-practical-playbook-execution)

   * [7.1 Create the Working Directory](#71-create-the-working-directory)
   * [7.2 Create the Inventory](#72-create-the-inventory)
   * [7.3 Verify Inventory](#73-verify-inventory)
   * [7.4 Test Host Connectivity](#74-test-host-connectivity)
   * [7.5 Create the Playbook](#75-create-the-playbook)
   * [7.6 Validate Playbook Syntax](#76-validate-playbook-syntax)
   * [7.7 Run Check Mode](#77-run-check-mode)
   * [7.8 Execute the Playbook](#78-execute-the-playbook)
   * [7.9 Validate the Result](#79-validate-the-result)
8. [Execution Result](#8-execution-result)
9. [Common Troubleshooting](#9-common-troubleshooting)
10. [Best Practices](#10-best-practices)
11. [Recommendation / Conclusion](#11-recommendation--conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

This Standard Operating Procedure (SOP) provides a step-by-step process for executing an Ansible Playbook in a controlled and reliable manner.

---

# 2. Purpose

The purpose of this SOP is to establish a standard procedure for executing Ansible Playbooks and validating the expected results.

This SOP helps ensure that:
* The correct target hosts are selected.
* Required inputs are available.
* Connectivity is verified before execution.
* Playbook syntax is checked before applying changes.
* Changes can be reviewed before execution where applicable.
* Execution results are properly reviewed.
* The final system state is validated.

---

# 3. What is an Ansible Playbook

An **Ansible Playbook** is a YAML file that defines the tasks Ansible should perform on one or more managed hosts.

A playbook normally specifies:

* Target hosts
* Tasks
* Ansible modules
* Privilege requirements
* Handlers

For example:

```yaml
---
- name: Configure Web Server
  hosts: webservers
  become: true

  tasks:
    - name: Ensure nginx is installed
      ansible.builtin.apt:
        name: nginx
        state: present
```

In this example:

* `hosts` defines where the playbook will run.
* `become` allows privilege escalation when required.
* `tasks` contains the operations to perform.
* `ansible.builtin.apt` manages the Nginx package.

---

# 4. Prerequisites

Before executing a playbook, verify the following requirements.

| Requirement              | Description                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **Ansible**              | Ansible must be installed on the control node.                                                                      |
| **Python**               | A compatible Python interpreter must be available on the managed host for the Ansible modules used by the playbook. |
| **Playbook**             | A valid Ansible Playbook must be available.                                                                         |
| **Inventory**            | The target host must be defined in the inventory.                                                                   |
| **SSH Access**           | SSH connectivity and authentication to the target host must be configured.                                          |
| **Required Permissions** | The user must have sufficient privileges to perform the tasks defined in the playbook.                              |


### Verify Ansible Installation

Run:

```bash
ansible --version
```

Confirm that Ansible is installed and the expected version is displayed.

---

# 5. Required Inputs 

| Category |	Required Input |	Purpose	| Example |
|----------|-----------------|----------|---------|
| Inventory | IP |	To identify the target server	|51.20.85.75 |
| Inventory |	Group Name |	To group servers together |	webservers |
| Inventory	| SSH User	| To log in to the server	| ubuntu |
| Inventory	| SSH Key |	For authentication	| Public key |
| Playbook	| Hosts	| Which server/group the playbook will run |	webservers |
| Playbook	| Tasks	| What operation needs to be performed	| Install Nginx |
| Playbook	| Modules	| To execute the operation |	apt, copy, service |
| Playbook	| Become	| For sudo/root permission	| become: yes |


---

# 6. Playbook Structure

A basic Ansible Playbook can be understood using the following structure:

```text
Playbook
   |
   +-- Play
       |
       +-- name
       +-- Hosts
       +-- Tasks
             |
             +-- Task
             +-- Task
             +-- Task
```

| **Component** | **Purpose**                                                                        |
| ------------- | ---------------------------------------------------------------------------------- |
| **Playbook**  | YAML file containing the automation instructions.                                  |
| **Play**      | Defines what should be performed on selected hosts.                                |
| **Hosts**     | Specifies the target hosts or inventory group.                                     |
| **Variables** | Stores values required by the playbook.                                            |
| **Tasks**     | Defines individual operations.                                                     |
| **Modules**   | Perform specific operations such as package, service, file, or command management. |
| **Handlers**  | Run specific actions when notified by a task, such as restarting a service.        |

---

# 7. Practical Playbook Execution

This section demonstrates a basic end-to-end Ansible Playbook execution.

The example installs Nginx on the target server and ensures that the service is running.

## 7.1 Create the Working Directory

Create a separate directory for the Ansible files:

```bash
mkdir ansible-sop
cd ansible-sop
```

The directory will contain the inventory and private Key of node.

Expected structure:

```text
ansible-playbook-demo/
├── inventory
└── demo_key.pem
```



<img width="768" height="170" alt="Screenshot 2026-08-31 200534" src="https://github.com/user-attachments/assets/76bf6128-610c-414c-86fd-9a40f556d5cc" />


---

## 7.2 Create the Inventory

Create an inventory file:

```bash
nano inventory
```

Add the target server:

```
[webserver]
server1 ansible_host=<SERVER_IP> ansible_user=ubuntu ansible_ssh_private_key_file=PATH/TO/PRIVATE_KEY
```

Replace `<SERVER_IP>` with the IP address of the server on which the playbook should run.

Save the file after adding the required host.



<img width="1357" height="137" alt="Screenshot 2026-08-31 202024" src="https://github.com/user-attachments/assets/d59e3b36-97d1-4e0a-b1d4-309ab69e383b" />


---

## 7.3 Verify Inventory

Before running the playbook, verify that Ansible can read the inventory correctly.

Run:

```bash
ansible-inventory -i inventory --list
```

Review the output and confirm that the expected host is present under the correct group.

This step helps prevent accidental execution against an incorrect or incomplete inventory.




<img width="1175" height="615" alt="Screenshot 2026-08-31 204401" src="https://github.com/user-attachments/assets/fe0c95fc-649c-494e-9df3-8f3b4689809f" />


---

## 7.4 Test Host Connectivity

Test connectivity between the Ansible control node and the managed host:

```bash
ansible webserver -i inventory -m ping
```

A successful response should contain:

```text
"ping": "pong"
```

This confirms that Ansible can communicate with the target host.

If the host is unreachable, resolve the connectivity or authentication issue before continuing.



<img width="1651" height="380" alt="Screenshot 2026-08-31 202002" src="https://github.com/user-attachments/assets/ad9b0bb5-6a8e-47e4-aff7-0b28fa971861" />


---

## 7.5 Create the Playbook

Create the playbook:

```bash
nano test.yml
```

Add the following content:

```yaml
---
- name: Configure Web Server
  hosts: webservers
  become: true

  tasks:
    - name: Install nginx
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: true

    - name: Ensure nginx is running
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true
```

This playbook performs two main operations:

1. Installs Nginx if it is not already installed.
2. Ensures that the Nginx service is running and enabled.




<img width="957" height="616" alt="Screenshot 2026-08-31 202521" src="https://github.com/user-attachments/assets/9dfa0557-e73d-40fe-b5fe-5d78d8d59939" />


---

## 7.6 Validate Playbook Syntax

Before applying any changes, validate the playbook syntax:

```bash
ansible-playbook -i inventory test.yml --syntax-check
```

If the syntax is correct, Ansible reports that the playbook syntax is valid.

### Why This Step is Required

A syntax check helps identify YAML or playbook structure errors before the playbook is executed.

**Note:** A successful syntax check does not guarantee successful execution. Connectivity, permissions, variables, and target-system conditions must also be valid.




<img width="1307" height="203" alt="Screenshot 2026-08-31 202649" src="https://github.com/user-attachments/assets/0025a75e-3c65-4b77-91fd-332b15fae46e" />



---

## 7.7 Run Check Mode

Where supported, use check mode to preview the expected changes:

```bash
ansible-playbook -i inventory test.yml --check
```

Review the output before performing the actual execution.

Check mode helps identify what Ansible expects to change without normally applying those changes.

**Note:** Not every Ansible module can fully simulate its actions in check mode.

---

## 7.8 Execute the Playbook

After completing the required checks, execute the playbook:

```bash
ansible-playbook -i inventory test.yml
```

During execution, review the output for:

* `ok`
* `changed`
* `skipped`
* `failed`
* `unreachable`

A successful execution should complete without unexpected `failed` or `unreachable` results.



<img width="1657" height="512" alt="Screenshot 2026-08-31 202929" src="https://github.com/user-attachments/assets/b7a88ca2-9f16-462d-8f3c-07e3dcd9e060" />


---

## 7.9 Validate the Result

After the playbook completes successfully, verify that Nginx is running:

```bash
ansible webserver -i inventory -m command -a "systemctl is-active nginx"
```

The expected result is:

```text
active
```



<img width="1491" height="230" alt="Screenshot 2026-08-31 203115" src="https://github.com/user-attachments/assets/71bc5aab-ad06-489d-b897-a4ba9c038f60" />



This confirms that the intended service state has been achieved.

You can also verify the service directly on the target server:


```bash
systemctl status nginx
```

The service should show an active/running state.



<img width="1920" height="1140" alt="Screenshot 2026-08-31 203141" src="https://github.com/user-attachments/assets/02bcf173-f863-48d7-8277-f4d45c76470f" />


---

# 8. Execution Result

Ansible provides a summary at the end of playbook execution.

A typical summary contains values such as:

```text
PLAY RECAP
server1 : ok=2 changed=1 unreachable=0 failed=0 skipped=0
```

The values indicate the result of task execution:

| **Status**      | **Meaning**                                              |
| --------------- | -------------------------------------------------------- |
| **ok**          | Task completed successfully without making a change.     |
| **changed**     | Task completed successfully and made a change.           |
| **skipped**     | Task was not executed because its condition was not met. |
| **failed**      | Task could not be completed successfully.                |
| **unreachable** | Ansible could not establish communication with the host. |

---

# 9. Common Troubleshooting

| **Issue**              | **Possible Cause**                                   | **Recommended Action**                                                   |
| ---------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------ |
| **Host Unreachable**   | Network or SSH connectivity issue.                   | Verify the host address, network connectivity, and SSH access.           |
| **Permission Denied**  | Insufficient user privileges.                        | Verify user permissions and use privilege escalation when required.      |
| **Syntax Error**       | Invalid YAML or playbook structure.                  | Run `ansible-playbook --syntax-check` and correct the reported error.    |
| **Undefined Variable** | Required variable is missing or incorrectly defined. | Check the playbook, inventory, and variable files.                       |
| **Task Failed**        | Incorrect configuration or target-system issue.      | Review the error message and verify the affected task and target system. |

---
# 10. Best Practices

| **Best Practice**           | **Description**                                                              |
| --------------------------- | ---------------------------------------------------------------------------- |
| **Verify Inventory**        | Confirm that the playbook targets the intended hosts.                        |
| **Test Connectivity**       | Check host connectivity before executing configuration tasks.                |
| **Validate Syntax**         | Run a syntax check before applying changes.                                  |
| **Review Before Execution** | Use check mode where applicable to review expected changes.                  |
| **Validate Results**        | Confirm that the intended changes were successfully applied after execution. |

---

# 11. Recommendation / Conclusion

Ansible Playbooks should be executed using a consistent process that includes **input verification, connectivity testing, syntax validation, controlled execution, and result validation**.
Following this SOP helps reduce execution errors, maintain consistency, and ensure that automated changes produce the expected system state.

---

# 12. Contact Information

| **Name**      | **Email**   |
| ------------- | ----------- |
| Anshul Kotiya |  anshul.kotiya.snaatak@mygurukulam.co |

---

# 13. References

| **Reference**                                                                                                                              | **Description**                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| [Ansible Playbooks Documentation]( https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_intro.html )   | Official documentation for understanding Ansible Playbooks and their structure. |
|    |     |
---
