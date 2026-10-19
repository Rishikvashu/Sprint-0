# Shared Library Documentation

<p align="center">
  <img src="https://miro.medium.com/v2/resize:fit:1116/1*5A8OrocBg3OhG4XHYoF3tQ.jpeg" width="500"/>
</p>

---

## Author Information
| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Mansoor Alam | 28-08-2026 | 1.0 | Mansoor Alam | 28-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |
| Mansoor Alam | 28-08-2026 | 1.1 | Mansoor Alam | 08-09-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |


---

## Table of Contents

- [Introduction](#introduction)
- [What is a Shared Library?](#what-is-a-shared-library)
- [Why Use a Shared Library?](#why-use-a-shared-library)
- [Jenkins Shared Library Structure](#jenkins-shared-library-structure)
  - [`vars/`](#vars)
  - [`src/`](#src)
  - [`resources/`](#resources)
- [Workflow](#workflow)
  - [Execution Flow](#execution-flow)
- [Advantages of the Shared Library](#advantages-of-the-shared-library)
- [Disadvantages of the Shared Library](#disadvantages-of-the-shared-library)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)
- [Contacts](#contacts)
- [Reference Table](#reference-table)
---

## Introduction
This document explains what a Jenkins Shared Library is, why it’s useful, and how to structure and use it effectively. It also highlights key differences between vars and src folders, shares best practices, and outlines a typical execution workflow.

---

## **What is a Shared Library?**

A **Shared Library** is a collection of reusable code that can be used
across multiple Jenkins pipelines.

In Jenkins, Shared Libraries help teams avoid repeating the same
Pipeline code by providing reusable functions, steps, and classes in a
centralized location.

---

## **Why Use a Shared Library?**

- **Code Reuse:** Write common logic once and use it in multiple
pipelines.
- **Easy Maintenance:** Common logic is maintained in one place.
- **Less Duplication:** Avoid repeating the same code in different
Jenkinsfiles.
- **Standardization:** Maintain common standards across projects.
- **Version Control:** Use library versions and roll back when
required.

---

# Jenkins Shared Library Structure

```
(root)
├── vars/
│   └── deployApp.groovy         # Entry points (exposed pipeline functions)
├── src/
│   └── org/
│       └── example/
│           └── Helper.groovy    # Supporting reusable classes and methods
├── resources/
│   └── config.yaml              # Any static config files
└── README.md
```

### `vars/`
The `vars/` directory contains reusable Pipeline steps and global variables that can be directly used in Jenkinsfiles.

For detailed documentation, see [`VARS.md`](https://github.com/SnaatakKubeClan/Sprint-0/blob/SCRUM-52-MANSOOR/Documentation/Common_Stack/Shared_Library/DOC/VARS.md).


### `src/`
The `src/` directory contains reusable Groovy or Java classes used to organize class-based functionality in the Shared Library.

For detailed documentation, see [`SRC.md`](https://github.com/SnaatakKubeClan/Sprint-0/blob/SCRUM-52-MANSOOR/Documentation/Common_Stack/Shared_Library/DOC/SRC.md).

### `resources/`
The `resources/` directory contains static resources such as configuration files, templates, or other assets that the Jenkins pipeline might need to reference during execution. The `config.yaml` file, as mentioned in your structure, likely holds configuration values that control certain aspects of the pipeline.


---


## **Workflow**
### Execution Flow

<img width="933" height="571" alt="shared library flow" src="https://github.com/user-attachments/assets/07d4139a-a70c-4176-be51-dbcbb737cb46" />


---

## **Advantages of the Shared Library**

| Feature               | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **Reusability**        | Write once, use across multiple Jenkins pipelines.                          |
| **Cleaner Pipelines**  | Keeps Jenkinsfile logic minimal and more readable.                        |
| **Modular Design**     | Allows separation of concerns through reusable utilities and classes.      |
| **Centralized Maintenance** | Any updates in the library reflect across all using pipelines.        |
| **Consistency**        | Ensures coding and execution standards across teams/projects.               |

---

## **Disadvantages of the Shared Library**

| Feature                  | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| **Learning Curve**        | Developers need to understand Groovy, `vars/`, `src/`, and Jenkins shared library structure. |
| **Debugging Difficulty**  | Errors within the shared library can be harder to trace from the pipeline UI. |
| **Version Control Complexity** | Managing different library versions across multiple teams/projects can get tricky. |
| **CI/CD Impact**          | Bugs in shared code can affect all consuming pipelines unless versioned carefully. |


---


## Best Practices

- **Keep Responsibilities Clear**  
  Use `vars/` for Pipeline-facing steps and use `src/` when functionality
  is better organized as reusable classes.

- **Use Meaningful Names**  
  Use clear and consistent names for Pipeline steps, classes, methods,
  and variables so that the shared code is easy to understand and use.

- **Avoid Hardcoded Environment-Specific Values**  
  Keep environment-specific configuration outside the shared library
  whenever possible. Use parameters or external configuration when
  different environments require different values.

---

## Conclusion

Through this documentation, I learned how Jenkins Shared Libraries help
reuse and organize Pipeline code across multiple projects.

I understood the purpose of `vars/`, `src/`, and `resources/`, how they
work together, and how proper structure and best practices make shared
code easier to maintain.

---

## Contacts

| Name | Email Address |
| --- | --- |
| Mansoor Alam | mansoor.alam.snaatak@mygurukulam.co |

---

## Reference Table

|      Descriptions                                                                                                                       |              Links              |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
|    Jenkins official shared library docs| https://www.jenkins.io/doc/book/pipeline/shared-libraries/    |
|     Shared Libraries tutorial and guide         |  https://techforyou.medium.com/shared-libraries-in-jenkins-pipeline-a-comprehensive-guide-with-examples-83ddf0eec46e |
