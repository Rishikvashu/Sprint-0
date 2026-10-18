# JQ Documentation
<img width="268" height="137" alt="image" src="https://github.com/user-attachments/assets/b7e6c6d8-3bfb-48c0-8963-0b9821eaffb1" />

---

# Author Table

| **Author**         | **Created On** | **Version** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ------------------ | -------------- | ----------- | ------------------ | --------------- | --------------- | --------------- |
| Vashishtha Prakash | 31-08-2026     | v1.3         | 09-09-2026         | Sunny/Shubhan   | Shreya/Nikita   | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is JQ](#2-what-is-jq)
3. [Why JQ is Required](#3-why-jq-is-required)
4. [Key Features](#4-key-features)
5. [Conclusion](#7-conclusion)
6. [Contact Information](#8-contact-information)
7. [References](#9-references)

---

# 1. Introduction

This documentation is designed to provide a basic understanding of JQ, including what JQ is, why it is required, its key features..

---

# 2. What is JQ

JQ (`jq`) is a lightweight and flexible command-line JSON processor used to **parse, filter, search, extract, transform, and manipulate JSON data** directly from the terminal.

The basic syntax is:

```bash
jq '<filter>' <input-file>
```

For example:

```bash
jq '.name' employee.json
```

---
# 3. Why JQ is Required

Modern applications, cloud platforms and APIs frequently generate structured JSON output. These responses can contain hundreds or thousands of lines, making it difficult to manually find and extract the specific information required by an engineer.

For example, the AWS CLI command:

```bash
aws ec2 describe-instances
```

can return a large JSON response containing details about multiple EC2 instances. If we only need the instance IDs, processing the complete response manually is unnecessary and inefficient. JQ solves this problem by allowing us to **filter, extract, transform, and process JSON data directly from the command line**.

For example:

```bash
aws ec2 describe-instances \
  | jq -r '.Reservations[].Instances[].InstanceId'
```

This command extracts only the EC2 instance IDs from the AWS JSON response, making the output easier to read and use in scripts or automation.

---

# 4. Key Features

| **Feature**                  | **Description**                                               |
| ---------------------------- | ------------------------------------------------------------- |
| **JSON Parsing**             | Reads and interprets structured JSON input.                   |
| **Field Extraction**         | Extracts specific fields or values from JSON objects.         |
| **Filtering**                | Selects JSON objects or values based on specified conditions. |
| **Array Processing**         | Processes individual elements of JSON arrays.                 |
| **Nested Data Access**       | Allows access to deeply nested JSON objects and fields.       |
| **Transformation**           | Creates new JSON structures from existing data.               |
| **Pipe Operations**          | Combines multiple filters using the `\|` operator.            |
| **Raw Output**               | Uses `-r` to produce shell-friendly string output.            |

---

# 5. Conclusion

JQ saves time and extra efforts by making it easy for the developers to search for a particular entry by just writing some JQ queries with required filters. 

---

# 6. Contact Information

| **Name**           | **Email**                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------- |
| Vashishtha Prakash | [vashishtha.prakash.snaatak@mygurukulam.co](mailto:vashishtha.prakash.snaatak@mygurukulam.co) |

---

# 7. References

| **Topic**                                            | **Description**                                                                            |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [JQ Official Documentation](https://jqlang.org/)     | Official JQ website and documentation.                                                     |
| [JQ Tutorial](https://jqlang.org/tutorial/)          | Official tutorial covering JQ fundamentals and practical usage.                            |
| [JQ Manual](https://jqlang.org/manual/)              | Official reference for JQ filters, functions, operators, command-line options, and syntax. |
| [JQ GitHub Repository](https://github.com/jqlang/jq) | Official source repository for the JQ implementation.                                      |
| [JQ Download](https://jqlang.org/download/)          | Official installation and download resources for different platforms.                      |
| [JQ Releases](https://github.com/jqlang/jq/releases) | Official JQ release history and release assets.                                            |
