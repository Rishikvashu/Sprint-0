# Gunicorn Intro Documentation
 
<p align="center">
  <img src="https://static.myflashinfo.com/image/4/c/0/4c065b16bed53a5b831ec1cad958afed.png" alt="Logrotate Logo" width="700"/>
</p>

---

## Author Information
| **Author** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Mansoor Alam | 26-08-2026 | 1.0 | Mansoor Alam | 26-08-2026 | Rajnish Sharma | Pritam/Komal | Abhishek/Manish Nautiyal |



---

## Table of Contents

- [What is Gunicorn?](#what-is-gunicorn)
- [Why Use Gunicorn?](#why-use-gunicorn)
- [Architecture View](#architecture-view)
  - [How It Works](#how-it-works)
  - [Request Flow](#request-flow)
- [Key Features](#key-features)
- [Limitations of Gunicorn](#limitations-of-gunicorn)
- [Use Cases](#use-cases)
- [Conclusion](#conclusion)
- [Contacts](#contacts)
- [Reference Table](#reference-table)

---

## What is Gunicorn?

Gunicorn (Green Unicorn) is a production-ready WSGI (Web Server Gateway Interface) server used to run and serve Python web applications in production. It is commonly used with Python web frameworks such as Flask and Django. Gunicorn manages multiple worker processes to handle incoming requests and send responses from the application. It is often used behind a web server or reverse proxy such as Nginx.

---

## Why Use Gunicorn?
Gunicorn is used to run and serve Python web applications such as Flask and Django in a production environment. It provides a reliable way to handle incoming requests using multiple worker processes. Multiple workers allow the application to handle multiple requests concurrently. Gunicorn is also easy to integrate with web servers or reverse proxies such as Nginx, making it suitable for production deployments.

---

## Architecture View

<img width="444" height="359" alt="gunicorn" src="https://github.com/user-attachments/assets/7431dda2-521a-4dd1-9b07-e1204d3c9041" />




### How It Works:

- The **Python application** contains the application logic and handles the actual business operations.
- **Gunicorn** runs and serves the Python application and uses worker processes to handle incoming requests.
- **Nginx** commonly acts as a reverse proxy in front of Gunicorn. It receives client requests and forwards them to Gunicorn.
- Gunicorn passes the request to the Python application, and the response is sent back to the client through Nginx.

### Request Flow:

Client → Nginx → Gunicorn → Worker → Python Application → Response

---

## Key Features

| **Feature** | **Description** |
|---|---|
| **Pre-Fork Worker Model** | Gunicorn uses multiple worker processes to handle incoming requests concurrently. |
| **WSGI Support** | Gunicorn can serve WSGI-compatible Python web applications such as Flask and Django. |
| **Simple CLI** | Gunicorn can be started and configured easily using command-line options such as `gunicorn app:app`. |
| **Flexible Worker Types** | Gunicorn provides different worker types such as sync, threaded, and asynchronous workers for different workloads. |
| **Graceful Worker Management** | Gunicorn can gracefully restart or reload workers so that running requests are handled properly. |
| **Logging** | Gunicorn provides access and error logs that help with monitoring and troubleshooting. |

---

## Limitations of Gunicorn

| **Limitation** | **Description** |
|---|---|
| **Not Native on Windows** | Gunicorn is designed for UNIX-based systems such as Linux and macOS. On Windows, it is commonly used through WSL or a Linux environment. |
| **Blocking with Sync Workers** | With the default synchronous worker model, a slow or blocking request can keep a worker busy until the request is completed. |
| **WSGI-Focused** | Gunicorn is primarily designed for WSGI-based Python applications. For applications that require advanced asynchronous features such as WebSockets, an ASGI server such as Uvicorn or Hypercorn is generally more suitable. |
| **No Multi-Server Load Balancing** | Gunicorn manages workers on a single server. Traffic distribution across multiple servers requires an external load balancer or reverse proxy such as Nginx, HAProxy, or a cloud load balancer. |
| **Requires Additional Components for Production Architecture** | Features such as reverse proxying, TLS termination, multi-server load balancing, and advanced deployment strategies are typically handled by additional components such as Nginx, a load balancer, systemd, containers, or Kubernetes. |

---

##  Use Cases

| **Use Case** | **Description** |
|---|---|
| **Web Application Deployment** | Gunicorn is used to run and serve Python web applications such as Flask and Django in production. |
| **Handling Web Traffic** | Gunicorn can use multiple workers to handle concurrent requests and improve application capacity on a server. |
| **API Server** | Gunicorn can serve Python-based APIs used by web applications, mobile applications, and other systems. |
| **Microservices** | Gunicorn can be used to serve Python-based microservices, with each service running as an independent application. |
| **Cloud-Based Hosting** | Gunicorn can be deployed on cloud platforms such as AWS, GCP, and Azure as part of a production application architecture. |
---



## Conclusion

Gunicorn is essential for production-grade Python applications, providing improved performance, scalability, and ease of use. By supporting various worker types and configurations, it ensures high availability and robust operation in demanding environments.

---

## Contacts

| Name | Email Address |
| --- | --- |
| Mansoor Alam|  mansoor.alam.snaatak@mygurukulam.com|

---

## Reference Table

|      Descriptions                                                                                |  Links         |
|--------------------------------------------------------------------------------------------|----------------------|
|  What is Gunicorn - Blog | https://medium.com/@serdarilarslan/what-is-gunicorn-5e674fff131b 
|         Gunicorn Docs       |  [https://docs.gunicorn.org/en/stable/](https://docs.gunicorn.org/en/stable/)       |
