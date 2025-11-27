---
sidebar_position: 2
---

# Docker Installation   
## Linux & Windows (Docker Desktop)

This document provides **step-by-step Docker installation instructions** for:
- Linux (Ubuntu, RHEL/CentOS, Amazon Linux)
- Windows using Docker Desktop (WSL 2)

---

## 1. Docker Installation on Linux

### 1.1 Prerequisites
- 64-bit OS
- Kernel 3.10+
- sudo/root access

Verify OS:
```bash
cat /etc/os-release
```

---

## 1.2 Install Docker on Ubuntu (20.04 / 22.04 / 24.04)

### Remove old versions
```bash
sudo apt remove -y docker docker-engine docker.io containerd runc
```

### Update system
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
```

### Add Docker GPG key
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### Add Docker repository
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Start & enable Docker
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### Run Docker without sudo
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Verify installation
```bash
docker version
docker run hello-world
```

---

## 1.3 Install Docker on RHEL / CentOS / Rocky Linux

```bash
sudo yum remove -y docker docker-client docker-engine docker.io
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 1.4 Install Docker on Amazon Linux 2

```bash
sudo yum update -y
sudo amazon-linux-extras install docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
```

Re-login required.

---

## 2. Docker Installation on Windows (Docker Desktop)

### 2.1 System Requirements
- Windows 10/11 64-bit
- Virtualization enabled
- WSL 2

---

### 2.2 Enable WSL 2
Open PowerShell as Administrator:
```powershell
wsl --install
wsl --set-default-version 2
```

Restart system if prompted.

---

### 2.3 Download Docker Desktop
Download from:
```text
https://www.docker.com/products/docker-desktop/
```

---

### 2.4 Install Docker Desktop
- Run installer
- Select **Use WSL 2**
- Complete installation

---

### 2.5 Verify Docker on Windows
```powershell
docker version
docker run hello-world
```

---

## 3. Docker Compose Check

```bash
docker compose version
```

---

## 4. Common Issues

### Permission denied
```bash
sudo usermod -aG docker $USER
```

### Docker not running
```bash
sudo systemctl start docker
```

### Check WSL version
```powershell
wsl -l -v
```

---

## 5. Summary

✅ Linux runs Docker natively  
✅ Windows uses Docker Desktop with WSL 2  
✅ Verify using `docker run hello-world`  


# Configure Docker Desktop on Windows Without WSL

This guide explains how to install and configure **Docker Desktop on Windows without WSL (Windows Subsystem for Linux)** using **Hyper-V**.

---

## 1. Why Configure Docker Without WSL?

Organizations may avoid WSL due to:
- Corporate security policies
- Restricted admin permissions
- Need for Windows containers
- Preference for Hyper-V isolation
- Avoiding WSL kernel dependencies

✅ Docker Desktop fully supports **Hyper-V–based Docker**.

---

## 2. Supported Windows Versions

Docker Desktop without WSL requires **Hyper-V**.

| Windows Version | Supported |
|----------------|----------|
| Windows 10 Pro / Enterprise | ✅ |
| Windows 11 Pro / Enterprise | ✅ |
| Windows Home | ❌ (WSL required) |

---

## 3. System Requirements

- 64-bit OS
- Virtualization enabled in BIOS
- Minimum 4 GB RAM (8 GB recommended)
- Administrator access

---

## 4. Enable Hyper-V & Containers

Open **PowerShell as Administrator**:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Hyper-V-All /all /norestart
dism.exe /online /enable-feature /featurename:Containers /all /norestart
```

Restart the system.

---

## 5. Verify Hyper-V

```powershell
systeminfo | findstr /i "Hyper-V"
```

Expected:
```text
Hyper-V Requirements: A hypervisor has been detected.
```

---

## 6. Install Docker Desktop

1. Download Docker Desktop for Windows  
2. Run installer  
3. ❌ Uncheck **Use WSL 2 instead of Hyper-V**  
4. Complete installation  
5. Restart the system  

---

## 7. Disable WSL Engine

- Open Docker Desktop
- Go to **Settings → General**
- Disable **Use the WSL 2 based engine**
- Restart Docker Desktop

---

## 8. Switch Container Mode

### Switch to Windows Containers
- Right-click Docker tray icon
- Select **Switch to Windows containers**

### Verify
```powershell
docker info
```

Look for:
```text
OSType: windows
```

---

## 9. Run Containers Without WSL

Test Linux container:
```powershell
docker run hello-world
```

Test Windows container:
```powershell
docker run mcr.microsoft.com/windows/nanoserver:ltsc2022 cmd
```

---

## 10. Docker Hyper-V Architecture

```text
Docker CLI
  |
Docker Desktop
  |
Hyper-V VM
  |
Docker Engine
  |
Containers
```

---

## 11. Configure Resources

Docker Desktop → **Settings → Resources**
- CPU cores
- Memory
- Disk size

---

## 12. Networking Without WSL

```powershell
docker run -d -p 8080:80 nginx
```
Access:
```text
http://localhost:8080
```

---

## 13. Volumes Without WSL

```powershell
docker volume create mydata
docker run -v mydata:/data busybox
```

---

## 14. Troubleshooting

### Docker Not Starting
- Enable virtualization in BIOS
- Ensure Hyper-V installed

### Port Conflicts
```powershell
netstat -ano | findstr :8080
```

---

## 15. WSL vs Hyper-V

| Feature | WSL 2 | Hyper-V |
|------|------|--------|
| Windows Home | ✅ | ❌ |
| Windows Containers | ❌ | ✅ |
| Enterprise Policy Friendly | ❌ | ✅ |
| Isolation | Medium | High |

---

## 16. When to Use Hyper-V

✅ Corporate laptops  
✅ Windows containers  
✅ Policy-restricted systems  

---

## 17. Commands Cheat Sheet

```powershell
docker info
docker ps
docker images
docker run hello-world
```

---

## 18. Summary

- Docker Desktop works **without WSL** using Hyper-V
- Requires Windows Pro/Enterprise
- Supports both Linux and Windows containers
- Ideal for enterprise environments

