---
sidebar_position: 2
---

# Jenkins Local Installation

This guide explains how to install Jenkins **locally on a machine or VM**.
Local installation is ideal for **learning, PoCs, and small team setups**.

---

## Supported Operating Systems

Jenkins can be installed on:
- Linux (recommended)
- macOS
- Windows

> Production environments usually prefer **Linux**.

---

## Prerequisites

Before installing Jenkins, ensure:

- Java LTS installed (Java 11 or 17 recommended)
- Minimum 2 GB RAM (4 GB recommended)
- At least 10 GB free disk space
- Internet access (for plugins)

Verify Java:
```bash
java -version
```

---

## Jenkins Installation on Linux

### Step 1: Add Jenkins Repository
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

### Step 2: Install Jenkins
```bash
sudo apt update
sudo apt install jenkins
```

---

### Step 3: Start & Enable Jenkins
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Check status:
```bash
sudo systemctl status jenkins
```

---

## Jenkins Installation on macOS

### Using Homebrew
```bash
brew install jenkins-lts
```

Start Jenkins:
```bash
brew services start jenkins-lts
```

---

## Jenkins Installation on Windows

### Using Installer
- Download Jenkins LTS installer
- Install as Windows service
- Choose Java path during installation

---

## Access Jenkins UI

After installation, access Jenkins at:
```
http://localhost:8080
```

---

## Initial Unlock

Retrieve the admin password:

### Linux / macOS
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

### Windows
```text
C:\Program Files\Jenkins\secrets\initialAdminPassword
```

---

## Verify Installation

- Jenkins UI loads
- Setup wizard starts
- No errors in system logs

---

## Common Issues

- Jenkins not starting → Java version mismatch
- Port 8080 blocked → firewall issue
- Permission errors → wrong file ownership

---

## Production Notes

- Avoid local install for large teams
- Prefer Docker or dedicated VM
- Do not run builds on controller
