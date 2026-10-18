# SOP: Gunicorn

<p align="center">
<img width="740" height="162" alt="image" src="https://github.com/user-attachments/assets/8ea8fcb7-e8de-410c-b158-6d217f571c0e" />
</p>

---

# Author Table

| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Maqbool Alam | 25-08-2026 | 1.0 | Maqbool Alam | 25-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Application Preparation](#4-application-preparation)
5. [Python Virtual Environment](#5-python-virtual-environment)
6. [Gunicorn Installation](#6-gunicorn-installation)
7. [Gunicorn Configuration](#7-gunicorn-configuration)
8. [Create systemd Service](#8-create-systemd-service)
9. [Start and Manage Gunicorn](#9-start-and-manage-gunicorn)
10. [Validation](#10-validation)
11. [Use Cases](#11-use-cases)
12. [Troubleshooting](#12-troubleshooting)
13. [Best Practices](#13-best-practices)
14. [Conclusion](#14-conclusion)
15. [Contact Information](#15-contact-information)
16. [References](#16-references)

---

# 1. Introduction

This SOP provides a structured guide for installing, configuring, running, and managing **Gunicorn** for Python web applications on **Ubuntu/Linux servers**.

Gunicorn is a production-grade Python WSGI HTTP server commonly used to run Python web applications such as Flask and Django.

The SOP covers application preparation, Python virtual-environment setup, Gunicorn installation, configuration, systemd integration, service management, validation, and troubleshooting.

---

# 2. Purpose

The purpose of this SOP is to provide a standardized procedure for:

- Installing Python and required system packages.
- Preparing a Python application for Gunicorn.
- Creating and activating a Python virtual environment.
- Installing Gunicorn.
- Testing the application with Gunicorn.
- Configuring Gunicorn workers and binding.
- Creating a systemd service for automatic startup.
- Managing and monitoring the Gunicorn service.
- Validating the deployment.
- Troubleshooting common Gunicorn issues.

These procedures help maintain **reliability, performance, maintainability, and operational consistency**.

---

# 3. Prerequisites

| **Prerequisite** | **Details** |
| ---------------- | ----------- |
| OS & Access | Ubuntu/Linux server with SSH/terminal access |
| Python | Python 3.x installed |
| Application | Existing Flask/Django WSGI application |
| Permissions | `sudo/root` access |
| Required Packages | `python3`, `python3-pip`, `python3-venv` |
| Application User | Dedicated Linux user recommended |
| Network | Application port or Unix socket must be accessible as required |

Example application structure:

```text
/mnt/data/gunicorn-demo
├── app.py
├── requirements.txt
├── venv/
└── ...
```

> **NOTE**
> 
> The examples in this SOP use a Flask application with `app.py` containing a WSGI object named `app`. For Django or applications using a different module/object name, adjust the Gunicorn entry point accordingly.

---

# 4. Application Preparation

## Step 1: Update Package Repository

```bash
sudo apt update
```

Upgrade installed packages if required by the server-maintenance procedure:

```bash
sudo apt upgrade -y
```

---

## Step 2: Install Python and Required Packages

```bash
sudo apt install -y python3 python3-pip python3-venv
```

<img width="1771" height="949" alt="screen1" src="https://github.com/user-attachments/assets/435c1f41-348f-4fff-a107-d235a2c7b073" />


Verify Python:

```bash
python3 --version
```

Verify pip:

```bash
python3 -m pip --version
```

<img width="1771" height="94" alt="screen2" src="https://github.com/user-attachments/assets/f4000ab8-9374-480b-aa4d-1146e8c827db" />


---

## Step 3: Create Application Directory

Create the application directory if it does not already exist:

```bash
sudo mkdir -p /mnt/data/gunicorn-demo
```

Assign ownership to the application user:

```bash
sudo chown -R $USER:$USER /mnt/data/gunicorn-demo
```

---

# 5. Python Virtual Environment

## Step 1: Create Virtual Environment

From the application directory:

```bash
/mnt/data/gunicorn-demo
python3 -m venv venv
```

Verify:

```bash
ls -la venv
```

<img width="1771" height="309" alt="screen3" src="https://github.com/user-attachments/assets/6d2ccf01-443b-4f1f-80e6-43ab832719bb" />

---

## Step 2: Activate Virtual Environment

```bash
source venv/bin/activate
```

The shell should now show the virtual environment, for example:

```text
(venv) user@server:/mnt/data/gunicorn-demo$
```

<img width="1771" height="48" alt="screen4" src="https://github.com/user-attachments/assets/4e231e03-acd1-4855-a8e6-67b1120b55d1" />

---

## Step 3: Upgrade pip

```bash
python -m pip install --upgrade pip
```

<img width="1771" height="280" alt="screen5" src="https://github.com/user-attachments/assets/4513fa1a-7faf-426d-b4c6-852aa50dbcb2" />

---

## Step 4: Install Application Dependencies

If `requirements.txt` exists:

```bash
pip install -r requirements.txt
```

Verify installed packages:

```bash
pip list
```

<img width="1771" height="759" alt="screen6" src="https://github.com/user-attachments/assets/6bd9ea15-74d6-45eb-aa70-ce37e245b4b8" />

---

# 6. Gunicorn Installation

## Step 1: Install Gunicorn

With the virtual environment activated:

```bash
pip install gunicorn
```

Verify:

```bash
gunicorn --version
```

Expected:

```text
gunicorn (version)
```

<img width="1771" height="443" alt="screen7" src="https://github.com/user-attachments/assets/0efd6754-150b-4210-a678-a809e6f49cdb" />

---

## Step 2: Verify Gunicorn Location

```bash
which gunicorn
```

Expected:

```text
/mnt/data/gunicorn-demo/venv/bin/gunicorn
```

<img width="1771" height="64" alt="screen8" src="https://github.com/user-attachments/assets/2564b39a-e810-4f85-8e62-1210caa19fe6" />


> **NOTE**
> 
> Always use the Gunicorn executable from the application's virtual environment when configuring the systemd service.

---

## Step 3: Identify the WSGI Application

For Flask:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello World"
```

The Gunicorn application target is:

```text
app:app
```

The format is:

```text
<python_module>:<application_object>
```

For example:

```text
app:app
```

If the Python file is `main.py` and the WSGI object is `application`:

```text
main:application
```

---

# 7. Gunicorn Configuration

## Step 1: Test Gunicorn Manually

From the application directory:

```bash
cd /mnt/data/gunicorn-demo
source venv/bin/activate
```

Run:

```bash
gunicorn --bind 0.0.0.0:8001 app:app
```

Expected output:

```text
[INFO] Starting gunicorn
[INFO] Listening at: http://0.0.0.0:8001
[INFO] Using worker: sync
```

<img width="1771" height="133" alt="screen9" src="https://github.com/user-attachments/assets/8c16451a-d796-449f-961a-e7ad8e770b40" />

---

## Step 2: Test the on Browser

From the server:

```bash
http://127.0.0.1:8001/
```

Expected:

<img width="379" height="133" alt="screen10" src="https://github.com/user-attachments/assets/2e1ec44f-04de-4c76-81f6-0d5f560ccc57" />

Stop Gunicorn with:

```text
Ctrl+C
```

---

## Step 3: Configure Gunicorn Workers

A basic configuration can use:

```bash
gunicorn --workers 3 --bind 127.0.0.1:8001 app:app
```

Parameters:

| Parameter | Description |
| --------- | ----------- |
| `--workers 3` | Starts three Gunicorn worker processes |
| `--bind 127.0.0.1:8001` | Binds Gunicorn to local port 8001 |
| `app:app` | Python module and WSGI application |

<img width="1061" height="188" alt="screen11" src="https://github.com/user-attachments/assets/149bf8cb-71dd-4b73-ae71-b203bcbb291f" />

> **NOTE**
> 
> Worker count should be selected based on CPU, memory, application behavior, request characteristics, and workload. Do not blindly use a fixed worker formula for every application.

---

## Step 4: Create Gunicorn Configuration File

Create:

```bash
nano /mnt/data/gunicorn-demo/gunicorn.conf.py
```

Example:

```python
bind = "127.0.0.1:8001"

workers = 3

worker_class = "sync"

timeout = 120

accesslog = "-"
errorlog = "-"

capture_output = True
```

Save the file.

<img width="1061" height="290" alt="screen12" src="https://github.com/user-attachments/assets/6bc1c5dd-7d11-48e6-8edb-b1b4ffa3078a" />

---

## Step 5: Test Configuration File

Run:

```bash
cd /mnt/data/gunicorn-demo
source venv/bin/activate

gunicorn -c gunicorn.conf.py app:app
```
<img width="1061" height="195" alt="screen13" src="https://github.com/user-attachments/assets/aee0030d-4225-4621-a2b5-458bc6fab547" />


Verify:

```bash
http://127.0.0.1:8001/
```
<img width="379" height="133" alt="screen10" src="https://github.com/user-attachments/assets/3af2ae8f-1b69-4a5f-bf0e-e159bf6c5bd9" />

Stop the process after validation:

```text
Ctrl+C
```

---

# 8. Create systemd Service

## Step 1: Create Service File

Create:

```bash
sudo nano /etc/systemd/system/myapp.service
```

Add:

```ini
[Unit]
Description=Gunicorn service for MyApp
After=network.target

[Service]
User=<APP_USER>
Group=<APP_USER>
WorkingDirectory=/mnt/data/gunicorn-demo
Environment="PATH=/mnt/data/gunicorn-demo/venv/bin"
ExecStart=/mnt/data/gunicorn-demo/venv/bin/gunicorn \
    --config /mnt/data/gunicorn-demo/gunicorn.conf.py \
    app:app

Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

<img width="1061" height="364" alt="screen14" src="https://github.com/user-attachments/assets/19abf6dd-52d4-4a16-a3d5-95b406a625c8" />


with the Linux user that owns/runs the application.

---

## Step 2: Reload systemd

```bash
sudo systemctl daemon-reload
```

---

## Step 3: Enable Gunicorn at Boot

```bash
sudo systemctl enable myapp
```

Expected:

```text
Created symlink ...
```

<img width="1061" height="101" alt="screen15" src="https://github.com/user-attachments/assets/12ebfb77-3f6d-4f3a-b97d-be0f082aaeb0" />


---

## Step 4: Start Gunicorn

```bash
sudo systemctl start myapp
```

<img width="1061" height="491" alt="screen16" src="https://github.com/user-attachments/assets/8f9fa58a-b063-4669-b3f0-50fc48f9bc49" />

---

## Step 5: Check Service Status

```bash
sudo systemctl status myapp
```

Expected:

```text
Active: active (running)
```

<img width="1061" height="491" alt="screen16" src="https://github.com/user-attachments/assets/f2fd3cff-e617-4e30-b00a-d77b1c8808bb" />

---

# 9. Start and Manage Gunicorn

## Start

```bash
sudo systemctl start myapp
```

## Stop

```bash
sudo systemctl stop myapp
```

## Restart

```bash
sudo systemctl restart myapp
```

## Reload systemd Configuration

```bash
sudo systemctl daemon-reload
```

## Enable at Boot

```bash
sudo systemctl enable myapp
```

## Disable at Boot

```bash
sudo systemctl disable myapp
```

## Check Status

```bash
sudo systemctl status myapp
```

---

## Step 1: View Gunicorn Logs

```bash
sudo journalctl -u myapp
```

Follow logs in real time:

```bash
sudo journalctl -u myapp -f
```

Show logs from the current boot:

```bash
sudo journalctl -u myapp -b
```

Show the last 100 lines:

```bash
sudo journalctl -u myapp -n 100
```

<img width="1586" height="778" alt="screen17" src="https://github.com/user-attachments/assets/5ef20668-6b0f-4ddc-880e-331b0765e7a1" />

---

## Step 2: Check Listening Port

```bash
sudo ss -lntp | grep 8001
```

Expected:

```text
LISTEN ... 127.0.0.1:8001 ... gunicorn
```

<img width="1586" height="71" alt="screen18" src="https://github.com/user-attachments/assets/35e83851-ca07-4d3f-9641-a03d7523b7da" />

---

## Step 3: Test the Application

```bash
curl -I http://127.0.0.1:8001/
```

Expected:

```text
HTTP/1.1 200 OK
```

<img width="908" height="149" alt="screen19" src="https://github.com/user-attachments/assets/35b0202a-23c1-401d-b662-c978388d6e06" />

---

# 10. Validation

### Validate Python

```bash
python3 --version
```

Expected:

```text
Python 3.x.x
```

<img width="908" height="81" alt="screen20" src="https://github.com/user-attachments/assets/d9943a8e-6530-4b09-bfe2-b7da7cd76427" />


### Validate Virtual Environment

```bash
ls -l /mnt/data/gunicorn-demo/venv/bin/python
```

Expected:

```text
/mnt/data/gunicorn-demo/venv/bin/python
```

<img width="1003" height="81" alt="screen21" src="https://github.com/user-attachments/assets/3a26609c-0ebb-4cac-bc87-24b305bb022d" />


### Validate Gunicorn

```bash
/mnt/data/gunicorn-demo/venv/bin/gunicorn --version
```

Expected:

```text
gunicorn (version)
```

<img width="1064" height="114" alt="screen22" src="https://github.com/user-attachments/assets/823cdaab-6993-41e6-8db3-23250aca9133" />


### Validate Service

```bash
sudo systemctl is-active myapp
```

Expected:

```text
active
```

<img width="1064" height="84" alt="screen23" src="https://github.com/user-attachments/assets/d1097827-c0ed-44c4-bce5-55822c9d4cc8" />


### Validate Port

```bash
sudo ss -lntp | grep 8001
```

Expected:

Gunicorn is listening on the configured address and port.

<img width="1586" height="71" alt="screen18" src="https://github.com/user-attachments/assets/8bfbe4b7-3267-4e6a-b78f-e0da61988df7" />

### Validate Application

```bash
curl http://127.0.0.1:8001/
```

Expected:

The application's expected HTTP response.

<img width="1064" height="84" alt="screen24" src="https://github.com/user-attachments/assets/3638c7ed-45b4-4740-bf9d-d98c78ab1849" />
<img width="379" height="133" alt="screen10" src="https://github.com/user-attachments/assets/e2206057-d8e1-4348-b090-e0bc40389eb1" />

### Final Validation Checklist

| **Validation** | **Expected Result** |
| -------------- | ------------------- |
| Python installed | Python version is available |
| Virtual environment | `venv` exists and is usable |
| Dependencies | Application dependencies installed |
| Gunicorn | Gunicorn executable works |
| WSGI target | Correct module/object configured |
| Gunicorn service | Service is `active (running)` |
| Port | Gunicorn is listening on configured address/port |
| Application | HTTP request returns expected response |
| Logs | No startup or application errors |
| Boot persistence | Service starts after reboot |

---

# 11. Use Cases

| **Scenario** | **Commands / Actions** |
| ------------ | ---------------------- |
| Install Gunicorn | `pip install gunicorn` |
| Test Python application | `gunicorn --bind 127.0.0.1:8001 app:app` |
| Run multiple workers | Configure `workers` |
| Run application as service | Create `/etc/systemd/system/myapp.service` |
| Start application | `sudo systemctl start myapp` |
| Restart application | `sudo systemctl restart myapp` |
| Check application logs | `sudo journalctl -u myapp -f` |
| Verify listening port | `sudo ss -lntp \| grep 8001` |
| Test HTTP response | `curl http://127.0.0.1:8001/` |

---

# 12. Troubleshooting

| **Issue** | **Cause** | **Solution** |
| --------- | --------- | ------------ |
| `gunicorn: command not found` | Virtual environment is not active or Gunicorn is not installed | Activate `venv` and run `pip install gunicorn` |
| `ModuleNotFoundError` | Dependency is missing | Run `pip install -r requirements.txt` |
| `Failed to find attribute 'app'` | Incorrect WSGI target | Verify `<module>:<object>` |
| Service fails to start | Incorrect systemd configuration | Check `systemctl status` and `journalctl` |
| Port already in use | Another process is using the configured port | Run `sudo ss -lntp \| grep 8001` and change/stop the conflicting process |
| HTTP request fails | Application or Gunicorn is not running | Check service status and logs |
| Permission denied | Incorrect ownership/permissions | Verify application directory and service user |
| Service works manually but not with systemd | Environment differs between shell and systemd | Use absolute paths and configure required environment variables in systemd |
| Changes are not reflected | Old Gunicorn processes are running | Restart the systemd service |
| Workers repeatedly restart | Application errors, timeout, memory pressure, or worker configuration | Review Gunicorn logs and system resources |

---

# 13. Best Practices

| **Best Practice** | **Description** |
| ----------------- | --------------- |
| Use a virtual environment | Keep application dependencies isolated from system Python |
| Use a dedicated Linux user | Avoid running production applications as `root` |
| Use systemd | Provides automatic startup, restart, and service management |
| Use absolute paths | Prevent environment and PATH-related service failures |
| Keep Gunicorn behind a reverse proxy | Use Nginx or another appropriate reverse proxy for production deployments |
| Monitor workers | Review worker failures, response times, memory, and CPU utilization |
| Configure timeouts carefully | Avoid unnecessarily low or excessively high request timeouts |
| Configure logging | Send access/error logs to an appropriate centralized logging mechanism |
| Store secrets securely | Do not hard-code passwords, API keys, or tokens in application source code |
| Test after deployment | Validate service status, port, logs, and application response |
| Document worker configuration | Record why the selected worker count and timeout values were chosen |

---

# 14. Conclusion

This SOP provides a standardized approach to installing and operating **Gunicorn for Python web applications** on Ubuntu/Linux.

Following these procedures provides a consistent method for application preparation, dependency management, Gunicorn configuration, systemd integration, service management, validation, and troubleshooting.

---

# 15. Contact Information

| **Name** | **Email** |
| -------- | --------- |
| Maqbool Alam | maqbul.alam.snaatak@mygurukulam.co |

---

# 16. References

| **Topic** | **Description** | **Link** |
| --------- | --------------- | -------- |
| Gunicorn | Production WSGI HTTP server for Python applications | https://docs.gunicorn.org/en/stable/ |
| Gunicorn Configuration | Gunicorn settings reference (workers, bind, timeout, logging, etc.) | https://docs.gunicorn.org/en/stable/settings.html |
| Gunicorn Deployment | Recommended production deployment practices | https://docs.gunicorn.org/en/stable/deploy.html |
| Python | Python runtime and virtual-environment documentation | https://docs.python.org/3/ |
| Python `venv` | Creation of virtual environments | https://docs.python.org/3/library/venv.html |
| Flask | Flask WSGI web framework documentation | https://flask.palletsprojects.com/ |
| systemd | Linux service and process management | https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html |
| systemd `journalctl` | Querying and viewing systemd service logs | https://man7.org/linux/man-pages/man1/journalctl.1.html |
| Ubuntu | Ubuntu server administration documentation | https://ubuntu.com/server/docs |
