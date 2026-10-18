# MAVEN Documentation
<img width="200" height="204" alt="image" src="https://github.com/user-attachments/assets/90101e79-3835-4c59-bb64-50b09cc9f3e5" />

---

# Author Table

| **Author**    | **Created On** | **Version** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ------------- | -------------- | ----------- | ------------------ | --------------- | --------------- | --------------- |
| Vashishtha Prakash | 31-08-2026     | v1.4         | 10-09-2026         | Sunny/Shubham   | Shreya/Nikita  | Piyush Upadhyay   |


---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Maven](#2-what-is-maven)
3. [Why Maven is Required](#3-why-maven-is-required)
4. [Maven Build & Repository Workflow](#4-maven-build--repository-workflow)

   * [4.1 Workflow Diagram](#4-maven-build--repository-workflow)
   * [4.2 Local Repository](#42-local-repository)
   * [4.3 Remote Repository](#43-remote-repository)
   * [4.4 Local Repository vs Remote Repository](#44-local-repository-vs-remote-repository)
5. [Best Practices](#5-best-practices)
6. [Conclusion](#6-conclusion)
7. [Contact Information](#7-contact-information)
8. [References](#8-references)

---

# 1. Introduction

This documentation of Maven is based on Maven's Build and Dependency management feature and its local and remote repositories.

---

# 2. What is Maven

Apache Maven is a Java-based build automation and dependency management tool widely used to build, test, package, and deploy Java applications. Maven provides a standard project structure and uses the `pom.xml` file to define project metadata, dependencies, plugins, build configuration, repositories, and other project information.

---
## 2.1 .Key Features of Maven

| **Feature**                    | **Description**                                                                         |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| **Dependency Management**      | Downloads and manages project dependencies automatically.                               |
| **Build Automation**           | Compiles, tests and packages Java applications.                                         |
| **POM Configuration**          | Centralizes project and build configuration in `pom.xml`.                               |
| **Transitive Dependencies**    | Automatically resolves dependencies of dependencies.                                    |
| **Build Lifecycle**            | Provides standard phases such as `compile`, `test`, `package`, `install`, and `deploy`. |
| **Plugin Ecosystem**           | Uses plugins to perform compilation, testing, packaging, analysis and deployment.       |
| **Repository Management**      | Supports local and remote artifact repositories.                                        |
| **Reproducible Builds**        | Dependency versions and build configuration can be defined explicitly.                  |

---

# 3. Why Maven is Required

Maven is required when a Java project needs a consistent and automated mechanism for building, testing, dependency management and artifact management. 


### Without Maven :-

A developer manually downloads the required JAR files and configures the classpath. The Java application is then compiled and tested to ensure everything works correctly. After successful testing, the developer creates the required JAR or WAR package. Version management and dependency updates are handled manually.


### With Maven :-

The developer defines project dependencies and build configuration in the `pom.xml` file. Maven reads the configuration and automatically resolves the required dependencies.
It then compiles the source code, runs tests, and packages the application.Finally, Maven can install the package locally and deploy it to a configured repository or environment.


Maven's standard lifecycle provides phases such as `validate`, `compile`, `test`, `package`, `verify`, `install`, and `deploy`.

---

# 4. Maven Build & Repository Workflow

<details>

<summary>Click to Expand Maven Build & Local/Remote Repository Workflow Diagram</summary>

<img width="1061" height="1483" alt="1" src="https://github.com/user-attachments/assets/5db28c9a-62c5-4c60-9abc-a92935eebfc0" />

</details>

---

## 4.2 Local Repository

The **local repository** is a directory on the machine where Maven is executed.

By default:

```text
Linux/macOS:
~/.m2/repository

Windows:
C:\Users\<username>\.m2\repository
```

The default location is `${user.home}/.m2/repository`, although it can be changed through `settings.xml`.

The local repository primarily serves two purposes:

1. It caches artifacts downloaded from remote repositories.
2. It stores artifacts installed locally using Maven's `install` phase.

### Example

Suppose `pom.xml` contains:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.18.0</version>
</dependency>
```

When Maven needs this dependency:

<img width="697" height="358" alt="image" src="https://github.com/user-attachments/assets/dc5c17f5-4283-4b2b-b50f-00e4423b0e9a" />


This reduces repeated downloads and can significantly improve subsequent builds.

---

## 4.3 Remote Repository

A **remote repository** is a repository accessed from another location.

Examples include:

* Maven Central
* Nexus Repository
* JFrog Artifactory
* Company-hosted Maven repositories

Remote repositories can be used for both **downloading** and **uploading** artifacts.

### Dependency Download

<img width="229" height="368" alt="image" src="https://github.com/user-attachments/assets/a9f9ef3a-7234-433f-b59d-8072df3c6580" />


### Artifact Upload

After a successful build:

<img width="297" height="365" alt="image" src="https://github.com/user-attachments/assets/21f08c07-493a-4e43-8d24-839991367e51" />


The Maven `deploy` phase is intended for build/release environments and copies the final package to a remote repository for sharing with other developers and projects.

---

## 4.4 Local Repository vs Remote Repository

| **Parameter**           | **Local Repository**               | **Remote Repository**                     |
| ----------------------- | ---------------------------------- | ----------------------------------------- |
| **Location**            | Developer/CI machine               | Server/cloud/network                      |
| **Default Example**     | `~/.m2/repository`                 | Maven Central / Nexus / Artifactory       |
| **Purpose**             | Cache and local artifact storage   | Shared artifact storage                   |
| **Dependency Download** | Maven checks it first              | Used when artifact is unavailable locally |
| **Artifact Sharing**    | Not intended for team-wide sharing | Designed for sharing                      |
| **Typical Command**     | `mvn install`                      | `mvn deploy`                              |



---

# 5. Best Practices

| **Best Practice**                           | **Description**                                                                                                           |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Pin Dependency Versions**                 | Define explicit and controlled dependency versions instead of relying on unpredictable versions.                          |
| **Do Not Commit `.m2`**                     | The Maven local repository is a machine-level cache and should not be stored in Git.                                      |
| **Use Internal Repository Managers**        | Enterprises should consider Nexus or Artifactory for controlled artifact storage and dependency proxying.                 |
| **Separate SNAPSHOT and Release Artifacts** | Use `SNAPSHOT` versions for ongoing development and release versions for stable artifacts.                                |
| **Secure Repository Credentials**           | Store repository credentials through Maven `settings.xml` secret mechanisms rather than committing passwords into Git. |
| **Use Dependency Management**               | Centralize dependency versions where appropriate, especially in multi-module projects.                                    |
| **Avoid Unnecessary Remote Repositories**   | Keep repository configuration controlled to reduce dependency and security risks.                                         |

---

# 6. Conclusion

Maven provides a structured and consistent approach to managing Java projects and their build requirements. Understanding its project structure, repositories, dependencies, and build process helps in maintaining projects efficiently and reliably.

---
# 7. Contact Information

| **Name** | **Email**                 |
| -------- | ------------------------- |
| Vashishtha Prakash   | vashishtha.prakash.snaatak@mygurukulam.co |

---

# 8. References

| **Topic**                                                                                                       | **Description**                                                                   |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [Apache Maven Official Documentation](https://maven.apache.org/)                                                | Official documentation for Apache Maven.                                          |
| [Maven Introduction to Repositories](https://maven.apache.org/guides/introduction/introduction-to-repositories) | Official documentation explaining local and remote Maven repositories.            |
| [Maven Repository Layout](https://maven.apache.org/repositories/layout.html)                                    | Official documentation explaining Maven repository structure and artifact paths.  |
| [Maven Local Repositories](https://maven.apache.org/repositories/local.html)                                    | Official documentation for Maven local repositories.                              |
| [Maven Remote Repositories](https://maven.apache.org/repositories/remote.html)                                  | Official documentation for Maven remote repositories.                             |
| [Maven Build Lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)        | Official documentation for Maven lifecycle phases.                                |
| [Maven Dependency Mechanism](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism) | Official documentation for dependency management and transitive dependencies.     |
| [Maven Settings Reference](https://maven.apache.org/settings.html)                                              | Official documentation for `settings.xml`, repositories, mirrors and credentials. |
