# Requirements.txt Documentation

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Priyanshu | 26-08-2026 | 1.1 | Priyanshu | 27-08-2026 | Aryan Mishra |  |  |
| Priyanshu | 26-08-2026 | 1.2 | Priyanshu | 11-08-2026 | Aryan Mishra | Aditya | |
| Priyanshu | 26-08-2026 | 1.3 | Priyanshu | 14-09-2026 | Aryan Mishra | Aditya | |


---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is requirements.txt](#2-what-is-requirementstxt)
3. [Why requirements.txt is Required](#3-why-requirementstxt-is-required)
4. [requirements.txt Workflow](#4-requirementstxt-workflow)
5. [Installation from requirementstxt](#5-installation-from-requirementstxt)
6. [Generating Python Dependencies](#6-generating-python-dependencies)
7. [Different Tools for Dependency Management](#7-different-tools-for-dependency-management)
8. [Advantages and Disadvantages](#8-advantages-and-disadvantages)
9. [Best Practices](#9-best-practices)
10. [Troubleshooting](#10-troubleshooting)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

This document serves as a comprehensive guide for managing Python project dependencies using requirements.txt.
It explains what requirements.txt is, why explicit dependency management is essential for Python CI/CD pipelines, and provides a step-by-step guide for defining, locking, and validating package versions.

---

# 2. What is requirements.txt

`requirements.txt` is a plain-text file that lists the Python packages (and typically their pinned versions) a project depends on. It is one of the most common building blocks of a Python CI/CD pipeline: it gives every stage of the pipeline — build, lint, test, and deploy — a single, deterministic source of truth for which dependencies to install, so the same environment can be reproduced on a developer's laptop, a CI runner, and production.

---

# 3. Why requirements.txt is Required

1. **Reproducibility**: Guarantees the same package versions are installed in development, CI, and production, avoiding "it works on my machine" failures. 
2. **Deterministic CI builds**: A CI/CD pipeline needs a single, unambiguous install step; without a requirements file, builds could silently pick up newer (and possibly breaking) package versions over time.
3. **Fail-fast pipelines**: The dependency install step runs before lint/test/build stages, so a broken or incompatible dependency set is caught immediately rather than mid-pipeline.
4. **Security scanning**: Tools such as `pip-audit` scan a `requirements.txt` file to flag known vulnerabilities (CVEs) in pinned dependencies as part of the CI check.
5. **Caching and speed**: CI systems can cache the dependency install step keyed on a hash of `requirements.txt`, significantly speeding up subsequent pipeline runs.

---

# 4. requirements.txt Workflow

A typical CI/CD workflow around `requirements.txt` looks like this:

1. **Environment Isolation** : Establish an isolated virtual environment or isolated container to prevent system-level package conflicts.
2. **Deterministic Installation** : Execute an exact dependency installation step where any network issue, package conflict, or missing release immediately halts the deployment pipeline.
3. **Validation & Security** : Perform multi-layered security checks by validating dependency graph compatibility, scanning pinned packages for vulnerabilities, and enforcing cryptographic hash verification for supply-chain integrity.
4. **Caching** : Cache downloaded package artifacts using a hash key derived directly from the requirements file to accelerate future execution runs.

---

# 5. Installation from requirementstxt


### 5.1 Setup Python and venv

```
sudo apt install python3 -y
```

```
sudo apt install python3.14-venv
```

### 5.2 Create a Virtual Environment

```
python3 -m venv venv
```

```
source venv/bin/activate
```

<img width="1343" height="97" alt="Screenshot (87)" src="https://github.com/user-attachments/assets/327d42cd-aedc-4a2f-936b-055e8e177906" />


### 5.3 Freeze Installed Dependencies

```
pip freeze > requirements.txt
```

<img width="1346" height="230" alt="Screenshot (88)" src="https://github.com/user-attachments/assets/f4ccf878-b83c-4880-8a84-1bfef2953c9e" />


### 5.4 Install Dependencies

```
pip install -r requirements.txt
```
<img width="1344" height="191" alt="Screenshot (89)" src="https://github.com/user-attachments/assets/46c4b2a3-9fba-42ab-80fa-a35c1804f496" />


# 6. Generating Python Dependencies

### 6.1 Define Dependencies

```
nano requirements.in
```

In requirements.in
```
requests >= 2.25.0
pandas
flask
```

### 6.2 Compile Exact Dependencies

```
pip-compile requirements.in
```

<img width="1342" height="325" alt="Screenshot (90)" src="https://github.com/user-attachments/assets/0b234574-83ae-4fbb-945d-8adfc6b7e4ca" />


### 6.3 Synchronize 

```
pip-sync
```

<img width="1344" height="354" alt="Screenshot (91)(1)" src="https://github.com/user-attachments/assets/5c53c65a-fe55-4549-869b-2a84345d86bc" />

### 6.4 Verify Installed Packages

```
pip list
```
<img width="1344" height="315" alt="Screenshot (91)(2)" src="https://github.com/user-attachments/assets/24e254d7-be62-4c60-b00c-6b7ee9d32177" />

---

# 7. Different Tools for Dependency Management

| **Tool** | **Description** |
| -------- | --------------- |
| `pip` + `requirements.txt` | Python's built-in installer paired with a plain-text dependency list; the most widely used and CI-friendly approach. |
| `pip-tools` | Compiles a fully pinned, hash-locked `requirements.txt` from a short, human-edited `requirements.in` file (`pip-compile`), and keeps environments in sync (`pip-sync`). |
| `Poetry` | Full dependency and packaging manager that uses `pyproject.toml` plus a `poetry.lock` file for reproducible installs, with built-in virtual environment management. |
| `Pipenv` | Combines `pip` and `virtualenv` workflows into a single tool, using a `Pipfile`/`Pipfile.lock` pair instead of `requirements.txt`. |

---

# 8. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| -------------- | ------------------ |
| Universally supported — every Python environment and CI system understands `pip install -r requirements.txt` | Plain `requirements.txt` has no built-in dependency resolver state — conflicting pins must be resolved manually unless paired with `pip-tools` |
| Simple, human-readable, and easy to diff/review in version control | Doesn't distinguish top-level (direct) dependencies from transitive ones unless deliberately structured that way |
| Works identically across OSes, containers, and CI providers with zero extra tooling | No native lock file with hashes unless `--require-hashes` and hash-pinned entries are explicitly used |
| Easy to cache in CI, keyed on a simple file hash | Keeping multiple environment-specific files (`-dev`, `-test`) in sync requires discipline or extra tooling |

---

# 9. Best Practices

1. Use strict version pins for deployable applications to ensure CI and production installations remain fully reproducible, while using broader version ranges only for reusable software libraries.
2. Keep a high-level, unpinned dependency specification and use Pip-Tools to compile it into a fully pinned requirements file, making dependency updates controlled and easy to audit.
3. Regularly scan dependency requirement files with security tools to detect known vulnerabilities and fail builds when critical security issues are found.
4. Always install Python packages inside dedicated virtual environments or containers to prevent dependency conflicts with system-level packages.
5. Review all changes to dependency files through the same rigorous pull-request process used for code changes to prevent breaking changes and security risks.

---

# 10. Troubleshooting

| **Symptom** | **Likely Cause** | **Resolution** |
| ----------- | ------------------ | -------------- |
| Packages fail to install due to permission errors | Running `pip install` without an active virtual environment attempts to write to system directories | Execute package installation inside an isolated virtual environment or container to avoid modifying system-level directories. |
| Dependency conflict during `pip install` | Incompatible package versions or conflicting pins exist across specified requirements | Use a dependency compilation tool like `pip-tools` to resolve the full dependency graph and generate a conflict-free lockfile. |
| Security audit tool flags known vulnerabilities | Pinned package versions contain documented CVEs or outdated releases | Update the targeted package version in your specification file, re-compile the requirements, and verify the patch with `pip-audit`. |
| Pipeline builds fail intermittently due to unpinned dependencies | Dependencies were specified using loose ranges or no version pins, picking up breaking upstream releases | Enforce strict `==` version pins in `requirements.txt` for application builds to ensure full reproducibility across environments. |

---

# 11. Conclusion

A version-pinned `requirements.txt` provides an efficient baseline without needing extra tooling. It is universally supported across Python environments and CI providers, keeping installation steps fast and easy to cache. Projects requiring higher reproducibility can layer `pip-tools` to lock transitive dependencies and verify cryptographic hashes. This setup maintains a concise `requirements.in` file while letting `pip-compile` generate the deterministic `requirements.txt` for production builds.

---

# 12. Contact Information

| **Name** | **Team** | **Email** |
| -------- | --------- | -------|
| Priyanshu | Kubeclan | [priyanshu.banwala.snaatak@mygurukulam.co](mailto:priyanshu.banwala.snaatak@mygurukulam.co) |
---

# 13. References

| **Description** | **Topic** |
| --------- | --------------- |
| Official pip documentation on requirements file syntax and options. | [pip Requirements File Format](https://pip.pypa.io/en/stable/reference/requirements-file-format/) | 
| Specification defining the version/marker syntax used in requirements files. | [PEP 508 – Dependency specification for Python](https://peps.python.org/pep-0508/) |
| Tooling for compiling and syncing pinned requirements files from a high-level spec. | [pip-tools (GitHub)](https://github.com/jazzband/pip-tools) |
