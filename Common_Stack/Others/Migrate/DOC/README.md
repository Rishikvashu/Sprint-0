# Migrate Documentation

---

## Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **PRE Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Arjun | 24-08-2026 | v1.1 | Arjun | 16-09-2026 | Team | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Migrate](#2-what-is-migrate)
3. [Why Migrate](#3-why-migrate)
4. [Key Features](#4-key-features)
5. [Summary](#5-summary)
6. [Contact Information](#6-contact-information)
7. [References](#7-references)

---

## 1. Introduction

Database schemas change frequently as applications evolve. New features may require creating tables, adding columns, modifying existing columns, creating indexes, or changing database structures.

Managing these changes manually can result in inconsistencies between development, testing, staging, and production environments.

**Migrate** provides a structured and version-controlled approach for managing database schema changes through migration files.

---

## 2. What is Migrate

**Migrate** is a database migration tool written in Go that manages changes to database schemas.

It allows developers to define database changes using versioned migration files and apply those changes to a database in a controlled order.

A migration commonly consists of two files:

```text
000001_create_users_table.up.sql
000001_create_users_table.down.sql
```

### Up Migration

The `.up.sql` file contains the changes that are applied to the database.

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

### Down Migration

The `.down.sql` file contains the operation used to revert the migration when required.

```sql
DROP TABLE users;
```

Migrate can be used through its Command Line Interface (CLI) or integrated into Go applications as a library.

---

## 3. Why Migrate

Database changes need to be controlled, repeatable, and traceable across different environments. Migrate helps manage database changes in a consistent manner by storing them as version-controlled migration files.

| Reason | Description |
| :--- | :--- |
| Version Control | Database changes can be stored and tracked using Git along with application code. |
| Consistency | The same migration files can be applied across development, testing, staging, and production environments. |
| Controlled Changes | Database changes are executed in a defined and ordered sequence. |
| Rollback Support | Down migrations can be used to revert changes when appropriate. |
| Automation | Migration commands can be integrated into CI/CD pipelines. |
| Version Tracking | The current migration version of the database can be checked. |
| Repeatability | The same migration process can be reproduced across environments. |

---

## 4. Key Features

| Feature | Description |
| :--- | :--- |
| Versioned Migrations | Assigns versions to database changes so migrations can be applied in the correct order. |
| Up and Down Migrations | Supports applying database changes and reverting migrations using separate migration files. |
| Multiple Database Support | Supports multiple database systems through database drivers. |
| CLI Support | Provides commands to create, apply, revert, and inspect migrations. |
| Migration Version Tracking | Allows users to check the current migration version of a database. |
| Multiple Migration Sources | Supports different sources for storing and loading migration files. |
| Go Library | Can be integrated directly into Go applications. |
| CI/CD Integration | Can be incorporated into automated deployment workflows. |

---

## 5. Summary

Migrate provides a structured approach for managing database schema changes.

It helps teams to:

- Track database changes using version control.
- Maintain consistency across different environments.
- Apply database changes in a controlled order.
- Revert migrations when required.
- Track the current database migration version.
- Integrate database migrations into CI/CD workflows.

Migrate makes database schema changes more manageable, repeatable, and traceable throughout the application lifecycle.

---

## 6. Contact Information

| Name | Email ID |
| :--- | :--- |
| Arjun Kumar | arjun.kumar.snaatak@mygurukulam.co |

---

## 7. References

| Topic | Link |
| :--- | :--- |
| Official Migrate Repository | [golang-migrate/migrate](https://github.com/golang-migrate/migrate) |
| Migrate CLI Documentation | [Migrate CLI](https://github.com/golang-migrate/migrate/tree/master/cmd/migrate) |
| Migrate Documentation | [Migrate Documentation](https://pkg.go.dev/github.com/golang-migrate/migrate/v4) |
