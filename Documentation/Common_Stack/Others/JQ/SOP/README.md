# JQ JSON Processor Documentation(SOP)

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer**            |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | -------------------------- |
| Vineet     | 28-08-2026     | 1.1         | Vineet              | 05-09-2026         | Aryan Mishra    |      Aditya Raj Singh     | |
| Vineet     | 28-08-2026     | 1.2        | Vineet              | 11-09-2026         | Aryan Mishra    | Aditya Raj Singh   |  |
| Vineet     | 28-08-2026     | 1.3        | Vineet              | 17-09-2026         | Aryan Mishra    | Aditya Raj Singh   |  |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is JQ](#2-what-is-jq)
3. [Why use JQ](#3-why-use-jq)
4. [Features](#4-features)
5. [JQ Processing Workflow](#5-jq-processing-workflow)
6. [Prerequisites](#6-prerequisites)
7. [JQ Installation](#7-jq-installation)
8. [JQ Configuration and Basic Usage](#8-jq-configuration-and-basic-usage)
9. [Validation](#9-validation)
10. [Troubleshooting](#10-troubleshooting)
11. [Advantages and Disadvantages](#11-advantages-and-disadvantages)
12. [Best Practices](#12-best-practices)
13. [Conclusion](#13-conclusion)
14. [Contact Information](#14-contact-information)
15. [References](#15-references)

---

# 1. Introduction

This SOP covers JQ installation, verification, basic usage, validation, troubleshooting, and best practices on Ubuntu-based systems such as **WSL and AWS EC2**. It provides a standardized procedure for using JQ in shell scripts and DevOps automation.

---
# 2. What is JQ

**JQ** is often described as the "sed for JSON." It is a flexible, lightweight, and highly capable command-line tool that allows you to slice, filter, map, and transform structured JSON data effortlessly. Instead of writing complex scripts to extract a single value from an API response, JQ allows you to retrieve it with a single command.

---

# 3. Why use JQ

In modern DevOps and Cloud environments, almost all APIs and configuration files communicate in JSON. JQ is required to:
* **Automate JSON Parsing:** Easily extract dynamic IP addresses, instance IDs, or deployment statuses from cloud provider outputs.
* **Format Data:** Beautify raw, unreadable JSON outputs into structured, color-coded, and human-readable formats.
* **Integrate with Shell Scripts:** Seamlessly pipe JSON data from `curl` commands directly into bash variables without external dependencies.

---
# 4. Features

| Feature | Description |
|---|---|
| **Zero Dependencies** | JQ is available as a lightweight, standalone command-line tool and does not require a separate runtime environment or complex dependency setup for basic JSON processing. |
| **Powerful Query Language** | JQ provides a flexible query language that supports filtering, mapping, selecting specific fields, transforming data, and working with complex JSON structures. |
| **Stream Processing** | JQ supports streaming JSON data, allowing large JSON inputs to be processed efficiently without requiring the complete data structure to be handled at once. |
| **Built-in Functions** | JQ provides built-in functions for mathematical calculations, string manipulation, array and object processing, conditional operations, and regular expression handling. |
---
# 5. JQ Processing Workflow

The following diagram represents the standard workflow of how JQ processes and filters JSON data in a pipeline.
<img width="862" height="181" alt="image" src="https://github.com/user-attachments/assets/c2a969b1-eba7-4e1b-857d-6c7f1ba0c6e7" />
### JQ Workflow Steps

1. Raw JSON Input / API Response: JQ first receives raw JSON data from an API response, JSON file, command output, or another input source. This data acts as the input for further processing.

2. JQ Command Line: The JSON data is passed to the JQ command through the command line or a UNIX pipe. JQ reads the input and prepares it for processing based on the specified filter.

3. Apply Filter: JQ applies the required filter to select specific data from the JSON input. Filters such as `.name`, `.department`, or other field expressions can be used to extract the required information.

4. Transform / Map Data: After selecting the required data, JQ can transform, map, filter, or restructure the JSON data according to the requirement. This step is useful for preparing data in the required format.

5. Formatted Structured Output: Finally, JQ generates clean and structured output. The processed data can be displayed on the terminal, passed to another command, stored in a file, or used further in automation and DevOps workflows.
---
# 6. Prerequisites

| **Prerequisite** | **Details**                                |
| ---------------- | ------------------------------------------ |
| OS & Access      | Ubuntu-based system such as WSL or AWS EC2 |
| Package          | `jq`                                       |
| Permissions      | `sudo/root` where required                 |

---

# 7. JQ Installation

### Step 1: Update Packages

```bash
sudo apt update
```

### Step 2: Install JQ

```bash
sudo apt install -y jq
```
<img width="1920" height="231" alt="Screenshot (438)" src="https://github.com/user-attachments/assets/fa6ed8be-c989-48b1-ad5e-203b960614b3" />


### Step 3: Verify Version

```bash
jq --version
```
<img width="1891" height="120" alt="Screenshot (549)" src="https://github.com/user-attachments/assets/6476bd75-c673-431b-8a1c-298639fae9e5" />

```
```
### Step 4: Verify Path

```bash
which jq
```
<img width="1920" height="142" alt="Screenshot (439)" src="https://github.com/user-attachments/assets/bab74177-c6fd-4644-9fc4-6c9dd4a808c2" />

```
```
### Step 5: Verify Package

```bash
dpkg -s jq | grep '^Status:'
```
<img width="1898" height="158" alt="Screenshot (548)" src="https://github.com/user-attachments/assets/c905cf4f-39cf-4ff9-aca6-6c7219e10b8f" />

---

# 8. JQ Configuration and Basic Usage

JQ does not require a separate configuration file for basic usage.

### Create Sample JSON

```bash
cat > sample.json <<'EOF'
{
  "name": "Employee",
  "department": "DevOps",
  "experience": 2
}
EOF
```
<img width="1920" height="184" alt="Screenshot (442)" src="https://github.com/user-attachments/assets/9d771276-1ddc-4056-8cb7-9c8058c9c446" />

### Format JSON

```bash
jq '.' sample.json
```
<img width="1920" height="171" alt="Screenshot (443)" src="https://github.com/user-attachments/assets/18366629-9295-4303-9bb8-c160c5aa41b8" />


### Extract a Field

```bash
jq '.name' sample.json
```
<img width="1920" height="120" alt="Screenshot (445)" src="https://github.com/user-attachments/assets/c427b3fd-7c7d-48a2-8267-55ece0636021" />


### Extract Raw Value

```bash
jq -r '.name' sample.json
```
<img width="1920" height="120" alt="Screenshot (551)" src="https://github.com/user-attachments/assets/abf06c2e-885f-48d1-bcee-76f8c1bce7ec" />

### Process JSON from Standard Input

```bash
echo '{"name":"Employee","role":"DevOps"}' | jq '.'
```
<img width="1920" height="202" alt="Screenshot (552)" src="https://github.com/user-attachments/assets/bdb7ae3b-283a-447f-9237-411a371fd7a2" />

### Use JQ in Shell Automation

```bash
JSON='{"status":"success","code":200}'
echo "$JSON" | jq -r '.status'
```
<img width="1920" height="129" alt="Screenshot (553)" src="https://github.com/user-attachments/assets/0f0d8bfe-7ff7-4979-b21c-08f3437c9111" />

---

# 9. Validation

### Validate Installation

```bash
jq --version
```
<img width="1891" height="120" alt="Screenshot (549)" src="https://github.com/user-attachments/assets/d3f68161-b0ff-407d-8b03-a1f847ab070a" />


### Validate Path

```bash
which jq
```
<img width="1920" height="120" alt="Screenshot (554)" src="https://github.com/user-attachments/assets/37807c28-7a0f-4f69-9b67-4d56728c7b76" />

### Validate JSON Processing

```bash
echo '{"name":"Vineet","role":"DevOps"}' > test.json
jq '.' test.json
```
<img width="1920" height="165" alt="Screenshot (555)" src="https://github.com/user-attachments/assets/9c95e9c0-d5db-4548-abb4-ea556eaa4579" />

### Validate Field Extraction

```bash
jq -r '.role' test.json
```
<img width="1920" height="120" alt="Screenshot (557)" src="https://github.com/user-attachments/assets/043a482b-8636-4539-94ff-844ad62a163c" />
```
---

# 10. Troubleshooting

| **Issue**                     | **Solution**                   |
| ----------------------------- | ------------------------------ |
| `jq: command not found`       | Run `sudo apt install -y jq`   |
| `Unable to locate package jq` | Run `sudo apt update`          |
| `apt update` fails            | Check network and repositories |
| `jq --version` fails          | Reinstall JQ                   |


---
# 11. Advantages and Disadvantages

| Advantages | Disadvantages |
|---|---|
| Extremely Fast: Performs operations almost instantaneously, making it suitable for automated deployment pipelines. | Syntax Learning Curve: Simple queries are easy, but advanced filters and arrays can be complex to learn. |
| Universal Standard: Available on many modern Linux distributions and commonly used in standard toolchains. | Strict JSON Formatting: Fails if the input JSON is malformed, missing quotes, or contains trailing commas. |
| Command Line Friendly: Integrates easily with standard UNIX pipes (`\|`). | No Direct File Editing: JQ cannot edit a JSON file in-place by default and requires creating a temporary file. |

---
# 12. Best Practices

* Always Verify Installation: Always verify that JQ is installed correctly before using it in scripts or automation. Use `jq --version` to confirm the installation and check the installed version.

* Use JQ Instead of Manually Parsing JSON: Use JQ to extract and process JSON data instead of manually parsing JSON in shell scripts. This makes JSON processing more reliable and easier to maintain.

* Validate JSON Input Before Processing: Always validate the JSON input before processing it with JQ. This helps prevent errors caused by malformed or invalid JSON data.

* Use `-r` for Raw String Output: Use the `-r` option when extracting string values that need to be used directly in shell scripts without JSON quotation marks.

* Use `-c` for Compact JSON: Use the `-c` option when compact JSON output is required, especially when passing JSON between commands or using it in automation workflows..

---

# 13. Conclusion

JQ is a lightweight and reliable command-line tool that simplifies parsing, filtering, and transforming JSON data directly from APIs and files. This SOP standardizes its installation, validation, and usage on Ubuntu-based systems to enhance command-line automation. Ultimately, integrating JQ into DevOps workflows eliminates manual processing, making JSON data manipulation fast, consistent, and reliable.

---

# 14. Contact Information

| **Name** | **Email**      |
| -------- | -------------- |
| Vineet   |  vineet.shrivastava.snaatak@mygurukulam.co |

---

# 15. References

| **Description**                               | **Reference (Link)**                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| JQ installation, usage, filters, and commands | [JQ Official Documentation](https://jqlang.org/)             |
| JQ options, functions, and syntax             | [JQ Manual](https://jqlang.org/manual/)                      |
| Ubuntu package and system administration      | [Ubuntu Documentation](https://documentation.ubuntu.com/)    |
| Linux command-line reference                  | [Linux Documentation](https://www.kernel.org/doc/man-pages/) |
