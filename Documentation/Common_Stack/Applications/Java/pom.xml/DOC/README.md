# COMMON STACK | Applications | Java | pom.xml Documentation

<p align="center">
<img width="180" height="140" alt="OIP" src="https://github.com/user-attachments/assets/7fe95d89-f3d4-4ffe-b493-987e20e3ca34" />
</p>


---

# Author Table

| **Author** | **Created On** | **Version**  | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------ | --------------- | --------------- | --------------- |
| Anshul kotiya | 28-08-2026 | 1.1 | 07-09-2026   |    Shubham Rathi   |  shreya / Nikita  | Piyush Upadhyay |

---

# Table of Contents
1. [Introduction](#1-introduction)
2. [What is pom.xml?](#2-what-is-pomxml)
3. [Why do we need pom.xml?](#3-why-do-we-need-pomxml)
4. [Core Elements of pom.xml](#4-core-elements-of-pomxml)
   * [4.1 Project Coordinates (GAV)](#41-project-coordinates-gav)
   * [4.2 Packaging](#42-packaging)
   * [4.3 Properties](#43-properties)
   * [4.4 Dependencies](#44-dependencies)
   * [4.5 Build](#45-build)
   * [4.6 parent](#46-parent)
   * [4.7 modules](#47-modules)

5. [Use Cases](#5-use-cases)

6. [Dependency & Versioning Best Practices](#6-dependency--versioning-best-practices)
   * [6.1 Use Specific Versions](#61-use-specific-versions)
   * [6.2 Use Properties for Common Versions](#62-use-properties-for-common-versions)
   * [6.3 Use dependencyManagement](#63-use-dependencymanagement)
   * [6.4 Regularly Check Dependencies](#64-regularly-check-dependencies)

7. [Recommendation / Conclusion](#7-recommendation--conclusion)
8. [Contact Information](#8-contact-information)
9. [Reference](#9-reference)

---

# 1. Introduction
 
 This document provides a complete overview of pom.xml, the core configuration file used by Apache Maven to build and manage Java projects. It covers what pom.xml is and why it is required, how Maven processes it through the build lifecycle and best practices to follow when working with pom.xml.

---

# 2. What is pom.xml?

pom.xml (Project Object Model) is the core configuration file used by Apache Maven to build and manage a Java project. It is an XML file placed at the root of a Maven project that describes the project's identity, its dependencies, build configuration, plugins, profiles, and other metadata needed to compile, test, package, and deploy the application.


- A minimal pom.xml looks like this:
```
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.opstree.otms</groupId>
  <artifactId>ot-microservice</artifactId>
  <version>1.0.0</version>
  <packaging>jar</packaging>
</project>
```
---

# 3. Why do we need pom.xml?

Without pom.xml, Maven has no way of knowing what a project needs to build, test, or run. It centralizes everything related to the build process in a single file, which brings the following benefits:

| **Benefit**                       | **Description**                                                                                                                                                |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Dependency Management**         | Declares external libraries; Maven automatically downloads them along with their transitive dependencies from repositories.                                    |
| **Build Standardization**         | Defines a consistent lifecycle such as `compile`, `test`, `package`, `install`, and `deploy`, which runs consistently on developer machines and build servers. |
| **Plugin Configuration**          | Configures the tools that perform build-related tasks, such as the compiler, test runner, and packager, in one place.                                          |
| **Project Metadata**              | Stores project identity information such as `groupId`, `artifactId`, and `version`, which are used for versioning and resolving artifacts from repositories.   |
| **Consistency**                   | Helps produce consistent builds across environments by controlling dependencies, plugins, and configuration through the same `pom.xml`.                        |
| **Convention Over Configuration** | Maven assumes a standard folder structure, so `pom.xml` only needs to define configurations that differ from the defaults.                                     |



---

# 4. Core Elements of pom.xml

 A full-featured pom.xml is made up of several major blocks. Understanding each one helps you read and write pom.xml files confidently.

### 4.1 Project Coordinates (GAV)

Every artifact in Maven is uniquely identified by three coordinates, together called the GAV:

| Element | Meaning |
|---------|---------|
| groupID | Identifies the organization or group that owns the project (reverse domain style), e.g. com.opstree.otms |
| artifactID | The name of the specific project |
| version | The version of the artifact being built | 


### 4.2 Packaging

Declares what kind of artifact this project produces. Common value:

- jar (default) — a plain java library or application
-	war — a web application archive, deployed to a servlet container
-	pom — used for parent projects that don't produce a binary artifact themselves
- ear — an enterprise application archive bundling multiple modules

### 4.3 Properties

A Key-value block used to define reusable values - Java version, encoding, or shared dependency version

```
<properties>
  <maven.compiler.source>17</maven.compiler.source>
  <maven.compiler.target>17</maven.compiler.target>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <spring.version>6.1.6</spring.version>
</properties>

```
### 4.4 Dependencies

Lists every external library the project needs, each as a <dependency> block with its own GAV.

### 4.5 Build

Configure how the project is actually built: source directories, output directories,  final artifact name and the plugins that run during the build.

```
<build>
  <finalName>ot-microservice</finalName>
  <plugins>
     <!-- plugin declarations go here -->
  </plugins>
</build>

```
### 4.6 Parent

Point to a parent pom.xml from this project inherits properties, dependency version and plugin configuration.
```
<parent>
  <groupId>com.opstree.otms</groupId>
  <artifactId>otms-parent</artifactId>
  <version>1.0.0</version>
</parent>
```
### 4.7 Modules 

Used only in a parent pom.xml (packaging = pom) to list the sub-projects that should be built together, and in what order Maven should resolve them.
```
<modules>
  <module>user-service</module>
  <module>order-service</module>
  <module>common-lib</module>
</modules>

```

---

# 5. Use Cases 

pom.xml is used any time a Java project is built with maven. Some typical scenarios where it plays a central role:

- Adding a new library to a project by declaring it as a Dependency

- Managing a multi-module project, where a parent pom.xml defines shared configuration and versions for child modules.

- Keeping builds consistent across environments,When a team needs every build to use the same java version, dependency version, pom.xml acts as the single source of truth that every machine reads before building. 

---

# 6. Dependency & Versioning Best Practices

Dependencies are external libraries required by a Java project. Maven manages these dependencies through the `pom.xml` file.

Versioning means managing the version of these dependencies to keep the project stable and consistent.

## 6.1 Use Specific Versions

Use a specific and stable version instead of `LATEST` or open version ranges.

```xml
<version>3.2.5</version>
```

This helps ensure that the same version is used during every build.

## 6.2 Use Properties for Common Versions

If multiple dependencies use the same version, define it once using `<properties>`.

```xml
<properties>
    <spring.version>6.1.6</spring.version>
</properties>
```

Then use:

```xml
<version>${spring.version}</version>
```

This makes version updates easier.

## 6.3 Use dependencyManagement

For multi-module projects, use `<dependencyManagement>` in the parent `pom.xml` to manage dependency versions centrally.

This keeps dependency versions consistent across modules.



## 6.4 Regularly Check Dependencies

Check dependencies regularly for conflicts, unused libraries, and available updates.

```bash
mvn dependency:tree
mvn dependency:analyze
mvn versions:display-dependency-updates
```
-	Run mvn versions:display-dependency-updates to see available upgrades
-	Run mvn dependency:tree to detect duplicate or conflicting transitive versions
-	Run mvn dependency:analyze to detect unused or undeclared dependencies

---
# 7. Recommendation / Conclusion
pom.xml is an important part of a Maven-based Java project. It provides a centralized place to manage project dependencies, versions, plugins, build configuration, profiles, and project metadata.

---

# 8. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Anshul Kotiya |  anshul.kotiya.snaatak@mygurukulam.co  |

# 9. Reference

| POM | https://maven.apache.org/pom.html |
|-----|-----------------------------------|

---
