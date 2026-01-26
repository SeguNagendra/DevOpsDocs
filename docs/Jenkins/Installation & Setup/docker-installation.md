---
sidebar_position: 3
---

# Jenkins Docker Installation

This guide explains how to run **Jenkins using Docker**, which is the **recommended approach** for modern CI/CD setups.

---

## Why Run Jenkins in Docker?

Docker-based Jenkins provides:

- Consistent environments
- Easy upgrades and rollbacks
- Isolation from host system
- Simple backup and restore

> Most production Jenkins setups today use Docker or Kubernetes.

---

## Prerequisites

Before starting:
- Docker installed
- Docker service running
- At least 4 GB RAM available

Verify Docker:
```bash
docker version
```

---

## Jenkins Docker Image

- Official image: `jenkins/jenkins:lts`
- Includes Jenkins LTS + recommended tools
- Runs Jenkins as a non-root user

---

## Basic Jenkins Docker Run

```bash
docker run -d   --name jenkins   -p 8080:8080   -p 50000:50000   -v jenkins_home:/var/jenkins_home   jenkins/jenkins:lts
```

### What This Does
- Exposes Jenkins UI on port 8080
- Enables agent communication on port 50000
- Persists Jenkins data using a Docker volume

---

## Access Jenkins UI

Open browser:
```
http://localhost:8080
```

---

## Retrieve Initial Admin Password

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

## Using Host Directory Instead of Volume

```bash
docker run -d   --name jenkins   -p 8080:8080   -p 50000:50000   -v /opt/jenkins:/var/jenkins_home   jenkins/jenkins:lts
```

---

## Installing Docker Inside Jenkins (Optional)

For Docker-based builds:

```bash
docker exec -it jenkins bash
apt update && apt install -y docker.io
```

> In production, prefer **Docker-outside-of-Docker** or dedicated Docker agents.

---

## Common Docker Issues

- Permission denied → volume ownership mismatch
- Jenkins not starting → insufficient memory
- Agent connection issues → blocked port 50000

---

## Production Best Practices

- Always use Jenkins LTS image
- Persist `jenkins_home`
- Limit container resources
- Do not run builds on controller container
- Use external agents for execution
