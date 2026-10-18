# SOP for npm Installation

<p align="left">
  <img width="240" height="110" alt="React" src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- | --------------- |
| Shivam Tomar | 24-08-2026 | v1.1 | Shivam Tomar | 06-09-2026 | Team | Ishaan | Anuj Jain | Piyush Upadhyay |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [Node.js and npm Setup](#3-nodejs-and-npm-setup)
4. [React Project Setup](#4-react-project-setup)
5. [Running the React Application](#5-running-the-react-application)
6. [Troubleshooting](#6-troubleshooting)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

# 1. Introduction

This Document provides a standardized procedure for setting up Node.js and npm and using them for a React JS development environment.

**npm** (Node Package Manager) is the default package manager for Node.js, used to install, share, and manage project dependencies, as well as execute automation scripts in React applications.

---

# 2. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| **Operating System** | Ubuntu / Debian or supported Linux distribution |
| **Access** | Terminal / SSH access |
| **Permissions** | `sudo` privileges for package installation |
| **Internet Access** | Required for downloading Node.js and npm packages |
| **Project Directory** | Required for housing the application |

---

# 3. Node.js and npm Setup

## Step 1: Update System Packages

```bash
sudo apt update && sudo apt install -y curl gnupg
```

## Step 2: Install Node.js LTS

```bash
# Add NodeSource official LTS repository
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

# Install Node.js
sudo apt install -y nodejs
```

## Step 3: Install the Latest npm Version

```bash
sudo npm install -g npm@latest
```

<img width="741" height="66" alt="image" src="https://github.com/user-attachments/assets/1f93746e-ecc6-425d-b6a9-68f1807f6928" />



## Step 4: Verify Installation

```bash
node --version
npm --version
```

<img width="457" height="73" alt="image" src="https://github.com/user-attachments/assets/bece355f-cb09-4bbb-beb9-ef2e071e67a9" />


---

# 4. React Project Setup

## Step 1: Create a React Application

```bash
npx create-react-app my-react-app
```

<img width="705" height="418" alt="image" src="https://github.com/user-attachments/assets/7da9997f-9bca-4536-876e-3738779dbb69" />


## Step 2: Navigate into the Project Directory

```bash
cd my-react-app
```

---

# 5. Running the React Application

## Step 1: Start the Development Server

Inside the root directory of your React project:

```bash
npm start
```

<img width="554" height="252" alt="image" src="https://github.com/user-attachments/assets/65b6d759-c57f-4835-8301-64d7ffb99492" />


## Step 2: Access the Application

The React application launches on default port 3000:
**http://localhost:3000**

---

# 6. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| --------- | --------- | ------------ |
| `node: command not found` | Node.js is not installed or not in system PATH | Install Node.js via NodeSource repository and restart the terminal |
| `Port 3000 is already in use` | Another process is occupying port 3000 | Accept alternate port prompt (`Y`) or terminate conflicting process (`kill -9 $(lsof -t -i:3000)`) |
| `EACCES: permission denied` | Insufficient permissions for global installations | Configure npm prefix directory for user space or avoid unnecessary global installations |
| Corrupted or missing `node_modules` | Incomplete installation or package conflict | Run `rm -rf node_modules package-lock.json && npm install` |
| `npm ERR! code ENOENT` | Command executed outside the project folder | Ensure you navigate (`cd`) into the directory containing `package.json` |

---

# 7. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| **Use LTS Releases** | Always use Node.js Active LTS releases for stability and long-term security support. |
| **Exclude `node_modules`** | Always add `node_modules/` to `.gitignore` to avoid committing bulky dependency packages. |
| **Commit `package-lock.json`** | Always commit `package-lock.json` to version control to guarantee identical dependency resolution across environments. |
| **Security Auditing** | Regularly run `npm audit` and `npm audit fix` to identify and patch security vulnerabilities. |
| **Prefer Local Installations** | Install dependencies locally within the project rather than globally, and use `npx` for one-off binaries. |

---

# 8. Conclusion

This Document provides a standardized procedure for installing Node.js and npm, bootstrapping a React JS application, and successfully launching the local development server.

---

# 9. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Shivam Tomar | [shivam.tomar.snaatak@mygurukulam.co](mailto:shivam.tomar.snaatak@mygurukulam.co) |

---

# 10. References

| **Topic** | **Link** |
| --------- | -------- |
| Node.js Official Documentation | [nodejs.org](https://nodejs.org/) |
| npm CLI Documentation | [docs.npmjs.com](https://docs.npmjs.com/) |
| React Official Documentation | [react.dev](https://react.dev/) |
| Create React App Documentation | [create-react-app.dev](https://create-react-app.dev/) |
