# Python requirements.txt Documentation

---

## Author Table

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Palak Upadhyay | 01-09-2026 | 1.0 | Palak Upadhyay | 02-09-2026 | Aryan Mishra | Aditya raj singh | - |
| Palak Upadhyay | 01-09-2026 | 1.1 | Palak Upadhyay | 12-09-2026 | Aryan Mishra | Aditya raj singh | - |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is requirements.txt](#2-what-is-requirementstxt)
3. [Why requirements.txt is Required](#3-why-requirementstxt-is-required)
4. [Structure of requirements.txt](#4-structure-of-requirementstxt)
5. [Dependency Versioning](#5-dependency-versioning)
6. [How to Set Up a Virtual Environment](#6-how-to-set-up-a-virtual-environment)
7. [Installing Dependencies](#7-installing-dependencies)
8. [Use Cases of requirements.txt](#8-use-cases-of-requirementstxt)
9. [Python requirements.txt Workflow](#9-python-requirementstxt-workflow)
10. [Alternative Dependency Tools Comparison](#10-alternative-dependency-tools-comparison)
11. [Advantages and Disadvantages](#11-advantages-and-disadvantages)
12. [Best Practices](#12-best-practices)
13. [Conclusion](#13-conclusion)
14. [Contact Information](#14-contact-information)
15. [References](#15-references)


---

## 1. Introduction

This SOP provides a simple guide to managing Python dependencies using `requirements.txt`. It covers setup, usage, workflow, and best practices.

Following these steps helps keep Python environments consistent and makes application setup easier across development and production.

---

## 2. What is requirements.txt

`requirements.txt` is a file in a Python project that lists the packages and libraries needed to run the application.

It helps install all required packages easily using `pip install -r requirements.txt` and keeps the same dependencies across different environments.


---

## 3. Why requirements.txt is Required

requirements.txt helps keep the same Python packages and versions across development, testing, and production environments.

It makes builds more reliable, speeds up CI/CD setup, and helps avoid issues caused by different package versions.

---

## 4. Structure of requirements.txt

Without a proper `requirements.txt`, applications become difficult to reproduce and maintain.

| Structure Type | Example | Description |
| :--- | :--- | :--- |
| **Basic Package Listing** | `Flask` | Installs latest available version of the Flask package |
| **Exact Version Pinning** | `Flask==2.3.3` | Installs exact Version 2.3.3 of the Flask package |
| **Minimum Version** | `django>=4.2` | Installs Django version 4.2 or higher |
| **Maximum Version** | `numpy<2.0` | Restricts NumPy to versions lower than 2.0 |
| **Compatible Version** | `requests~=2.31` | Installs a version compatible with Requests 2.31.x |
| **Comments** | `# Web framework` | Used only for readability; ignored by pip |

---

## 5. Dependency Versioning

Dependency versioning defines **which version of a Python package should be installed** for the application.

It ensures that the application behaves **consistently across all environments**, including development, CI/CD pipelines, and production.

### Common Version Specifiers

| Operator | Meaning |
| :--- | :--- |
| `==` | Install exact version |
| `>=` | Minimum required version |
| `<=` | Maximum allowed version |
| `~=` | Compatible release |
| `>` | Greater than |
| `<` | Less than |

### Example

django==4.2  
requests>=2.25  
numpy~=1.2.0  


---

## 6. How to Set Up a Virtual Environment

It is standard DevOps practice to isolate project dependencies inside a Virtual Environment before generating `requirements.txt`.

### Quick Setup Commands:

1. **Create an isolated environment:**
   ```bash
   python3 -m venv myenv
   ```

2. **Activate the environment:**
   * **Linux / Ubuntu / macOS:**
     ```bash
     source myenv/bin/activate
     ```
   * **Windows:**
     ```cmd
     myenv\Scripts\activate
     ```

3. **Deactivate when finished:**
   ```bash
   deactivate
   ```

> [!NOTE]
> For advanced concepts and configurations, refer to the [Python Virtual Environment Documentation](https://github.com/SnaatakKubeClan/Sprint-0/blob/SCRUM-12-VINEET/Documentation/Common_Stack/Applications/Python/Virtual_Environment/DOC/README.md).

---

## 7. Installing Dependencies

| Operating System | Installation Commands |
| :--- | :--- |
| **Windows** | <details><summary>View Commands</summary><br><b>Install dependencies</b><br><code>pip install -r requirements.txt</code><br><br><b>Using Virtual Environment</b><br><code>python -m venv venv; .\venv\Scripts\activate; pip install -r requirements.txt</code></details> |
| **Linux** | <details><summary>View Commands</summary><br><b>Install dependencies</b><br><code>pip install -r requirements.txt</code><br><br><b>Using Virtual Environment</b><br><code>python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt</code></details> |
| **macOS** | <details><summary>View Commands</summary><br><b>Install dependencies</b><br><code>pip install -r requirements.txt</code><br><br><b>Using Virtual Environment</b><br><code>python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt</code></details> |

---

## 8. Use Cases of requirements.txt

| Use Case | Description |
| :--- | :--- |
| **Team Collaboration** | Ensures all developers use the exact same dependency versions, preventing environment conflicts. |
| **Docker Containerization** | Used in `Dockerfile` (`RUN pip install -r requirements.txt`) to build reproducible container images. |
| **CI/CD Pipelines** | Automatically installs required packages before running automated tests and deployment builds. |
| **Production Deployment** | Enables fast, reliable, and consistent environment setup on production Linux servers. |
| **Version Rollbacks** | Helps quickly restore known stable package versions if a new library update causes bugs. |

---

## 9. Python requirements.txt Workflow


![Requirements Workflow](requirements_workflow.png)

---

### Workflow Explanation

1. **Virtual Environment Isolation:** Create and activate a clean, isolated virtual environment (`python -m venv venv`) to keep project-specific dependencies segregated from the host system.
2. **Package Installation:** Install required application dependencies and third-party libraries using `pip install <package_name>`.
3. **Dependency Manifest Generation:** Freeze and export the exact active package versions into a manifest file using `pip freeze > requirements.txt`.
4. **Version Control Commit:** Track and version the generated `requirements.txt` file in Git (`git add`, `git commit`, `git push`) alongside application source code.
5. **Deployment & CI/CD Restoration:** Reproduce the identical runtime environment across CI/CD pipelines, staging servers, and Docker containers by executing `pip install -r requirements.txt`.
6. **Security Audit & Maintenance:** Scan pinned libraries for known CVE vulnerabilities using `pip-audit` and verify package hashes before releasing to production.

---

## 10. Advantages and Disadvantages

| Advantages | Disadvantages |
| :--- | :--- |
| Built-in natively with Python; requires zero third-party tools to start. | Mixes direct dependencies with secondary transient sub-dependencies in `pip freeze`. |
| Installs packages sequentially with very high speed and minimal overhead. | Does not generate an automated deterministic lockfile without external tools. |
| Human-readable plain text format that is easy to inspect, diff, and track in Git. | Requires explicit `--require-hashes` flag to enforce cryptographic integrity checking. |

---

## 11. Best Practices

* Always use virtual environments to isolate project dependencies from global system packages.
* Pin exact package versions (`==`) in production files to prevent breaking changes from upstream updates.
* Keep separate dependency files for production (`requirements.txt`) and testing/development (`requirements-dev.txt`).
* Run automated vulnerability checks using `pip-audit` in CI/CD pipelines before deployment.
* Use `--require-hashes` in mission-critical environments to ensure package integrity against supply chain risks.

---

## 12. Conclusion

Managing Python dependencies with `requirements.txt` provides a lightweight, universal, and reproducible environment across development and production pipelines.

Pinning exact versions and isolating runtime packages with virtual environments eliminates version drift and unexpected build failures.
Following these standard practices guarantees predictable CI/CD deployments, enhanced container security, and streamlined project onboarding.

---

## 13. Contact Information

| Name | Email Address |
| :--- | :--- |
| Palak Upadhyay | [palak.upadhyay.snaatak@opstree.com](mailto:palak.upadhyay.snaatak@opstree.com) |

---

## 14. References

| Description | Reference Link |
| :--- | :--- |
| Official standards and best practices for managing and distributing Python packages | [Python Packaging User Guide](https://packaging.python.org/en/latest/) |
| Comprehensive user guide and CLI reference for the pip package installer | [pip Documentation](https://pip.pypa.io/en/stable/user_guide/) |
| Formal specification for semantic versioning numbers and release rules | [Semantic Versioning 2.0.0](https://semver.org/) |
