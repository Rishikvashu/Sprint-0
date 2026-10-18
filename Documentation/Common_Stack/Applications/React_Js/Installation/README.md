# React Js Installation Guide

<p align="center">
  <img width="150" height="150" alt="react-dark" src="https://github.com/user-attachments/assets/4d0832e5-0488-4db3-8e1d-e8d545105df2" />
</p>

<p align="center">
  <a href="https://react.dev/">
    <img src="https://img.shields.io/badge/Tool-ReactJS-blue?style=for-the-badge" />
  </a>
  <a href="https://en.wikipedia.org/wiki/Front-end_web_development">
    <img src="https://img.shields.io/badge/Category-Frontend-green?style=for-the-badge" />
  </a>
  <a href="https://en.wikipedia.org/wiki/DevOps">
    <img src="https://img.shields.io/badge/DevOps-Automation-orange?style=for-the-badge" />
  </a>
  <a href="https://en.wikipedia.org/wiki/Software_architecture">
    <img src="https://img.shields.io/badge/Architecture-Reference--Example-purple?style=for-the-badge" />
  </a>
</p>

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Rani Kumari | 31-08-2026 | 1.0 | Rani Kumari | 05-09-2026 | Ishaan | Anuj Jain | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#introduction)
2. [Understanding React Setup](#understanding-react-setup)
3. [React Installation Script](#react-installation-script)
4. [React Upgrade Script](#react-upgrade-script)
5. [Best Practices](#best-practices)
6. [Common Errors](#common-errors)
7. [Conclusion](#conclusion)
8. [Contact Information](#contact-information)
9. [References](#references)
---

<a id="introduction"></a>

## 1. Introduction

This document provides a **step-by-step** guide for installing and configuring **React JS** using a Bash script. It covers **Node.js and npm installation**, React project setup, **version handling**, and upgrade support to ensure React is ready for development and application deployment.

**React** is a **high-level, component-based JavaScript library** widely used for building fast, interactive user interfaces, single-page applications, and modern front-end web applications.

---

<a id="understanding-react-setup"></a>

## 2. Understanding React Setup

| Component      | Description                                                  |
|----------------|--------------------------------------------------------------|
| Node.js        | Runtime environment to execute JavaScript outside the browser |
| npm            | Package manager used to install and manage dependencies      |
| package.json   | Contains project metadata and dependency definitions         |
| node_modules/  | Directory that stores all installed dependencies             |

---

<a id="react-installation-script"></a>

## 3. React Installation Script

This script installs dependencies and runs the application.

```bash
#!/bin/bash
set -e

PROJECT_DIR="OT-Micro/frontend"

# Ask for Node.js version
read -p "Enter Node.js version: " NODE_VERSION

# Update packages
sudo apt update -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | sudo -E bash -
sudo apt install -y nodejs

# Check installed versions
echo "Node.js version: $(node -v)"
echo "npm version: $(npm -v)"

# Go to React project
cd "$PROJECT_DIR"

# Install project dependencies
npm install

# Start React application
npm start
```

<img width="535" height="287" alt="image" src="https://github.com/user-attachments/assets/7c3cc61e-1281-49b9-b53a-8668d81c916e" />


---

<img width="1456" height="819" alt="image" src="https://github.com/user-attachments/assets/118d7c78-75e0-48cd-af2f-d00bd0d9c1c9" />


## 4. React Upgrade Script

This script updates dependencies and rebuilds the application.

```bash
#!/bin/bash
set -e

PROJECT_DIR="OT-Micro/frontend"

# Go to React project
cd "$PROJECT_DIR"

# Get latest code
git pull origin main

# Install dependencies
npm ci || npm install

# Remove old build
rm -rf build

# Create new production build
npm run build

# Reload Nginx
sudo nginx -t
sudo systemctl reload nginx

echo "React application upgraded successfully"
```
<img width="1456" height="817" alt="image" src="https://github.com/user-attachments/assets/40b38853-fc57-42f6-a985-717719b80f9f" />

---

## 5. Best Practices

| Practice | Description |
|----------|--------------|
| Use `.env` files | For configuration instead of hardcoding values |
| Avoid hardcoding API URLs | Keep URLs configurable across environments |
| Use consistent Node.js version | Avoid version mismatch issues across environments |
| Maintain clean dependency versions | Prevent conflicts and ensure reproducible builds |
| Integrate with CI/CD pipelines | Automate build, test, and deployment processes |

---

<a id="common-errors"></a>

## 6. Common Errors

| Error               | Cause               | Solution                        |
| ------------------- | ------------------- | ------------------------------- |
| npm not found       | Node missing        | Install Node.js                 |
| build fails         | dependency conflict | Delete node_modules & reinstall |
| blank UI            | incorrect build     | rebuild project                 |
| port already in use | conflict            | kill process                    |

---

## 7. Conclusion

React applications are built once and deployed as static assets. Proper setup and upgrade practices ensure consistency, reliability, and smooth deployments in any environment.

---

# 8. Contact Information

| **Name** | **Email** |
| :--- | :--- |
| Rani Kumari | [rani.kumari.snaatak@mygurukulam.co](mailto:rani.kumari.snaatak@mygurukulam.co) |

---

<a id="references"></a>

## 9. References

| **Topic**                 | **Link**                                    |
| ------------------------- | ------------------------------------------- |
| **React Documentation**   | [React Documentation](https://react.dev)    |
| **Node.js Documentation** | [Node.js Documentation](https://nodejs.org) |
