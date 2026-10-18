<p align="center">
  <img width="100%" height="200" style="object-fit: cover; border-radius: 6px;" alt="GNU Make Banner" src="https://images.openai.com/static-rsc-4/6vc9WaQHnbGsDDonQPImyWEKzflyXbmfqufYvt2rK8Iun1BTnj_0c617hqdC9wKhQR7QfMqm5VncLz0kh4GDTwny8ScWdUB34JQQPs2GTrKATlf54Yedv4KRQ4PC-EyOMOsbUEcExFV4S5jUbnMs-f1so3q3qGFEjQ43VQ_bLS7MqLjed8zLMORmruhVLuTN?purpose=fullsize" />
</p>

# SOP: Build Automation | Ubuntu Linux | GNU Make and Makefile Setup

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Anurag Maurya | 25-08-2026 | v1 | Anurag Maurya | 25-08-2026 | Divya M | Aayush Verma | Mahesh Kumar/Varun |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is GNU Make](#2-what-is-gnu-make)
3. [Why GNU Make is Required](#3-why-gnu-make-is-required)
4. [Key Features of GNU Make](#4-key-features-of-gnu-make)
5. [Prerequisites and System Requirements](#5-prerequisites-and-system-requirements)
6. [GNU Make Installation and Verification](#6-gnu-make-installation-and-verification)
7. [Quick Commands](#7-quick-commands)
8. [Troubleshooting](#8-troubleshooting)
9. [Use Cases](#9-use-cases)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

Step-by-step Standard Operating Procedure (SOP) for installing GNU Make and configuring custom `Makefile` targets on Ubuntu Linux. Written in simple, friendly English for beginners to master build automation.

---

# 2. What is GNU Make

GNU Make is a build automation tool that automatically controls the generation of executables and non-source files of a program from the program's source files. It reads configuration rules from a `Makefile` to execute compilation, testing, and cleanup commands efficiently.

---

# 3. Why GNU Make is Required

Managing multi-step compilation, testing, and cleanup manually becomes error-prone as projects grow:
- **Automation of Repetitive Tasks**: One simple command (`make`) replaces long, complex compilation flags.
- **Smart Incremental Builds**: Make automatically checks file modification timestamps and only rebuilds modified components, saving build time.
- **Standardized Developer Experience**: Team members execute identical targets (`make build`, `make test`, `make clean`) across environments.

---

# 4. Key Features of GNU Make

| **Feature** | **Description** |
| ----------- | --------------- |
| **Target Rules** | Define custom execution targets (`all`, `build`, `test`, `clean`). |
| **Phony Targets** | Explicitly declare non-file targets using `.PHONY` to avoid naming conflicts. |
| **Incremental Building** | Skip compilation of unchanged files by comparing timestamps. |
| **Dry-Run Mode** | Preview commands before execution using `make -n`. |
| **Variables & Macros** | Reusable variables (`CC = gcc`, `CFLAGS = -Wall`) for maintainable Makefiles. |

---

# 5. Prerequisites and System Requirements

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| Operating System | Ubuntu 20.04/22.04/24.04 LTS |
| User Access | Account with `sudo` privileges |
| Package Manager | `apt` package manager |
| Text Editor | Any standard editor (`nano`, `vim`, or `VS Code`) |
| Compiler | `gcc` / `g++` (included in `build-essential`) |

> [!NOTE]
> Tool versions and installation outputs may vary depending on active package repository mirrors.

---

# 6. GNU Make Installation and Verification

### Step 1: Install GNU Make (`build-essential`)

Update `apt` repository cache and install Make compiler utilities.

```bash
# Update package lists
sudo apt update -y

# Install build-essential package (includes make, gcc, g++)
sudo apt install -y build-essential make
```

Expected output:

```bash
Reading package lists... Done
make is already the newest version (4.3-4.1build1).
```

*What this command sequence does:* Refreshes package lists and installs `build-essential` containing `make`, `gcc`, and `g++` tools needed to compile code and process Makefiles.

<details>
<summary>Click to view Terminal Screenshot: GNU Make Installation</summary>
<br>

![Make Installation Terminal Screenshot](./assets/make_install.png)

</details>

---

### Step 2: Verify GNU Make Version

Confirm Make CLI binary is available on your path.

```bash
make --version
```

Expected output:

```bash
GNU Make 4.3
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2020 Free Software Foundation, Inc.
```

*What this command does:* Displays installed GNU Make binary version and build target architecture.

<details>
<summary>Click to view Terminal Screenshot: Verify Make Version</summary>
<br>

![GNU Make Version Terminal Screenshot](./assets/make_version.png)

</details>

---

### Step 3: Create Workspace Directory Structure

Establish a clean project workspace folder.

```bash
# Create directory structure
mkdir -p ~/make-demo/src

# Navigate into project directory
cd ~/make-demo
```

Expected output:

```bash
~/make-demo
```

*What this command sequence does:* Creates project directory `~/make-demo/src` and changes working directory context into `~/make-demo`.

<details>
<summary>Click to view Terminal Screenshot: Create Workspace</summary>
<br>

![Make Workspace Setup Terminal Screenshot](./assets/make_mkdir.png)

</details>

---

### Step 4: Create C Source File & Makefile (`Makefile`)

Create sample C program and configure Make targets.

```bash
# Create C sample file
cat << 'EOF' > src/main.c
#include <stdio.h>

int main() {
    printf("GNU Make Build Automation Successful!
");
    return 0;
}
EOF

# Create Makefile
cat << 'EOF' > Makefile
# Variables
CC = gcc
CFLAGS = -Wall -g
TARGET = app

# Default target
.PHONY: all build test clean

all: build

build:
	@echo "Building binary executable..."
	$(CC) $(CFLAGS) src/main.c -o $(TARGET)

test: build
	@echo "Executing application test..."
	./$(TARGET)

clean:
	@echo "Cleaning up build artifacts..."
	rm -f $(TARGET)
EOF
```

Expected output:

```bash
Makefile created successfully
```

*What this configuration does:* Defines targets `all`, `build`, `test`, and `clean`, using variables for compiler (`gcc`) and compilation flags (`-Wall -g`).

> [!IMPORTANT]
> Makefile recipe lines **MUST** be indented with a true `Tab` character. Indenting recipes with spaces will trigger `*** missing separator. Stop.` syntax errors.

<details>
<summary>Click to view Terminal Screenshot: Makefile Configuration</summary>
<br>

![Makefile Editor View Terminal Screenshot](./assets/make_makefile_editor.png)

</details>

---

### Step 5: Execute Default Build Target (`make`)

Execute default compilation target.

```bash
make
```

Expected output:

```bash
Building binary executable...
gcc -Wall -g src/main.c -o app
```

*What this command does:* Reads `Makefile` and executes recipe steps under `build` target to compile `src/main.c` into output binary `./app`.

<details>
<summary>Click to view Terminal Screenshot: Execute Default Build</summary>
<br>

![Make Default Target Terminal Screenshot](./assets/make_default_run.png)

</details>

---

### Step 6: Execute Test Target (`make test`)

Run application test target.

```bash
make test
```

Expected output:

```bash
Executing application test...
GNU Make Build Automation Successful!
```

*What this command does:* Triggers `test` target which runs `./app` executable and prints binary console output.

<details>
<summary>Click to view Terminal Screenshot: Execute Test Target</summary>
<br>

![Make Test Target Terminal Screenshot](./assets/make_test_run.png)

</details>

---

### Step 7: Preview Commands in Dry-Run Mode (`make -n`)

Preview execution commands without actually running them.

```bash
make -n clean
```

Expected output:

```bash
echo "Cleaning up build artifacts..."
rm -f app
```

*What this command does:* `-n` flag prints commands Make would execute for target `clean` without modifying files.

<details>
<summary>Click to view Terminal Screenshot: Preview Dry-Run (make -n)</summary>
<br>

![Make Dry Run Terminal Screenshot](./assets/make_dry_run.png)

</details>

---

### Step 8: Clean Build Artifacts (`make clean`)

Remove generated binary files.

```bash
make clean
```

Expected output:

```bash
Cleaning up build artifacts...
rm -f app
```

*What this command does:* Executes `clean` recipe to remove compiled `./app` binary and maintain a clean workspace.

<details>
<summary>Click to view Terminal Screenshot: Clean Build Artifacts</summary>
<br>

![Make Execution Log Terminal Screenshot](./assets/make_execution_log.png)

</details>

---

# 7. Quick Commands

| **Task** | **Command** | **Description** |
| -------- | ----------- | --------------- |
| Build default | `make` | Execute default `all` / `build` target |
| Run test | `make test` | Execute `test` target |
| Clean artifacts | `make clean` | Remove binary output files |
| Dry run preview | `make -n <target>` | Preview target commands without executing |
| Custom Makefile | `make -f MyMakefile` | Execute specific Makefile |

---

# 8. Troubleshooting

| **Symptom / Error** | **Possible Root Cause** | **Resolution Step** |
| ------------------- | ----------------------- | ------------------- |
| `*** missing separator. Stop.` | Recipe line indented with spaces instead of a Tab | Replace spaces with a true `Tab` character in Makefile lines. |
| `make: Nothing to be done for 'all'` | Target output file is up to date | Declare non-file targets as `.PHONY: targetname` in Makefile. |
| `make: *** No targets specified and no makefile found. Stop.` | Running `make` in folder without `Makefile` | Ensure current working directory contains a file named `Makefile`. |
| `gcc: command not found` | Compiler package not installed | Install compiler tools via `sudo apt install -y build-essential`. |

---

# 9. Use Cases

1. **Software Compilation**: Automate multi-file C/C++ compilation into single commands.
2. **CI/CD Pipeline Standardization**: Use `make build`, `make test`, `make docker-push` as standardized stage steps in GitHub Actions or Jenkins.
3. **Local Dev Automation**: Run database setup, linting, and testing scripts via simple single-word commands.

---

# 10. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Always Use `.PHONY` | Declare non-file targets (`.PHONY: build clean test`) to avoid conflict if a folder shares target name. |
| Use Variables | Define compiler variables (`CC = gcc`) at the top of Makefile for easy updates. |
| Keep Recipes Silent | Use `@` prefix (`@echo "Building..."`) to suppress printing raw shell echoes. |
| Commit Makefile | Keep `Makefile` in root of Git repository for team consistency. |

---

# 11. Conclusion

GNU Make provides a clean, fast, and reliable method to automate build workflows, simplify complex command invocation, and accelerate software development on Linux servers.

---

# 12. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Anurag Maurya | [anurag.maurya.snaatak@mygurukulam.co](mailto:anurag.maurya.snaatak@mygurukulam.co) |

---

# 13. References

| **Topic** | **Description** |
| --------- | --------------- |
| [GNU Make Official Manual](https://www.gnu.org/software/make/manual/) | Complete GNU Make documentation and syntax reference. |
| [Ubuntu build-essential Manual](https://packages.ubuntu.com/search?keywords=build-essential) | Reference for Ubuntu build compiler suite. |
