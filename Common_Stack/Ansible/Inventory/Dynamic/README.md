## Common Stack | Ansible | Inventory | Dynamic

<p align="center">
<img width="full" height="full" alt="image" src="https://img.shields.io/badge/Ansible-Dynamic%20Inventory-blue" />

</p>

##  Author Table

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Arjun | 24-08-2026 | v1.1    | Arjun           | 24-08-2026     |       Team      |      Rajnish sharma      | Pritam/Komal           |     Abhsihek/Manish Nautiyal       |

## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Ansible Inventory?](#2-what-is-ansible-inventory)  
3. [Static vs Dynamic Inventory](#3-static-vs-dynamic-inventory)  
4. [How Dynamic Inventory Works](#4-how-dynamic-inventory-works)  
5. [AWS EC2 Dynamic Inventory](#5-aws-ec2-dynamic-inventory)  
6. [Prerequisites](#6-prerequisites)
7. [Dynamic Inventory Configuration](#7-dynamic-inventory-configuration)  
8. [Testing Inventory](#8-testing-inventory)  
9. [Best Practices](#9-best-practices)
10. [Advantages and Disadvantages](#10-advantages-and-disadvantages)   
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)



## 1. Introduction

This document explains how Ansible inventory works, focusing on dynamic inventory.

It covers:
- Inventory basics  
- Static vs dynamic approach  
- AWS-based inventory  
- Testing and best practices  

Goal: Automatically manage servers without manual updates.



## 2. What is Ansible Inventory?

An Ansible inventory is a list of machines that Ansible manages.

| Part | Meaning |
|------|--------|
| Host | Server IP or hostname |
| Group | Logical grouping (e.g., api, db) |
| Variables | Connection details (user, key) |

Ansible uses inventory before running any playbook.



## 3. Static vs Dynamic Inventory

| Feature | Static | Dynamic |
|--------|--------|---------|
| Definition | Manual file | Auto-generated |
| Updates | Manual | Automatic |
| Cloud Support | Good | Excellent |
| Scaling | Hard | Easy |
| Best Use | Small setups | Cloud / large infra |

Dynamic inventory is preferred for modern systems.



## 4. How Dynamic Inventory Works

Steps:

1. Ansible calls inventory plugin  
2. Plugin queries AWS API  
3. AWS returns host details  
4. Ansible runs playbook on hosts  

Flow:

<img width="2055" height="665" alt="image" src="https://github.com/user-attachments/assets/f6705d8d-137d-4db6-9718-06ccfe28afaf" />




## 5. AWS EC2 Dynamic Inventory

Uses `amazon.aws.aws_ec2` plugin.

Instances are grouped using tags.

| Tag | Purpose |
|-----|--------|
| Service | Application name |
| Environment | dev / staging / prod |



## 6. Prerequisites

Before configuring AWS EC2 Dynamic Inventory, ensure the following are available:

- Ansible installed on the control node.
- AWS CLI installed and configured.
- Valid AWS credentials with EC2 read permissions.
- `amazon.aws` Ansible collection installed.
- Python `boto3` and `botocore` packages installed.
- At least one running EC2 instance in the configured AWS region.
- SSH access to the EC2 instance.

**Verify Installation**

```bash
ansible --version
aws --version
aws sts get-caller-identity
```

**Install Required Dependencies**

```bash
ansible-galaxy collection install amazon.aws
python3 -m pip install boto3 botocore
```

The AWS credentials should not be hardcoded in the inventory file or committed to Git.



## 7. Dynamic Inventory Configuration

File: inventories/aws_ec2.yml

```yaml
plugin: amazon.aws.aws_ec2

regions:
  - ap-south-1

filters:
  instance-state-name: running

keyed_groups:
  - key: tags.Service
    prefix: service
  - key: tags.Environment
    prefix: env

compose:
  ansible_host: private_ip_address
  ansible_user: ubuntu
```

| Field | Meaning |
|-------|--------|
| plugin | AWS EC2 plugin |
| regions | AWS region |
| filters | Only running instances |
| keyed_groups | Group by tags |
| compose | Set connection details |



## 8. Testing Inventory

| Command | Purpose |
|---------|--------|
| ansible-inventory --list | Show all hosts |
| ansible-inventory --graph | Show groups |
| ansible -m ping | Test connectivity |

Always verify inventory before running playbooks.


## 9. Best Practices

| Practice | Reason |
|----------|-------|
| Use tags | Enables grouping |
| Avoid hardcoding credentials | Improves security |
| Test with --list | Prevent errors |
| Use private IPs | Reliable connectivity |
| Keep naming consistent | Easy management |

## 10. Advantages and Disadvantages

### Advantages

| Advantage | Description |
|-----------|-------------|
| Automatic Updates | Inventory is automatically updated when infrastructure changes. |
| Easy Scaling | New instances can be discovered without manually updating inventory files. |
| Cloud Integration | Integrates directly with cloud platforms such as AWS. |
| Tag-Based Grouping | Hosts can be automatically grouped using instance tags. |
| Reduced Manual Work | Eliminates repetitive inventory maintenance. |
| Improved Accuracy | Reduces errors caused by outdated or manually maintained host lists. |

### Disadvantages

| Disadvantage | Description |
|--------------|-------------|
| Cloud Dependency | Requires access to the cloud provider API for dynamic discovery. |
| API Dependency | Inventory generation can fail if the cloud API is unavailable. |
| Credential Management | Requires secure configuration of cloud credentials and permissions. |
| Initial Configuration | Plugin configuration requires more setup compared to a simple static inventory. |
| Debugging Complexity | Troubleshooting inventory issues can be more difficult than with static files. |
| API Rate Limits | Frequent inventory queries may be affected by cloud API rate limits. |




## 11. Conclusion

Dynamic inventory makes Ansible scalable and reliable.

- No manual updates  
- Always accurate  
- Works well with cloud

## 12. Contact Information

| Name           | Email ID |
|----------------|----------|
| Arjun Kumar  | arjun.kumar.snaatak@mygurukulam.co |



## 13. References

| Description | Link |
|-------------|------|
| Official guide for managing Ansible inventory | [Ansible Inventory Guide](https://docs.ansible.com/ansible/latest/inventory_guide/) |
| AWS EC2 dynamic inventory plugin documentation | [AWS EC2 Plugin](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws_ec2_inventory.html) |
