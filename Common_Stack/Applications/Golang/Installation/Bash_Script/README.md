# Golang Installation via Bash Script (Documentation)

<p align="center">
<img width="369" height="137" alt="image" src="https://github.com/user-attachments/assets/d704e199-dcab-418e-9292-9e6a0f8a5eea" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Maqbool Alam | 26-08-2026 | 1.1 | Maqbool Alam | 10-09-2026 | Rajnish Sharma  | Pritam/Komal | Abhishek/Manish Nautiyal |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Why Golang Installation via Bash Script is Required](#2-why-golang-installation-via-bash-script-is-required)
3. [Workflow Diagram](#3-workflow-diagram)
4. [Bash Script](#4-bash-script)
5. [Script Usage](#5-script-usage)
6. [Multiple Go Versions](#6-multiple-go-versions)
7. [Upgrade Go Version](#7-upgrade-go-version)
8. [Advantages and Disadvantages](#8-advantages-and-disadvantages)
9. [Best Practices](#9-best-practices)
10. [Recommendation / Conclusion](#10-recommendation--conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

# 1. Introduction

This document provides a standardized approach for installing and managing **Golang** on Linux systems using a reusable Bash script.

The script is designed to support:

- Fresh Go installation.
- Installation of a specific Go version.
- Multiple Go versions on the same server.
- Switching between installed versions.
- Upgrading an existing Go installation.
- Removing an installed Go version.
- Verification of the active Go version.

---

# 2. Why Golang Installation via Bash Script is Required

A reusable installation script is useful because it:

- Reduces manual installation effort.
- Standardizes Go installation across servers.
- Supports multiple Go versions.
- Makes version upgrades predictable.
- Provides repeatable installation and removal operations.
- Reduces configuration mistakes.
- Simplifies automation through CI/CD or server-provisioning workflows.

---

# 3. Workflow Diagram

<details>
<summary>Click to Expand Golang Installation Workflow Diagram</summary>

<img width="1335" height="321" alt="image" src="https://github.com/user-attachments/assets/963c1647-2228-4f62-b6d3-6cd21a2e54c6" />

</details>

---

# 4. Bash Script

Create the installation script:

```bash
nano install-go.sh
```
./Script/install-go.sh


# 5. Script Usage

## Step 1: Make the Script Executable

```bash
chmod +x install-go.sh
```

<img width="1064" height="140" alt="screen1" src="https://github.com/user-attachments/assets/0fac6a96-673d-4c02-ab63-e30a976ce7a9" />

---

## Step 2: Install a Specific Go Version

Example:

```bash
sudo ./install-go.sh install 1.24.6
```

The script will:

1. Validate the version.
2. Detect the server architecture.
3. Download the appropriate Go archive.
4. Extract Go.
5. Store the installation under `/usr/local/go-versions/`.
6. Update `/usr/local/go`.
7. Configure `/etc/profile.d/go.sh`.
8. Make the selected version active.

<img width="1064" height="301" alt="screen2" src="https://github.com/user-attachments/assets/130eadd1-373d-4e4a-a563-6eaf05ea8a9b" />

---

## Step 3: Load the PATH Configuration

```bash
source /etc/profile.d/go.sh
```

Verify:

```bash
go version
```

Expected:

```text
go version go1.24.6 linux/amd64
```

<img width="1064" height="83" alt="screen3" src="https://github.com/user-attachments/assets/35498128-c5d1-4ba5-8d58-16bfba574338" />

---

## Step 4: List Installed Versions

```bash
sudo ./install-go.sh list
```

Example:

```text
1.20.1
1.24.6
```

<img width="1064" height="83" alt="screen4" src="https://github.com/user-attachments/assets/3ced85ee-d470-4fd8-a023-c5877e12a198" />

---

## Step 5: Check Current Version

```bash
sudo ./install-go.sh current
```

Example:

```text
Active installation:
/usr/local/go-versions/go1.20.1

go version go1.20.1 linux/amd64
```

<img width="1064" height="102" alt="screen5" src="https://github.com/user-attachments/assets/801b8652-c17b-4e38-916a-16a80aa1603d" />

---

# 6. Multiple Go Versions

The script supports multiple versions on the same server.

Install the first version:

```bash
sudo ./install-go.sh install 1.20.1
```

<img width="1064" height="284" alt="screen6" src="https://github.com/user-attachments/assets/3b2f9f94-b485-4ae6-a595-4ab4c2ea27be" />

Install another version:

```bash
sudo ./install-go.sh install 1.24.6
```

<img width="1064" height="301" alt="screen2" src="https://github.com/user-attachments/assets/13735018-0ade-4580-aa53-1ffa53698b72" />

List installed versions:

```bash
sudo ./install-go.sh list
```

Output:

```text
1.20.1
1.24.6
```

<img width="1064" height="102" alt="screen5" src="https://github.com/user-attachments/assets/80f17202-5737-460e-957b-17d462607404" />

Switch to Go 1.20.1:

```bash
sudo ./install-go.sh use 1.20.1
```

Verify:

```bash
source /etc/profile.d/go.sh
go version
```

Switch back:

```bash
sudo ./install-go.sh use 1.24.6
```

Verify:

```bash
go version
```

Expected:

```text
go version go1.24.6 linux/amd64
```

<img width="1064" height="133" alt="screen7" src="https://github.com/user-attachments/assets/7286f31b-16a1-4cb1-89ae-3cdccaeea2c3" />

The `/usr/local/go` symlink determines which installed version is the system-wide default.

---

# 7. Upgrade Go Version

## Step 1: Check Current Version

```bash
sudo ./install-go.sh current
```

Example:

```text
go version go1.20.1 linux/amd64
```

<img width="1064" height="71" alt="screen8" src="https://github.com/user-attachments/assets/1aa485e0-64b6-4973-a3c3-63edb6f5c730" />

---

## Step 2: Install the New Version

For example:

```bash
sudo ./install-go.sh upgrade 1.24.6
```

<img width="1064" height="119" alt="screen9" src="https://github.com/user-attachments/assets/a92c0d00-1627-4929-8aca-a85e47208303" />


The script installs the new version without deleting the old version.

---

## Step 3: Verify the Upgrade

```bash
source /etc/profile.d/go.sh
go version
```

Expected:

```text
go version go1.24.6 linux/amd64
```

<img width="1064" height="81" alt="screen10" src="https://github.com/user-attachments/assets/aebc9b5b-60ce-49f0-a714-3ff2564ebb52" />

---

## Step 4: Remove the Old Version

After confirming that applications work correctly:

```bash
sudo ./install-go.sh remove 1.20.1
```

<img width="1064" height="584" alt="screen11" src="https://github.com/user-attachments/assets/c5d8d14a-544d-4ef0-aeef-d8eb3b510991" />

> **NOTE**
> 
> The script intentionally prevents removal of the currently active Go version. Switch to another version first.

---

# 8. Advantages and Disadvantages

| **Advantages** | **Disadvantages** |
| -------------- | ----------------- |
| Supports multiple Go versions | Requires root/sudo access |
| Easy version switching | Requires manual verification of release availability |
| Simplifies upgrades | Script downloads binaries from the Go distribution site |
| Repeatable installation process | PATH changes require a new shell or sourcing the profile |
| Keeps versions isolated | Additional disk space is required for multiple versions |
| Supports both amd64 and arm64 | Version-specific application compatibility still needs testing |

---

# 9. Best Practices

| **Best Practice** | **Description** |
|---|---|
| Pin exact versions | Use a specific version such as `1.24.6` |
| Test before switching | Validate builds and tests before activation |
| Keep old versions | Retain the previous version for easy rollback |
| Use dedicated directory | Store versions under `/usr/local/go-versions/` |
| Verify architecture | Ensure the binary matches the server architecture |
| Use checksums | Verify SHA256 checksums in production |
| Clean unused versions | Remove obsolete versions after migration |

---

# 10. Recommendation / Conclusion

A version-aware Bash installation script is recommended for managing multiple Go versions in a controlled and repeatable way.

Repeatable installation
Multiple Go versions
Controlled version switching
Easy upgrades and rollback
Centralized versions under /usr/local/go-versions/

For production, add SHA256 checksum verification and test against approved Go versions.

---

# 11. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Maqbool Alam | maqbul.alam.snaatak@mygurukulam.co |

---

# 12. References

| **Topic** | **Description** | **Link** |
| --------- | ----------- | -------- |
| Go Downloads | Official Go binary downloads and releases | https://go.dev/dl/ |
| Go Documentation | Official Go language and tooling documentation | https://go.dev/doc/ |
| Go Installation | Official installation guidance | https://go.dev/doc/install |
| Go `go env` / Environment Variables | Reference for GOROOT, GOPATH, and related settings | https://go.dev/cmd/go/#hdr-Environment_variables |
