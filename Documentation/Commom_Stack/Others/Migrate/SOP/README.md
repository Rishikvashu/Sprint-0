# SOP for Migrate

<p align="center">
<img width="607" height="341" alt="migration" src="https://github.com/user-attachments/assets/01e05aa5-c7c7-4582-99e5-9aacd04df56a" />
</p>

---


| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Mansoor Alam | 24-08-2026 | 1.0 | Mansoor Alam | 24-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |



## Introduction
This SOP provides a step-by-step guide to installing and using the golang-migrate tool.
It explains how database migrations are created, applied, and verified using migration files.
It also covers the process of managing database schema changes in a consistent and reliable way.

---

## Table of Contents

1. [What is migrate?](#what-is-migrate)
2. [Why migrate?](#why-migrate)
3. [Step by step installation guide](#step-by-step-installation-guide)
     - [Install go](#1-install-go)
     - [Install Migrate](#2-install-migrate)
     - [Verify installation](#3-verify-installation)
     - [Run Migrations](#4-run-migrations)
4. [Contacts](#contacts)
5. [References](#references)

---


## What is migrate?
Migrate is a versatile command-line tool used to manage database schema migrations. It allows you to evolve your database schema over time in a structured and organized way. Instead of manually altering your database structure, you write migrations as code, which can then be applied to any database environment. This ensures consistency and simplifies database updates, especially in complex or collaborative projects.

## Why migrate?
Migrate helps you manage database schema changes in a version-controlled way, ensuring consistency across different environments.  It automates database updates, making them reliable and reproducible.



## Step by step installation guide

### Step 1: Update Package Index

```
sudo apt update
```

### Step 2: Install Go & Verify 
Go is a prerequisite for installing and using the migrate CLI.
```
sudo apt install golang-go -y
go version
```
<img width="1144" height="130" alt="img1" src="https://github.com/user-attachments/assets/11cfd584-1274-4495-9a53-b34df76a549f" />

### Step 3: Download Migrate

```
curl -L https://github.com/golang-migrate/migrate/releases/download/v4.15.2/migrate.linux-amd64.tar.gz | tar xvz
ls -lh migrate
```
<img width="1363" height="177" alt="img2" src="https://github.com/user-attachments/assets/edf2b59b-b94c-4116-90d9-1b197903f8e8" />

### Step 4: Install Migrate Binary
Move the migrate binary to /usr/local/bin/

```
sudo mv migrate /usr/local/bin/migrate
```
- /usr/local/bin is commonly used for manually installed system-wide command-line programs.
- Check whether the binary is available:

```
which migrate
migrate --version
```

<img width="1075" height="93" alt="migrate version" src="https://github.com/user-attachments/assets/62fd15f0-e12e-4050-8307-99be0409ac85" />


### Step 5: Run Migrations
After setting up the database and migration files for the database, use the migrate command with the -path (location of your migrations) and -database (your connection string) flags.  It's best to use an environment variable to store the connection string.

```bash
make run-migrations
```

<img width="1094" height="71" alt="img5" src="https://github.com/user-attachments/assets/b92c9041-aabb-4bf7-87b2-4402b18c9360" />

### Step 6: Verify Migration Status
Check the current migration version

Syntax
```
migrate -path migrations -database "$DATABASE_URL" version
```

<img width="1197" height="58" alt="img6" src="https://github.com/user-attachments/assets/dcf8c6bd-919c-4508-93a8-2e9a9fd49443" />

---


## Conclusion

This SOP provides a step-by-step guide to installing and using the `golang-migrate` tool on Ubuntu. It covers the installation and verification of Go and migrate, along with using the existing migration files of the Employee API to apply database changes. By following this process, we can ensure that database schema changes are managed in a consistent, controlled, and reliable way.

## Contacts

| Name            | Email Address                                 |
|-----------------|-----------------------------------------------|
| Mansoor Alam | mansoor.alam.snaatak@mygurukulam.co        |

---

## References

| **Title**                              | **Link**                                                                                      |
|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Migrate Command-Line Usage             |        https://dev.to/wiliamvj/using-migrations-with-golang-3449        |
