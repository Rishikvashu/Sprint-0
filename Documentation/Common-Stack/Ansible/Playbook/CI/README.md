# Ansible Playbook CI | Documentation
<img width="240" height="240" alt="icons8-ansible-240" src="https://github.com/user-attachments/assets/ca4bc43a-1e60-4aa1-ad93-1a8db8d65daf" />

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------ | --------------- | --------------- | --------------- |
| Vashishtha Prakash | 31-08-2026     | v1.3         | 06-10-2026         | Sunny/Shubhan   | Shreya/Nikita   | Piyush Upadhyay|


---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Ansible Playbook CI](#2-what-is-ansible-playbook-ci)
3. [Why Ansible Playbook CI is Required](#3-why-ansible-playbook-ci-is-required)
4. [Ansible Playbook CI Workflow](#4-ansible-playbook-ci-workflow)
5. [Recommendation / Conclusion](#5-recommendation--conclusion)
6. [Contact Information](#6-contact-information)
7. [References](#7-references)

---

# 1. Introduction

This documentation is about implementing an Ansible Playbook using CI process.

---

# 2. What is Ansible Playbook CI

Ansible Playbook CI is the integration of Ansible Playbook validation into a Continuous Integration pipeline. 

---

# 3. Why Ansible Playbook CI is Required

Ansible Playbook CI is required to improve the reliability, consistency, and quality of infrastructure automation. Manual execution of Ansible Playbooks can introduce several problems. Following is the table for such problems and their solutions:

---

# 4. Ansible Playbook CI Workflow

<img width="1538" height="2664" alt="image" src="https://github.com/user-attachments/assets/e10cb0af-e8f0-460b-8587-c6addc63f4a2" />

---

### Workflow Steps 


| # | Step | Tool / Command | What it does | On failure |
|---|------|----------------|--------------|------------|
| 1 | Trigger | Git push / Pull Request | Starts the pipeline automatically when a developer pushes code or opens a PR. | N/A |
| 2 | Checkout | `git` (e.g. `actions/checkout`) | Pulls the latest code of the branch or PR onto the CI runner. | Pipeline stops; check repo access and branch name. |
| 3 | YAML lint | `yamllint .` | Checks YAML formatting: indentation, trailing spaces, line length, duplicate keys. | Fix the reported file and line, then push again. |
| 4 | Ansible lint | `ansible-lint` | Checks Ansible best practices: task names, FQCN module names, `changed_when`, file permissions, risky `shell`/`command` use. | Fix the violated rule and push again. |
| 5 | Syntax check | `ansible-playbook -i <inventory> <playbook>.yml --syntax-check` | Confirms Ansible can parse the playbook. Nothing is executed. | Fix the parse error (unknown keyword, bad include/import). |
| 6 | Molecule test | `molecule test` | Runs the role or playbook in a temporary container or VM. Includes an idempotence check (second run must show `changed=0`) and verification of the result. | Fix the failing task, idempotence issue or verify assertion. |
| 7 | Dry run | `ansible-playbook -i <inventory> <playbook>.yml --check --diff` | Simulates the run and shows what would change, without applying any change. | Review the diff and fix unexpected changes. |
| 8 | Secret scan | `gitleaks detect --source .` | Detects hardcoded passwords, API keys and tokens in the repository. | Remove the secret, move it to Ansible Vault, and rotate the leaked credential. |
| 9 | Notify | PR status check, Slack / email | Reports the pipeline result to the developer on the PR or in chat. | N/A |
| 10 | Result check | Pipeline status | Evaluates whether all previous checks passed. | Go to step 12 if any check failed. |
| 11 | Pipeline passed | N/A | All checks succeeded. | N/A |
| 12 | Pipeline failed | N/A | At least one check failed. The developer fixes the issue and pushes again, which restarts the pipeline from step 1. | N/A |


---

# 5. Conclusion

Jenkins with Ansible and Ansible Lint is recommended for implementing Ansible Playbook CI. The combination provides a structured validation process before infrastructure changes are applied.

---

# 6. Contact Information

| **Name**             | **Email** |
| --------------------- | ---------- |
| Vashishtha Prakash | vashishtha.prakash.snaatak@mygurukulam.co |

---

# 7. References

| **Topic**                                                                                           | **Description**                                         |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| [Ansible Documentation](https://docs.ansible.com/)                                                      | Official documentation for Ansible.                     |
| [Ansible Playbook Documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks.html) | Official documentation for Ansible Playbooks.           |
| [Ansible Lint Documentation](https://ansible.readthedocs.io/projects/lint/)                             | Documentation for Ansible Lint and Playbook validation. |
| [Jenkins Documentation](https://www.jenkins.io/doc/)                                                    | Official documentation for Jenkins CI/CD.               |
| [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)                             | Official documentation for Jenkins Pipeline.            |
| [GitHub Documentation](https://docs.github.com/)                                                        | Documentation for GitHub source code management.        |
| [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)                                               | Official documentation for Amazon EC2.                  |
| [OpenSSH Documentation](https://www.openssh.com/manual.html)                                            | Documentation for OpenSSH and SSH-based connectivity.   |

---
