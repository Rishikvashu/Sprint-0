# Apache Maven Documentation

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer**            |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | -------------------------- |
| Vineet     | 28-08-2026     | 1.1         | Vineet              | 06-09-2026         | Aryan Mishra    |    Aditya Raj Singh      |    
| Vineet     | 28-08-2026     | 1.2         | Vineet              | 15-09-2026         | Aryan Mishra    |      Aditya Raj Singh           |                    |
| Vineet     | 28-08-2026     | 1.3         | Vineet              | 16-09-2026         | Aryan Mishra    | Aditya Raj Singh|                            |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Apache Maven](#2-what-is-apache-maven)
3. [Why Apache Maven](#3-why-apache-maven)
4. [Maven Reference Introduction](#4-maven-reference-introduction)
5. [Commonly Used Commands](#5-commonly-used-commands)
6. [Debugging Commands](#6-debugging-commands)
7. [Common Issues](#7-common-issues)
8. [Advantages and Disadvantages](#8-advantages-and-disadvantages)
9. [Best Practices](#9-best-practices)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)
---

# 1. Introduction

This document serves as a comprehensive Standard Operating Procedure (SOP) and practical guide for **Apache Maven**. 

It explains what Maven is, why it is essential for Java development, and provides a clear breakdown of its features, build workflow, and commonly used commands. 

---
# 2. What is Apache Maven

Apache Maven is a software project management and comprehension tool. Based on the concept of a Project Object Model (POM), Maven can manage a project's build processes, reporting, and documentation from a central, structured piece of information (`pom.xml`). 

Instead of manually writing complex build scripts, you simply configure the project details in the POM, and Maven dynamically handles the rest based on its built-in lifecycle.

---
# 3. Why Apache Maven

Maven is required to:

* **Automate the Build Process:** Eliminates the need for manual compilation and packaging.
* **Manage Dependencies:** Automatically downloads required libraries (JAR files) from central repositories so developers don't have to manually share or store them.
* **Standardize Project Structure:** Enforces a universal directory structure across all Java projects, making onboarding easier for new developers.
* **Streamline Deployment:** Easily integrates with automation tools (like Ansible) and CI/CD pipelines to build and deploy complex applications.
---
# 4. Maven Reference Introduction

For detailed Maven documentation, please refer this link [Maven Reference Documentation](https://github.com/SnaatakKubeClan/Sprint-0/blob/SCRUM-23-VASHISHTHA-PRAKASH/Documentation/Common_Stack/Application/Java/Maven/DOC/README.md).

---
# 5. Commonly Used Commands

| **Purpose**              | **Command**         |
| ------------------------ | ------------------- |
| Check Maven version      | `mvn --version`     |
| Check Maven path         | `which mvn`         |
| Validate project         | `mvn validate`      |
| Compile project          | `mvn compile`       |
| Run tests                | `mvn test`          |
| Package application      | `mvn package`       |
| Install artifact locally | `mvn install`       |
| Clean build files        | `mvn clean`         |
| Clean and build          | `mvn clean package` |

---
## 5.1 Check Maven Version

```bash
mvn --version
```
<img width="1472" height="167" alt="Screenshot (523)" src="https://github.com/user-attachments/assets/cf3bb103-32d8-47e5-8523-da9e061db7c8" />
This command displays the installed Maven version along with Java and Maven environment details.

---
## 5.2 Check Maven Path

```bash
which mvn
```
<img width="1178" height="120" alt="Screenshot (524)" src="https://github.com/user-attachments/assets/54ff86f0-7862-40f4-a61f-dc8e94fb5f5e" />
This command displays the location of the Maven executable installed on the system.

---

## 5.3 Validate Project

```bash
mvn validate
```
<img width="1627" height="246" alt="Screenshot (5261)" src="https://github.com/user-attachments/assets/26b5bf94-48ea-44a5-8d58-5858b3d979fb" />
This command checks whether the Maven project is correctly configured and ready for the build process.

---

## 5.4 Compile Project

```bash
mvn compile
```
<img width="1509" height="363" alt="Screenshot (525)" src="https://github.com/user-attachments/assets/0a663e9b-3fdd-407c-a05e-d3b36c27550c" />
This command compiles the project's source code and checks for compilation errors.

---

## 5.5 Run Tests

```bash
mvn test
```
<img width="1920" height="687" alt="Screenshot (526)" src="https://github.com/user-attachments/assets/5ff1dee3-77cc-4b08-946c-04439a3c47c5" />
This command executes the project's test cases to verify that the application works as expected.

---

## 5.6 Package Application

```bash
mvn package
```
<img width="1905" height="745" alt="Screenshot (527)" src="https://github.com/user-attachments/assets/0ae3ef32-f79d-45ac-96e2-1aa3826803f8" />
This command compiles the project, runs the tests, and packages the application into a distributable artifact.

---

## 5.7 Install Artifact Locally

```bash
mvn install
```
<img width="1892" height="197" alt="Screenshot (11119)" src="https://github.com/user-attachments/assets/cfe204ee-6c89-4a56-b2d2-258c339335c4" />
<img width="1920" height="162" alt="Screenshot (530)" src="https://github.com/user-attachments/assets/4b23e768-4ffa-4472-aa06-c9c76103c6c5" />
This command installs the packaged artifact into the local Maven repository for use by other projects.

---

## 5.8 Clean Build Files

```bash
mvn clean
```
<img width="1920" height="367" alt="Screenshot (531)" src="https://github.com/user-attachments/assets/df1b3d34-9a19-4fb8-836d-91d2eb585899" />
This command removes previously generated build files and artifacts from the project.

---

## 5.9 Clean and Build

```bash
mvn clean package
```
<img width="1909" height="197" alt="Screenshot (532)" src="https://github.com/user-attachments/assets/cb63dad0-60ee-4d9c-81df-46c11208bc28" />
<img width="1889" height="136" alt="Screenshot (533)" src="https://github.com/user-attachments/assets/f4383891-552f-4619-a169-a1101e16a7b1" />
This command removes previous build files and then builds and packages the project from a clean state

---

# 6. Debugging Commands
| Purpose | Command |
|---|---|
| View detailed Maven logs | `mvn package -X` |
| View dependency tree | `mvn dependency:tree` |
| Force dependency update | `mvn clean package -U` |
| Skip tests during build | `mvn package -DskipTests` |
| Clean previous build files | `mvn clean` |
| Check Maven configuration | `mvn --version` |

### 6.1 Detailed Maven Logs

```bash
mvn package -X
```
<img width="1920" height="198" alt="Screenshot (534)" src="https://github.com/user-attachments/assets/1f9127ff-65d9-46b3-b8e1-d5e94ad6233c" />
<img width="1920" height="198" alt="Screenshot (535)" src="https://github.com/user-attachments/assets/2bd08e8f-a125-4a97-8872-3b11304d0d58" />

Runs Maven with detailed debug output to help identify build issues.

### 6.2 Dependency Tree

```bash
mvn dependency:tree
```
<img width="1920" height="324" alt="Screenshot (536)" src="https://github.com/user-attachments/assets/65018370-6dc6-47d5-b8bc-2bf84feccd0f" />

Displays project dependencies and helps identify dependency conflicts.

### 6.3 Force Dependency Update

```bash
mvn clean package -U
```
<img width="1902" height="199" alt="Screenshot (538)" src="https://github.com/user-attachments/assets/fe2d0561-c901-4bc6-80ec-bb8edc7f0a1b" />
<img width="1904" height="204" alt="Screenshot (539)" src="https://github.com/user-attachments/assets/08ac7de4-add3-43e0-bad1-e3a89a4764d0" />

Forces Maven to check for updated dependencies.

### 6.4 Skip Tests

```bash
mvn package -DskipTests
```
<img width="1891" height="197" alt="Screenshot (541)" src="https://github.com/user-attachments/assets/fe6e9546-fd11-4fd7-84b9-e63d9ece8849" />
<img width="1920" height="180" alt="Screenshot (542)" src="https://github.com/user-attachments/assets/6660f526-ceed-464c-b93f-633634deec73" />

Builds the application without executing tests.

### 6.5 Clean Previous Build

```bash
mvn clean
```
<img width="1920" height="347" alt="Screenshot (544)" src="https://github.com/user-attachments/assets/7461756d-923c-472b-85ac-8b4f05ab0e10" />

Removes previously generated build artifacts.

### 6.6 Check Maven Configuration

```bash
mvn --version
```
<img width="1732" height="168" alt="Screenshot (545)" src="https://github.com/user-attachments/assets/c6a05094-0829-44ad-a80e-734c87b47272" />

Displays Maven version, Java version, Java home, and Maven home.

---

# 7. Common Issues

| **Issue**                  | **Solution / Debugging Command**                |
| -------------------------- | ----------------------------------------------- |
| `mvn: command not found`   | Install Maven using `sudo apt install -y maven` |
| `java: command not found`  | Install a supported JDK                         |
| `javac: command not found` | Install JDK and verify with `javac --version`   |
| Dependency conflict        | Run `mvn dependency:tree`                       |
| Build failure              | Run `mvn package -X`                            |
| Outdated dependency        | Run `mvn clean package -U`                      |
| Old build artifacts        | Run `mvn clean`                                 |

---
# 8. Advantages and Disadvantages

| Advantages | Disadvantages |
|---|---|
| Maven provides a consistent project structure and build process, making projects easier to manage. | Understanding POM files and plugin configurations can take some time for beginners. |
| Dependencies are managed externally, so they do not need to be stored in the Git repository. | Internet access is usually required to download dependencies that are not available locally. |
| Maven can detect missing or conflicting dependencies, helping developers manage project libraries easily. | Large projects with many dependencies and plugins may require more time during the build process. |

---
---

# 9. Best Practices

* Always specify plugin versions to prevent unexpected build failures.
* Use `mvn clean` before building to remove outdated artifacts.
* Manage dependencies centrally using `<dependencyManagement>`.
* Optimize automated deployments using batch mode (`-B`) and `-DskipTests` when appropriate.
* Avoid system scope dependencies and use reliable repositories.
* Run tests frequently in the local environment before deployment.
---

# 10. Conclusion

Apache Maven simplifies the **build and dependency management process** for Java applications. It provides commonly used commands for building, testing, packaging, dependency management, and debugging projects.

Using Maven with a properly configured Java environment helps maintain a **consistent, reliable, and manageable Java build process**.

---

# 11. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Vineet   | vineet.shrivastava.snaatak@mygurukulam.co |

---

# 12. References

| Description | Reference |
|---|---|
| Official Apache Maven documentation and project information. | [Apache Maven](https://maven.apache.org/) |
| Guide for getting started with Apache Maven projects. | [Maven Getting Started Guide](https://maven.apache.org/guides/getting-started/) |
| Detailed reference for Maven Project Object Model (POM). | [Maven POM Reference](https://maven.apache.org/pom.html) |
