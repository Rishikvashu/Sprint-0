# React JS Installation Guide

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Priyanshu | 28-08-2026 | 1.1 | Priyanshu | 29-08-2026 | Aryan Mishra |  |  |
| Priyanshu | 28-08-2026 | 1.2 | Priyanshu | 11-09-2026 | Aryan Mishra | Aditya | |
| Priyanshu | 28-08-2026 | 1.3 | Priyanshu | 15-09-2026 | Aryan Mishra | Aditya | |


---

# Table of Contents

1. [Introduction](#1-introduction)
2. [What is React JS](#2-what-is-react-js)
3. [Why React JS is Required](#3-why-react-js-is-required)
4. [Pre Requisite](#4-pre-requisite)
5. [React JS Installation Workflow](#5-react-js-installation-workflow)
6. [Different Build Tools for Installing React JS](#6-different-build-tools-for-installing-react-js)
7. [Advantages and Disadvantages](#7-advantages-and-disadvantages)
8. [Best Practices](#8-best-practices)
9. [Conclusion](#9-conclusion)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

# 1. Introduction

This document is a step-by-step installation guide for setting up React JS locally — covering everything from installing Node.js to scaffolding a project, running a development server, and producing a production-ready build. This guide walks through why React is the right choice for modern frontend development — highlighting its performance, rich ecosystem, and strong community support — and compares popular build tools like Vite, Create React App, and Next.js to help you pick the right starting point.

---

# 2. What is React JS

React is a declarative, component-based JavaScript library maintained by Meta for building single-page applications and complex UIs. Instead of directly manipulating the DOM, developers describe *what* the UI should look like for a given state, and React efficiently updates the DOM to match using a virtual DOM diffing algorithm. A typical React project is built and bundled with a build tool (Vite, Create React App, Next.js, etc.), compiled from JSX/modern JavaScript into browser-runnable code, and either served by a development server locally or built into static assets for production deployment.

---

# 3. Why React JS is Required

React JS is a popular JavaScript library designed for building fast, scalable, and interactive user interfaces. 

| Feature | Description |
| :--- | :--- |
| **Component-Based Architecture** | Encapsulates UI elements into reusable, self-contained components, reducing code duplication and improving maintainability across large applications. |
| **Virtual DOM for High Performance** | Minimizes direct manipulation of the actual DOM by computing diffs in memory, leading to faster updates and smoother rendering. |
| **Declarative UI** | Simplifies code readability by allowing developers to design views for each application state, automatically updating components when data changes. |
| **Rich Ecosystem & Flexibility** | Integrates easily with routing libraries, state management tools (like Redux or Zustand), and backend APIs without imposing a rigid monolithic structure. |
| **Strong Community & Support** | Backed by Meta and an extensive open-source community, ensuring continuous updates, comprehensive documentation, and long-term stability. |

---

# 4. Pre Requisite

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Access | Any OS with terminal access |
| Required Packages | `nodejs` (bundles `npm`); no global React package needed — `create-vite` runs via `npx`/`npm create` |
| Required Commands | `node`, `npm` |
| Permissions | No root/sudo required for project-level installs; sudo only if installing Node.js system-wide via a package manager |
| Network | Access to the npm registry (`registry.npmjs.org`) to download packages |

---

# 5. React JS Installation Workflow

### Step 1: Install Node.js (includes npm)

```bash
sudo apt update && sudo apt install -y nodejs npm
```

<img width="1315" height="158" alt="REACT-JS-1" src="https://github.com/user-attachments/assets/51051f18-5c81-43a3-8f95-a1a4a276555d" />


### Step 2: Verify

React tooling (Vite/Create React App) runs on Node.js; npm is bundled with it.

```bash
node -v
npm -v
```

<img width="1304" height="97" alt="REACT-JS-2" src="https://github.com/user-attachments/assets/da90acc1-d8ea-4696-88d1-7a72316c83c5" />


### Step 3: Scaffold a new React project

The current recommended way to start a React project is via **Vite**, which is faster than the older Create React App tooling.

```bash
npm create vite@5 my-react-app -- --template react
```

<img width="1319" height="201" alt="REACT-JS-3(2)" src="https://github.com/user-attachments/assets/a6f226b6-4dc9-45d6-8c9f-a6c196cc102c" />


### Step 4: Install dependencies

```bash
cd my-react-app
npm install
```

<img width="1319" height="250" alt="REACT-JS-3(1)" src="https://github.com/user-attachments/assets/dc343d46-4ab8-4948-b900-e201a4ef00d1" />


---

### Step 5: Start the development server

```bash
npm run dev -- --host
```

<img width="1319" height="201" alt="REACT-JS-3(3)" src="https://github.com/user-attachments/assets/ea818b4f-6884-472d-b27c-97843f98a20f" />

### Step 6: Verify on Browser 

```bash
http://<IP ADDRESS>:5173/
```

<img width="1366" height="601" alt="REACT-JS-4" src="https://github.com/user-attachments/assets/43f6a473-3201-43cd-b468-d3824fde9a6c" />

---

# 6. Different Build Tools for Installing React JS

| **Tool** | **Description** |
| -------- | --------------- |
| Vite | Modern, fast build tool and dev server; the current recommended way to scaffold a plain React SPA (`npm create vite@latest`). |
| Create React App (CRA) | The historical official React starter (`npx create-react-app`); now in maintenance mode and no longer actively recommended by the React team. |
| Next.js | A full React framework (`npx create-next-app`) adding server-side rendering, routing, and API routes on top of React. |
| Node Version Manager (nvm) | Manages multiple Node.js versions on one machine, so different React projects can pin the Node version they need. |

---

# 7. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| --------------- | ------------------ |
| Component-based architecture promotes reusable, testable UI code | Requires a build step/toolchain (Node, bundler) rather than being usable as a simple `<script>` include for larger apps |
| Huge ecosystem of libraries, tooling, and community support | Rapid ecosystem churn (CRA deprecation, tool changes) can make "the right way to install" a moving target |
| Vite-based setup is fast to install and start (dev server ready in ~200ms in this test) | JSX and modern JS syntax require transpilation, adding a layer of build complexity for newcomers |
| Hot module reload gives near-instant feedback during development | Bundle size and performance require active management (code-splitting, lazy loading) as an app grows |
| Production builds are simple static assets, deployable anywhere | Version mismatches between Node/npm and project tooling are a common source of install failures |

---

# 8. Best Practices

1. Use an LTS Node.js version and pin the project-specific version with `nvm` to ensure long-term stability.
2. Prefer Vite for new plain-React projects because it provides a faster and more modern development experience than Create React App.
3. Commit `package-lock.json` to ensure local, CI, and team installations use the same dependency tree.
4. Run `npm install` after cloning to install the dependencies defined by the project's lockfile.
5. Run `npm run build` locally before deployment to catch production build errors early.

---

# 9. Conclusion

For new React projects, use Node.js (LTS) + Vite with `npm create vite@latest`. Vite quickly scaffolds a minimal React project with a fast development server and HMR. Use `npm run build` to create an optimized production build. Use Create React App only for maintaining existing CRA projects, not for new applications. For file-based routing, or backend API routes, prefer **Next.js** over plain Vite + React.

---

# 10. Contact Information

| **Name** | **Team** | **Email** |
| -------- | --------- | ------ | 
| Priyanshu | Kubeclan | [priyanshu.banwala.snaatak@mygurukulam.co](mailto:priyanshu.banwala.snaatak@mygurukulam.co) |
---

# 11. References

| **Description** | **Topic** |
| --------- | --------------- |
| Official React documentation, including "Quick Start" and "Installation" guides. | [React Official Documentation](https://react.dev/) |
| Official documentation for the Vite build tool and dev server used to scaffold this project. | [Vite Documentation](https://vite.dev/guide/) |
| Official Node.js documentation and downloads, including LTS releases. | [Node.js Documentation](https://nodejs.org/en/docs) |
