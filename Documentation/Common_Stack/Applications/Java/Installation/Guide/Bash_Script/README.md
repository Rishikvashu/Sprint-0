# Java Installation via Bash Script

<p align="left">
  <img width="120" height="120" alt="Java" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" />
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
3. [Operating System and Package Setup](#3-operating-system-and-package-setup)
4. [Java Installation Script](#4-java-installation-script)
5. [Script Usage](#5-script-usage)
6. [Troubleshooting](#6-troubleshooting)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

# 1. Introduction

This Document provides a standardized procedure for installing and managing OpenJDK on Ubuntu-based environments using an automated Bash script.

---

# 2. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| **Operating System** | Ubuntu-based environment |
| **Access** | Terminal / SSH access |
| **Permissions** | `sudo` privileges for package management |
| **Shell** | Bash |
| **Package Manager** | `apt` / `apt-get` |
| **Internet Access** | Required for downloading packages from Ubuntu repositories |

---

# 3. Operating System and Package Setup

Refreshes the available package information before installation:

```bash
sudo apt update
```

---

# 4. Java Installation Script

Create a script file named `java_manager.sh` with the following dynamic, upgrade-aware code:

```bash
#!/bin/bash
set -e

# Display usage instructions
print_usage() {
    echo "Usage: $0 [OPTIONS]"
    echo "Options:"
    echo "  --install, -i <version>  Install or upgrade a specific Java major version available in APT (e.g., 17, 21)"
    echo "  --set-default, -s        Configure active default Java runtime and compiler alternatives"
    echo "  --help, -h               Display usage instructions"
    echo ""
    echo "Running without arguments launches interactive mode to enter versions manually,"
    echo "browse available repository packages, or configure default alternatives."
}

# Verify that the current user has sudo privileges
check_sudo() {
    if ! sudo -v >/dev/null 2>&1; then
        echo "Error: Sudo privileges are required to execute this script." >&2
        exit 1
    fi
}

# Validate that the version input is a positive integer format
validate_version() {
    local version="$1"
    if [[ ! "$version" =~ ^[1-9][0-9]*$ ]]; then
        echo "Error: Invalid Java version '$version'. Please provide a valid major version number (e.g., 17, 21)." >&2
        return 1
    fi
    return 0
}

# Dynamically retrieve available OpenJDK major versions from configured APT repositories
get_available_versions() {
    local raw_pkgs
    raw_pkgs=$(apt-cache pkgnames openjdk-) || return 1
    [ -z "$raw_pkgs" ] && return 0

    # Extract major version number from openjdk-<major>-jdk packages
    echo "$raw_pkgs" | awk -F'-' '$1=="openjdk" && $3=="jdk" && $2 ~ /^[0-9]+$/ {print $2}' | sort -n -u
}

# Install or upgrade the requested OpenJDK version
# Accepts an optional second argument (true) to skip redundant apt-get update
install_java() {
    local version="$1"
    local skip_update="${2:-false}"

    validate_version "$version" || return 1

    local pkg="openjdk-${version}-jdk"
    check_sudo

    if [ "$skip_update" != "true" ]; then
        echo "Updating package index..."
        sudo apt-get update
    fi

    # Verify that the package exists in the APT repository
    if ! apt-cache show "$pkg" >/dev/null 2>&1; then
        echo "Error: Package '$pkg' is not available in the current APT repositories." >&2
        return 1
    fi

    # Retrieve candidate and installed versions to handle upgrades idempotently
    local policy_output candidate_ver installed_ver
    policy_output=$(apt-cache policy "$pkg")
    candidate_ver=$(awk '/Candidate:/ {print $2}' <<< "$policy_output")

    if [ -z "$candidate_ver" ] || [ "$candidate_ver" = "(none)" ]; then
        echo "Error: No installation candidate found for package '$pkg' in configured repositories." >&2
        return 1
    fi

    installed_ver=$(dpkg-query -W -f='${Version}' "$pkg" 2>/dev/null || true)

    if [ -n "$installed_ver" ]; then
        if dpkg --compare-versions "$candidate_ver" le "$installed_ver"; then
            echo "Java $version ($pkg) is already installed and up to date ($installed_ver). Skipping installation."
            return 0
        else
            echo "Upgrading Java $version ($pkg) from version $installed_ver to $candidate_ver..."
        fi
    else
        echo "Installing $pkg..."
    fi

    sudo apt-get install -y "$pkg"

    # Explicitly verify package installation state
    if ! dpkg -s "$pkg" >/dev/null 2>&1; then
        echo "Error: Package $pkg failed to install." >&2
        return 1
    fi

    echo "Java $version ($pkg) installed successfully."
    echo ""
    echo "Current active/default Java version:"
    if command -v java >/dev/null 2>&1; then
        java -version
    else
        echo "No default Java binary currently configured in PATH."
    fi

    if command -v javac >/dev/null 2>&1; then
        echo ""
        echo "Current active/default Java compiler:"
        javac -version
    fi
}

# Configure default Java runtime and compiler alternatives
set_default_java() {
    check_sudo

    if ! update-alternatives --list java >/dev/null 2>&1; then
        echo "Error: No Java installations found to configure as default." >&2
        exit 1
    fi

    echo "Configuring default Java runtime..."
    sudo update-alternatives --config java

    if update-alternatives --list javac >/dev/null 2>&1; then
        echo "Configuring default Java compiler..."
        sudo update-alternatives --config javac
    fi

    echo "Active Java version:"
    java -version
}

# Interactive menu for manual or dynamic installation
interactive_mode() {
    local choice ver ver_index selected_version
    local -a versions

    echo "======================================"
    echo " Java Installation and Manager Script "
    echo "======================================"
    echo "1) Enter Java version manually"
    echo "2) Show available Java versions"
    echo "3) Set active/default Java version"
    echo "4) Exit"
    read -rp "Select an option (1-4): " choice

    case "$choice" in
        1)
            read -rp "Enter Java version: " ver
            install_java "$ver"
            ;;
        2)
            check_sudo
            echo "Updating package index..."
            sudo apt-get update

            echo "Fetching available OpenJDK versions from repositories..."
            mapfile -t versions < <(get_available_versions)

            if [ "${#versions[@]}" -eq 0 ]; then
                echo "No OpenJDK packages found in current APT repositories."
                exit 1
            fi

            echo "Available OpenJDK versions:"
            for i in "${!versions[@]}"; do
                printf "  %d) Java %s (openjdk-%s-jdk)\n" "$((i + 1))" "${versions[i]}" "${versions[i]}"
            done

            read -rp "Select a version to install (1-${#versions[@]}): " ver_index
            if [[ "$ver_index" =~ ^[1-9][0-9]*$ ]] && [ "$ver_index" -le "${#versions[@]}" ]; then
                selected_version="${versions[$((ver_index - 1))]}"
                # Skip duplicate apt-get update since metadata was just refreshed
                install_java "$selected_version" true
            else
                echo "Error: Invalid selection." >&2
                exit 1
            fi
            ;;
        3)
            set_default_java
            ;;
        4)
            echo "Exiting."
            exit 0
            ;;
        *)
            echo "Error: Invalid selection." >&2
            exit 1
            ;;
    esac
}

# Main CLI entrypoint
case "$1" in
    --install|-i)
        if [ -z "$2" ]; then
            echo "Error: Version argument missing." >&2
            print_usage
            exit 1
        fi
        install_java "$2"
        ;;
    --set-default|-s)
        set_default_java
        ;;
    --help|-h)
        print_usage
        ;;
    "")
        interactive_mode
        ;;
    *)
        echo "Error: Unknown option '$1'." >&2
        print_usage
        exit 1
        ;;
esac
```

The script dynamically discovers available OpenJDK packages from configured APT repositories, compares package versions for idempotent installation and upgrades, verifies package installation, and provides interactive or CLI options for configuring system defaults.

---

# 5. Script Usage

## Step 1: Make the Script Executable

```bash
chmod +x java_manager.sh
```

<p align="left">
  <img width="550" height="77" alt="image" src="https://github.com/user-attachments/assets/130a8ab8-cade-42f0-b4ce-c1d16cd05541" />
</p>

## Step 2: Run Interactive Mode

```bash
./java_manager.sh
```

<img width="483" height="173" alt="image" src="https://github.com/user-attachments/assets/27cc0573-4a2e-4dd6-b57f-7f945479d309" />


## Step 3: Install a Specific Java Version

```bash
./java_manager.sh --install 17
```
<img width="935" height="240" alt="image" src="https://github.com/user-attachments/assets/4e452835-31d0-47e9-ac92-718ba9a7577e" />


The same command can be used with any valid OpenJDK major version available in the APT repositories (e.g., 17, 21, 25).

## Step 4: Set Default Java Version

```bash
./java_manager.sh --set-default
```
<img width="936" height="238" alt="image" src="https://github.com/user-attachments/assets/59fc0f4b-471d-4ce6-9395-26d84de628e4" />


## Step 5: Display Help

```bash
./java_manager.sh --help
```

<img width="924" height="191" alt="image" src="https://github.com/user-attachments/assets/d133b443-b049-495c-8c1a-7c450ca9de55" />


---

# 6. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| --------- | --------- | ------------ |
| `java: command not found` | Java is not installed or unavailable in PATH | Install an available Java version using the script |
| `Permission denied` | Script is not executable | Run `chmod +x java_manager.sh` |
| `Sudo privileges required` | User lacks sudo access | Use an account with sudo privileges |
| `Package not available in repositories` | Requested version is not in configured APT sources | Run `sudo apt update` or choose an available version from option 2 |
| `Incorrect active Java version` | Another Java version is selected | Run `./java_manager.sh --set-default` |

---

# 7. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| **Use LTS releases** | Prefer Long-Term Support (LTS) releases (e.g., Java 17, 21) for production workloads |
| **Avoid unnecessary reinstallation** | The script automatically skips installation if the package is installed and up to date |
| **Use sudo appropriately** | Use elevated privileges only for system-level package operations |
| **Use update-alternatives** | Use the standard Ubuntu mechanism to switch the active Java runtime and compiler |
| **Test script changes** | Validate script modifications in a non-production Ubuntu environment before production use |

---

# 8. Conclusion

This Bash script provides a standardized and dynamic method for installing and managing OpenJDK versions on Ubuntu-based environments. It discovers available repository packages dynamically, handles package upgrades idempotently, and provides a consistent method for configuring the active Java version.

---

# 9. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Shivam Tomar | [shivam.tomar.snaatak@mygurukulam.co](mailto:shivam.tomar.snaatak@mygurukulam.co) |

---

# 10. References

| **Topic** | **Link** |
| --------- | -------- |
| OpenJDK Official Website | [openjdk.org](https://openjdk.org/) |
| Ubuntu Package Management | [ubuntu.com - Package Management](https://ubuntu.com/server/docs/package-management) |
| Debian update-alternatives Manual | [debian.org - update-alternatives](https://manpages.debian.org/bookworm/dpkg/update-alternatives.1.en.html) |
| GNU Bash Reference Manual | [gnu.org - bash](https://www.gnu.org/software/bash/manual/) |
