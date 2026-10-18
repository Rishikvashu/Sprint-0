# Golang Installation Documentation
 ![image](https://cdn.dribbble.com/userupload/2624050/file/original-59266f4dea1c2aa43f2064cc0f3b165a.png?format=webp&resize=400x300&vertical=center)

---
##  **Author Information**
| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Mansoor Alam | 26-08-2026 | 1.0 | Mansoor Alam | 26-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |



---



##  Table of Contents

1. [Introduction](#1-introduction)  
2. [Golang Installation Guide (Step by Step) in Ubuntu](#2-golang-installation-guide-step-by-step-in-ubuntu)  
   - [Step 1: Download .tar.gz](#step-1-download-targz)  
   - [Step 2: Extract it](#step-2-extract-it)  
   - [Step 3: Add Go to your PATH](#step-3-add-go-to-your-path)  
   - [Step 4: To verify](#step-4-to-verify)  
3. [Setting up Workspace](#3-setting-up-workspace)  
   - [Go directory structure](#go-recommends-a-directory-structure-like)  
   - [Set environment variables](#set-environment-variables-in-bashrc-or-zshrc)  
4. [Test Installation](#4-test-installation)  
   - [Create a test file](#create-a-test-file)  
   - [Create main.go](#create-maingo)  
   - [Run it](#run-it)  
5. [Confirm Everything Works](#5-confirm-everything-works)  
6. [Conclusion](#6-conclusion)  
7. [Contact](#7-contact)  
8. [References](#7-references)

---




## 1. Introduction
This documentation outlines the core concepts and practical value of the Go programming language (Golang), highlighting why it was created, what it offers, and step by step installation guide.

---

## 2. What is Golang?
Go, also known as **Golang**, is an open-source programming language developed by Google.

Go is commonly used for:

- Backend applications
- REST APIs
- Microservices
- Cloud-native applications
- Command-line tools
- DevOps and infrastructure tools

---
## 3. Golang Installation Guide (Step by Step) in Ubuntu.

### Step-1: Check Existing Go Installation
Before installing Go, check whether Go is already installed.
```
go version
```
You can also check the location of the Go binary:
```
which go
```
### Step 2: Update Package Index
First, update the Ubuntu package index:
```
sudo apt update
```

### Step 3: Download Go
```
wget https://go.dev/dl/go1.22.1.linux-amd64.tar.gz
```
Verify that the downloaded archive exists:
```
ls -lh go1.22.1.linux-amd64.tar.gz
```

### Step 4: Extract Go

```
sudo tar -C /usr/local -xzf go1.22.1.linux-amd64.tar.gz
```
This installs Go under:
```
/usr/local/go
```
Verify the installation directory:
```
ls -ld /usr/local/go
```

### Step 5: Configure PATH
The Go executable is located at:
```
/usr/local/go/bin
```
Add this directory to the user's PATH:
```
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
```

### Step 6: Reload Shell Configuration
```
source ~/.bashrc
```
Check the PATH:
```
echo $PATH
```
You can also check the Go binary:
```
which go
```

Step 7: Verify Go Installation
```
go version
```
<img width="1144" height="130" alt="img1" src="https://github.com/user-attachments/assets/82594f61-f943-4973-959f-abe51250a913" />

---

## 4.  Test Go Installation
To make sure Go is not only installed but also working correctly, create a small test application.

### Step 1: Create Test Directory

```
mkdir -p ~/go-test
```
Move into the directory:
```
cd ~/go-test
```

### Step 2: Initialize Go Module
```
go mod init example.com/go-test
```
This creates a go.mod file.
Verify:
```
ls -lh
```
The go.mod file is used to define the Go module and manage its dependencies.


<img width="1081" height="162" alt="img2" src="https://github.com/user-attachments/assets/0baf7706-022a-4078-a939-084c006d6fb8" />


### Step 3: Create main.go
Create the Go source file:
```
nano main.go
```
Add the following code:
```
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```
<img width="1183" height="197" alt="img3" src="https://github.com/user-attachments/assets/32a02dfc-a811-474f-9bcc-a7ceb3e2f9f1" />

### Step 4: Run the Application
```
go run main.go
```
**Output**
```
Hello, World!
```

<img width="944" height="78" alt="img4" src="https://github.com/user-attachments/assets/008df1c8-b654-48cd-809f-d8fa5c6a6503" />


## Step 5: Confirm Everything Works

Run:
```bash
go env
```
It should show your Go environment:
- `GOROOT` – Go installation path
- `GOPATH` – Workspace path
- `GOOS`, `GOARCH`, etc.

---



## 5. Conclusion

Golang is a modern, efficient, and powerful language built with real-world software engineering in mind. Its clean syntax, fast performance, and built-in concurrency make it an excellent choice for scalable and maintainable software systems — especially in the era of microservices and cloud computing.

---

## 6. Contact

| Name         | Email Address                                 |
|--------------|-----------------------------------------------|
| Mansoor Alam   | mansoor.alam.snaatak@mygurukulam.co             |
---

## 7. References


| **Title**                        | **Link**                                                                                      |
|----------------------------------|-----------------------------------------------------------------------------------------------|
| Official Go Documentation  | [Link](https://golang.org/doc/) |
| Go official | [https://go.dev/dl/](https://go.dev/dl/) |
