#  Java Installation Guide

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/en/3/30/Java_programming_language_logo.svg" alt="Java Logo" width="100"/>
</p>

---
# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Sarthak Bhatnagar | 25-08-2026 |v1.1| Sarthak Bhatnagar | 07-09-2026 | Ishaan | Anuj Jain | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Java OpenJDK Installation](#4-java-openjdk-installation)
5. [Environment Variables Configuration](#5-environment-variables-configuration)
6. [Verify Java Versions](#6-Verify-java-versions)
7. [Validation](#7-validation)
8. [Use Cases](#8-use-cases)
9. [Troubleshooting](#9-troubleshooting)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

This document provides a **step-by-step** for installing and configuring Java. It covers **OpenJDK installation**, JAVA_HOME configuration, PATH setup, and verification to ensure Java is ready for development and application deployment.

**Java** is a high-level, **object-oriented programming language** widely used for building web applications, enterprise software, backend systems, and Android applications.

---

# 2. Purpose

The purpose of this Installation is to:
| **Requirement**           | **Description**                                                                       |
| ------------------------- | ------------------------------------------------------------------------------------- |
| **Install Java**          | Install **OpenJDK 17 / 21 LTS** on Linux servers.                                     |
| **Configure Environment** | Configure persistent **`JAVA_HOME`** and **`PATH`** environment variables.            |
| **Verify Installation**   | Verify the Java installation and switch between multiple Java versions when required. |

---

# 3. Prerequisites

| **Prerequisite** | **Details** |
| :--- | :--- |
| **Operating System** | Ubuntu 20.04 / 22.04 / 24.04 LTS |
| **User Privileges** | `sudo` or root access |
| **System Requirements** | Minimum 2 GB RAM and 1 GB free disk space |

---

# 4. Java OpenJDK Installation

### Step 1: Update System Packages
```bash
sudo apt update
```
<img width="1028" height="560" alt="Screenshot 2026-09-02 at 2 50 30 PM" src="https://github.com/user-attachments/assets/d4452626-4c69-433a-ad67-f359e68f27bc" />


### Step 2: Install OpenJDK 17
```bash
sudo apt install -y openjdk-17-jdk
```
<img width="1028" height="560" alt="Screenshot 2026-09-02 at 2 51 28 PM" src="https://github.com/user-attachments/assets/8f20bdd4-636a-45c8-b4b6-b0fbc4125ea1" />

---

# 5. Environment Variables Configuration

### Step 1: Set Persistent JAVA_HOME
```bash
sudo bash -c 'cat <<EOF > /etc/profile.d/java.sh
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=\$JAVA_HOME/bin:\$PATH
EOF'
```

### Step 2: Apply and Verify
```bash
sudo chmod +x /etc/profile.d/java.sh
source /etc/profile.d/java.sh
echo $JAVA_HOME
```
<img width="1205" height="81" alt="Screenshot 2026-09-02 at 3 22 03 PM" src="https://github.com/user-attachments/assets/da014cb1-dea3-4aef-94dc-9dddd714ccaa" />


---

# 6. verify Java Versions

### Check the installed Java compiler version.

```bash
java -version
```
<img width="1028" height="159" alt="Screenshot 2026-09-02 at 2 52 38 PM" src="https://github.com/user-attachments/assets/188ebd38-273a-4682-91ec-4fbc4e419d10" />

```bash
javac -version
```

<img width="1205" height="165" alt="Screenshot 2026-09-02 at 3 30 57 PM" src="https://github.com/user-attachments/assets/c1875f11-a918-4e55-a128-b59059a33198" />



---

# 7.Validation Checklist:

| **Check** | **Command** | **Expected Result** |
| :--- | :--- | :--- |
| Java Runtime | `java -version` | Returns OpenJDK 17.x |
| Java Compiler | `javac -version` | Returns javac 17.x |
| JAVA_HOME | `echo $JAVA_HOME` | Returns `/usr/lib/jvm/java-17-openjdk-amd64` |

---

# 8. Use Cases

| **Use Case** | **Example Command** |
| :--- | :--- |
| **Spring Boot Apps** | `java -jar app.jar` |
| **Build Tools (Maven/Gradle)** | `mvn clean package` or `./gradlew build` |
| **Big Data (Kafka / Spark)** | `bin/kafka-server-start.sh config/server.properties` |
| **Docker Containers** | `docker run -d eclipse-temurin:17-jre` |

---

# 9. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| :--- | :--- | :--- |
| `java: command not found` | OpenJDK is not installed or `PATH` is missing. | Run `sudo apt install -y openjdk-17-jdk`. |
| `javac: command not found` | Only JRE was installed instead of JDK. | Run `sudo apt install -y openjdk-17-jdk`. |


---

# 10. Best Practices


| Best Practice                  | Description                                                               |
| ------------------------------ | ------------------------------------------------------------------------- |
| **Use LTS Releases**           | Standardize on **Java 17** or **Java 21** LTS for production stability.   |
| **Use Vendor-Neutral OpenJDK** | Use open-source **OpenJDK** or **Eclipse Temurin**.                       |
| **Set Global JAVA_HOME**       | Configure `JAVA_HOME` in `/etc/profile.d/java.sh` for users and CI tools. |
| **Container Memory Limits**    | Use `-XX:MaxRAMPercentage=75.0` in Docker/Kubernetes.                     |


---

# 11. Conclusion

This documentation provides a **standardized and reliable** process for **Java installation** and configuration. It helps ensure that Java, JAVA_HOME, PATH, and the **Java** compiler are correctly configured and ready to support development, build tools, and CI/CD environments.

---

# 12. Contact Information

| **Name** | **Email** |
| :--- | :--- |
| Sarthak Bhatnagar | [sarthak.bhatnagar.snaatak@mygurukulam.co](mailto:sarthak.bhatnagar.snaatak@mygurukulam.co) |

---

# 13. References

| **Topic**             | **Link**                                                           |
| --------------------- | ------------------------------------------------------------------ |
| **OpenJDK Official**  | [openjdk.org](https://openjdk.org/)                                |
| **Ubuntu Java Guide** | [ubuntu.com/server/docs/java](https://ubuntu.com/server/docs/java) |
