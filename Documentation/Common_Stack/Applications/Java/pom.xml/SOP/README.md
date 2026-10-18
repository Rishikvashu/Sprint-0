# SOP: Java & Build Tools | Ubuntu Linux | Maven and pom.xml Setup

<p align="center">
  <img width="100%" height="200" style="object-fit: cover; border-radius: 6px;" alt="Maven Banner" src="https://vectorseek.com/wp-content/uploads/2024/02/Maven-new-Logo-Vector.svg-.png" />
</p>

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Anurag Maurya | 25-08-2026 | v1 | Anurag Maurya | 25-08-2026 | Divya M | Aayush Verma | Mahesh Kumar/Varun |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is Apache Maven](#2-what-is-apache-maven)
3. [Why Apache Maven is Required](#3-why-apache-maven-is-required)
4. [Key Features of Apache Maven](#4-key-features-of-apache-maven)
5. [Prerequisites and System Requirements](#5-prerequisites-and-system-requirements)
6. [Java Maven Setup and Verification](#6-java-maven-setup-and-verification)
7. [Quick Commands](#7-quick-commands)
8. [Troubleshooting](#8-troubleshooting)
9. [Use Cases](#9-use-cases)
10. [Best Practices](#10-best-practices)
11. [Conclusion](#11-conclusion)
12. [Contact Information](#12-contact-information)
13. [References](#13-references)

---

# 1. Introduction

Step-by-step Standard Operating Procedure (SOP) for installing Java OpenJDK 17, configuring Apache Maven, and creating standard `pom.xml` build files on Ubuntu Linux. Written in simple, clear English for beginners.

---

# 2. What is Apache Maven

Apache Maven is a build automation and software project management tool primarily used for Java projects. Maven uses a Project Object Model (POM) XML file (`pom.xml`) to manage project dependencies, build lifecycles, plugins, and compilation settings.

---

# 3. Why Apache Maven is Required

Managing Java libraries (`.jar` files) and compilation manually presents common challenges:
- **Dependency Hell**: Managing external JAR files manually causes version conflicts and missing library errors.
- **Automated Dependency Resolution**: Maven automatically downloads required libraries and sub-dependencies from Maven Central Repository.
- **Standardized Directory Structure**: Enforces standard folder layout (`src/main/java`, `src/test/java`) across all Java projects worldwide.

---

# 4. Key Features of Apache Maven

| **Feature** | **Description** |
| ----------- | --------------- |
| **Centralized `pom.xml`** | Define metadata (`groupId`, `artifactId`, `version`) and dependencies in one XML file. |
| **Build Lifecycles** | Pre-defined phases (`clean`, `compile`, `test`, `package`, `install`). |
| **Central Repository** | Automatic downloading and caching of open-source Java dependencies. |
| **Plugin Ecosystem** | Extensible plugin architecture for code coverage, linting, and dockerization. |
| **JAR / WAR Packaging** | Automated generation of runnable executable `.jar` or web `.war` artifacts. |

---

# 5. Prerequisites and System Requirements

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Version | Ubuntu 20.04/22.04/24.04 LTS |
| Java JDK | OpenJDK 17 LTS or newer (`openjdk-17-jdk`) |
| Build Tool | Apache Maven 3.6+ (`maven`) |
| User Privileges | Non-root user with `sudo` access |
| Network | Internet connection to reach Maven Central Repository |

> [!NOTE]
> JDK and Maven versions may vary depending on active APT mirror repositories.

---

# 6. Java Maven Setup and Verification

### Step 1: Install OpenJDK 17 (`openjdk-17-jdk`)

Install Java Development Kit runtime environment.

```bash
# Update APT index
sudo apt update -y

# Install OpenJDK 17 JDK
sudo apt install -y openjdk-17-jdk
```

Expected output:

```bash
openjdk-17-jdk is already the newest version (17.0.10+7-1ubuntu1).
```

*What this command sequence does:* Refreshes APT metadata and installs OpenJDK 17 compiler (`javac`) and Java runtime environment (`java`).

<details>
<summary>Click to view Terminal Screenshot: OpenJDK 17 Installation</summary>
<br>

![Java Version Terminal Screenshot](./assets/java_version.png)

</details>

---

### Step 2: Install Apache Maven (`maven`)

Install Apache Maven build automation CLI tool.

```bash
# Install Apache Maven
sudo apt install -y maven

# Verify Maven version
mvn -version
```

Expected output:

```bash
Apache Maven 3.8.7
Maven home: /usr/share/maven
Java version: 17.0.10, vendor: Ubuntu
```

*What this command sequence does:* Installs Maven CLI binaries (`mvn`) and validates installation against OpenJDK 17 environment.

<details>
<summary>Click to view Terminal Screenshot: Apache Maven Version Verification</summary>
<br>

![Apache Maven Version Terminal Screenshot](./assets/maven_version.png)

</details>

---

### Step 3: Create Standard Maven Folder Structure

Scaffold standard Java project layout.

```bash
# Create directory structure
mkdir -p ~/maven-demo/src/main/java/com/example
mkdir -p ~/maven-demo/src/test/java/com/example

# Switch directory
cd ~/maven-demo
```

Expected output:

```bash
~/maven-demo
```

*What this command sequence does:* Establishes standard Maven directory structure `src/main/java` for source code and `src/test/java` for unit test files.

<details>
<summary>Click to view Terminal Screenshot: Maven Directory Layout</summary>
<br>

![Maven Directory Layout Terminal Screenshot](./assets/maven_dir_layout.png)

</details>

---

### Step 4: Create Project Object Model Configuration (`pom.xml`)

Create `pom.xml` configuration file.

```bash
cat << 'EOF' > ~/maven-demo/pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>maven-demo-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.10.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
EOF
```

Expected output:

```bash
pom.xml created successfully
```

*What this configuration does:* Defines Maven coordinate (`groupId`, `artifactId`, `version`), configures Java 17 target compatibility flags, and includes JUnit 5 test dependency.

<details>
<summary>Click to view Terminal Screenshot: pom.xml Configuration Structure</summary>
<br>

![pom.xml Structure Terminal Screenshot](./assets/maven_pom_structure.png)

</details>

---

### Step 5: Write Sample Java Application (`App.java`)

Create Java entrypoint source file.

```bash
cat << 'EOF' > src/main/java/com/example/App.java
package com.example;

public class App {
    public static void main(String[] args) {
        System.out.println("Java Maven pom.xml Build Successful!");
    }
}
EOF
```

Expected output:

```bash
App.java created successfully
```

*What this command does:* Creates `App.java` under package `com.example` with a standard `main` method.

<details>
<summary>Click to view Terminal Screenshot: App Java Source File</summary>
<br>

![App Java File Terminal Screenshot](./assets/maven_app_java.png)

</details>

---

### Step 6: Compile Java Code (`mvn clean compile`)

Clean target folder and compile source code.

```bash
mvn clean compile
```

Expected output:

```bash
[INFO] --- maven-compiler-plugin:3.11.0:compile (default-compile) @ maven-demo-app ---
[INFO] Compiling 1 source file to /home/ubuntu/maven-demo/target/classes
[INFO] BUILD SUCCESS
```

*What this command does:* Cleans existing build outputs and compiles `.java` source files into bytecode `.class` files inside `target/classes`.

<details>
<summary>Click to view Terminal Screenshot: Compile Java Code (mvn clean compile)</summary>
<br>

![Maven Clean Compile Terminal Screenshot](./assets/maven_clean_compile.png)

</details>

---

### Step 7: Package Runnable JAR File (`mvn package`)

Package compiled bytecode into an executable `.jar` archive.

```bash
mvn package
```

Expected output:

```bash
[INFO] Building jar: /home/ubuntu/maven-demo/target/maven-demo-app-1.0.0.jar
[INFO] BUILD SUCCESS
```

*What this command does:* Bundles compiled Java classes into a distribution `.jar` archive inside `target/` directory.

<details>
<summary>Click to view Terminal Screenshot: Package Runnable JAR (mvn package)</summary>
<br>

![Maven Package Build Terminal Screenshot](./assets/maven_package_build.png)

</details>

---

### Step 8: Run Packaged Application (`java -cp`)

Execute packaged Java JAR application.

```bash
java -cp target/maven-demo-app-1.0.0.jar com.example.App
```

Expected output:

```bash
Java Maven pom.xml Build Successful!
```

*What this command does:* Invokes Java Virtual Machine (JVM) with classpath (`-cp`) set to generated JAR archive and executes `com.example.App`.

<details>
<summary>Click to view Terminal Screenshot: Run Java Application JAR</summary>
<br>

![Run Java Application JAR Terminal Screenshot](./assets/maven_run_jar.png)

</details>

---

# 7. Quick Commands

| **Task** | **Command** | **Description** |
| -------- | ----------- | --------------- |
| Compile source | `mvn compile` | Compile `.java` source files into bytecode |
| Clean target | `mvn clean` | Remove generated `target/` build folder |
| Run test suite | `mvn test` | Execute unit test classes |
| Package JAR | `mvn package` | Package compiled code into executable `.jar` |
| Install local | `mvn install` | Install `.jar` to local `~/.m2/repository` |

---

# 8. Troubleshooting

| **Symptom / Error** | **Possible Root Cause** | **Resolution Step** |
| ------------------- | ----------------------- | ------------------- |
| `JAVA_HOME is not set` | Environment variable `JAVA_HOME` is missing | Set `export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64` in `~/.bashrc`. |
| `[ERROR] Source option 5 is no longer supported` | Missing Java version target in `pom.xml` | Ensure `<maven.compiler.source>17</maven.compiler.source>` is set in properties. |
| `[ERROR] Cannot resolve dependency` | Network failure or invalid repository | Check internet connection and verify dependency XML syntax on Maven Central. |
| `[ERROR] Build failure: missing pom.xml` | Executing `mvn` outside project root | Ensure working directory contains `pom.xml` before running `mvn`. |

---

# 9. Use Cases

1. **Enterprise Java Development**: Manage multi-module microservice backend systems cleanly.
2. **CI/CD Integration**: Standardize build commands (`mvn clean package`) in Jenkins/GitLab CI pipelines.
3. **Automated Unit Testing**: Run automated test suites via `mvn test` prior to deploying releases.

---

# 10. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Use Explicit Properties | Always declare `<maven.compiler.source>` and `<maven.compiler.target>` explicitly. |
| Avoid Hardcoded Paths | Never hardcode local file paths inside `pom.xml`. |
| Commit `pom.xml` | Keep `pom.xml` in Git root, but add `target/` directory to `.gitignore`. |
| Leverage Local Cache | Utilize local `~/.m2/repository` cache to speed up offline builds. |

---

# 11. Conclusion

Apache Maven simplifies Java application management by automating dependency resolution, providing standard build lifecycles, and producing production-ready JAR/WAR release packages.

---

# 12. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Anurag Maurya | [anurag.maurya.snaatak@mygurukulam.co](mailto:anurag.maurya.snaatak@mygurukulam.co) |

---

# 13. References

| **Topic** | **Description** |
| --------- | --------------- |
| [Apache Maven Official Site](https://maven.apache.org/) | Official Maven documentation and plugin guide. |
| [Maven Central Repository](https://mvnrepository.com/) | Central index for Java dependencies and libraries. |
