---
sidebar_position: 10
---

# Docker Registry

## 1. What is a Docker Registry?

A **Docker Registry** is a **central storage and distribution system** for Docker images.

In simple terms:
> A Docker registry stores Docker images so they can be **pulled**, **pushed**, and **shared** between systems.

Examples:
- Docker Hub (public registry)
- GitHub Container Registry
- Amazon ECR
- Google Artifact Registry
- Private on‑prem registries

---

## 2. Why Do We Need a Docker Registry?

Without a registry:
- Images stay only on local machines
- Cannot share images across teams
- CI/CD pipelines break
- No versioned image management

### Problems Solved by Registry

| Problem | Without Registry | With Registry |
|------|------------------|--------------|
| Image sharing | Manual copy | Automated ✅ |
| CI/CD builds | Not possible | Seamless ✅ |
| Version control | Difficult | Easy ✅ |
| Rollbacks | Hard | Simple ✅ |
| Distributed systems | Impossible | Works ✅ |

👉 **Registries are critical for DevOps, CI/CD, and Kubernetes**.

---

## 3. Docker Registry Architecture

High‑level components:
```text
Developer → Docker Client → Registry → Storage Backend
```

Registry stores:
- Image layers
- Image manifests
- Tags and metadata

Storage backend can be:
- Local filesystem
- Cloud storage (S3, GCS, Azure Blob)

---

## 4. Types of Docker Registries

### 4.1 Public Registry

Anyone can pull images.

Example:
- Docker Hub (public repos)

Pros:
- Easy image sharing
- Huge ecosystem

Cons:
- Rate limits
- Security concerns

---

### 4.2 Private Registry

Restricted access.

Pros:
- Secure
- Full control
- Used in enterprises

Cons:
- Setup & maintenance needed

---

### 4.3 Cloud‑Managed Registries

Provided by cloud vendors.

Examples:
- AWS ECR
- GCP Artifact Registry
- Azure Container Registry

Pros:
- Highly available
- Secure
- Integrated with cloud IAM

---

## 5. Docker Image Naming & Registry Format

```text
[registry-domain]/[namespace]/[repository]:[tag]
```

Examples:
```text
nginx:1.27
docker.io/library/nginx:1.27
ghcr.io/myorg/myapp:1.0
123456789012.dkr.ecr.us-east-1.amazonaws.com/app:prod
```

---

## 6. Docker Hub – Default Registry

Docker Hub is the **default public registry**.

If registry is not specified:
```bash
docker pull nginx
```

Docker pulls from:
```text
docker.io/library/nginx
```

---

## 7. Registry Authentication

### 7.1 Login to Registry

```bash
docker login
```

Custom registry:
```bash
docker login registry.example.com
```

Credentials stored at:
```text
~/.docker/config.json
```

---

## 8. Pushing Images to Registry

### Step 1: Build Image
```bash
docker build -t myapp:1.0 .
```

### Step 2: Tag Image
```bash
docker tag myapp:1.0 mydockerhubuser/myapp:1.0
```

### Step 3: Push Image
```bash
docker push mydockerhubuser/myapp:1.0
```

---

## 9. Pulling Images from Registry

```bash
docker pull mydockerhubuser/myapp:1.0
```

Docker checks:
1. Local cache
2. Registry if not found

---

## 10. Image Tags & Versioning

Tags:
- Are mutable labels
- Point to image digests
- Do NOT guarantee immutability

Example:
```bash
docker tag myapp:1.0 myapp:latest
```

Best practices:
- Use semantic versioning (1.0.0, 1.1.0)
- Avoid `latest` in production

---

## 11. Image Digests (Immutable)

Digests uniquely identify images.

Example:
```bash
docker pull nginx@sha256:abc123...
```

Digests:
- Never change
- Ideal for production deployments

---

## 12. Private Docker Registry Setup

Run a local registry container:

```bash
docker run -d   -p 5000:5000   --name registry   registry:2
```

Push image:
```bash
docker tag myapp localhost:5000/myapp:1.0
docker push localhost:5000/myapp:1.0
```

---

## 13. Registry with Persistent Storage

```bash
docker run -d   -p 5000:5000   -v registry_data:/var/lib/registry   --name registry   registry:2
```

Without volume → images lost if container removed.

---

## 14. Registry Security

### 14.1 Authentication

- Username & password
- Token‑based auth
- IAM (cloud registries)

### 14.2 TLS (HTTPS)

Registries should always run over HTTPS.

```text
https://registry.example.com
```

Avoid:
```text
http://registry.example.com
```

---

## 15. Registry Garbage Collection

Over time:
- Old image layers accumulate

Cleanup via:
```bash
registry garbage-collect
```

Used in:
- Self‑hosted registries

---

## 16. Docker Registry with Docker Compose

```yaml
version: "3.9"

services:
  registry:
    image: registry:2
    ports:
      - "5000:5000"
    volumes:
      - registry_data:/var/lib/registry

volumes:
  registry_data:
```

Start:
```bash
docker compose up -d
```

---

## 17. Registry in CI/CD Pipelines

Common CI/CD flow:
```text
Code → Build Image → Tag → Push → Deploy
```

Example:
```bash
docker build -t app:${GIT_COMMIT} .
docker push app:${GIT_COMMIT}
```

Registries act as:
✅ Artifact storage  
✅ Deployment source  

---

## 18. Registry Best Practices

- Use private registries for production
- Enable authentication and TLS
- Use immutable tags or digests
- Regularly clean old images
- Scan images for vulnerabilities
- Limit push/pull permissions

---

## 19. Common Mistakes

1. Using `latest` tag in production
2. Storing secrets inside images
3. No authentication on private registry
4. No backups
5. No cleanup policy

---

## 20. Docker Registry vs Image vs Container

| Concept | Purpose |
|------|--------|
| Image | Application blueprint |
| Registry | Image storage & distribution |
| Container | Running instance of image |

---

## 21. Docker Registry Cheat Sheet

```bash
docker login
docker logout
docker tag image repo/image:tag
docker push repo/image:tag
docker pull repo/image:tag
```

---

## 22. Summary

- Docker Registry stores and distributes images
- Essential for CI/CD and production systems
- Supports public, private, and cloud‑managed options
- Tags are mutable; digests are immutable
- Security, backups, and cleanup are critical


