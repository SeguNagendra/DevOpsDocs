---
sidebar_position: 1
---

# Docker Introduction

## 1. What Docker Does

Docker solves the classic developer problem:

> **“It works on my machine, but not on the server!”** 😅

With Docker, you package your application with all its dependencies into a **container** → move it anywhere → and it runs the same way everywhere, whether on your laptop, a testing server, or in the cloud.

---

## 2. Key Concepts in Docker

| Component | Description | Example |
|---------|------------|---------|
| Image | A read-only template that contains your app + environment | `nginx:latest` |
| Container | A running instance of an image | Running Nginx server |
| Dockerfile | A script with instructions to build an image | `FROM ubuntu:20.04` |
| Docker Engine | The core service that runs containers | Installed with Docker |
| Docker Hub | A public registry to store and share images | hub.docker.com |

---

## 3. How Docker Works

Think of Docker as a **shipping container system for software**:

- Traditionally, apps run on different environments → dependency issues arise  
- Docker isolates your app in a container → it always works the same  
- Containers share the OS kernel, making them **faster and lighter than virtual machines**  

### Example Workflow

```bash
# Pull an image from Docker Hub
docker pull nginx

# Run a container from that image
docker run -d -p 8080:80 nginx

# Check running containers
docker ps
```

✅ This starts an **Nginx web server** on port **8080** in just seconds.

---

## 4. Docker vs Virtual Machines

| Feature | Docker (Containers) | Virtual Machines |
|------|-----------------|----------------|
| Startup Time | Seconds | Minutes |
| Resource Usage | Lightweight | Heavy |
| Isolation | Process-level | Full OS-level |
| Portability | High | Medium |
| Size | MBs | GBs |

---

## 5. Why Docker is Popular

- 🚀 **Speed** – Start applications in seconds  
- 🛠️ **Consistency** – Runs the same everywhere  
- 🧩 **Isolation** – No conflicts between applications  
- 🌍 **Portability** – Works on any machine  
- 📦 **Scalability** – Ideal for microservices and cloud deployments  

---

## 6. Real-Life Example

Imagine you’re developing a **Java web application**:

### Without Docker
- Install Java
- Configure Tomcat
- Set up MySQL
- Handle dependencies manually

### With Docker
```bash
docker run -d -p 8080:8080 tomcat
docker run -d -p 3306:3306 mysql
```

✅ Tomcat and MySQL are ready in seconds — **no setup headaches**.

---

## 7. Simple Diagram

```
+-------------------------------------+
| Your Application                    |
| (Code + Libraries + Config)         |
+-------------------------------------+
| Docker Container                    |
+-------------------------------------+
| Docker Engine / Daemon              |
+-------------------------------------+
| Host OS & Hardware                  |
+-------------------------------------+
```

---

## Summary

- **Docker** = Platform to build, run, and ship apps in containers  
- **Containers** = Lightweight, isolated environments  
- Docker ensures **consistency, speed, portability, and scalability**  
- Ideal for **developers, testers, DevOps engineers, and cloud deployments**
