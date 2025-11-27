---
sidebar_position: 4
---

# Docker Images

## 1. What Is a Docker Image?

A **Docker image** is a read-only template used to create containers.  
You can think of it as:

- A *blueprint* for containers
- A *snapshot* of a filesystem + metadata
- A *package* that includes:
  - OS filesystem (or a minimal runtime)
  - Application code
  - Libraries & dependencies
  - Configuration (environment variables, default command, etc.)

Containers are **running instances** of images.

---

## 2. Image vs Container

| Concept   | Docker Image                                   | Docker Container                             |
|----------|-------------------------------------------------|----------------------------------------------|
| Nature   | Read-only template                              | Running (or stopped) instance of an image    |
| State    | Immutable→ Images cannot be changed once created      | Mutable (writes go to a writable layer)      |
| Use      | Build-time & distribution                       | Runtime                                      |
| Storage  | Stored in image cache / registry                | Uses image + writable container layer        |
| Example  | `nginx:latest`                                  | `nginx` container created from that image    |

**Flow:**

1. Create / pull image  
2. Run container from image  
3. Container creates a writable layer on top of image layers  

---

## 3. Image Layers & Union Filesystem

Docker images are composed of **multiple layers** stacked on top of each other.  
Each layer is:

- A read-only filesystem change (add/modify/delete files)
- Identified by a content hash (like `sha256:...`)

### 3.1 How Layers Work

- Each `Dockerfile` instruction generally creates a **new layer**.
- Lower layers are shared between images (saves storage).
- When you run a container, Docker adds a **thin writable layer** on top.

Example:

```text
Image: myapp:1.0

Layer 4: app code (COPY . /app)
Layer 3: dependencies (RUN pip install -r requirements.txt)
Layer 2: runtime (RUN apt-get install python3)
Layer 1: base OS (FROM debian:12)
```

Multiple images built `FROM debian:12` share **Layer 1**.

### 3.2 Benefits of Layers

- **Storage efficiency** – shared layers between images
- **Faster builds** – cached layers reused
- **Faster pulls** – only missing layers are downloaded

---

## 4. Base Image, Parent Image, and `scratch`

### 4.1 Base / Parent Image

The `FROM` line in Dockerfile specifies the **parent image**:

```dockerfile
FROM ubuntu:24.04
```

Here:
- `ubuntu:24.04` is the base/parent image
- Your Dockerfile builds additional layers on top

Common base images:

- Full OS: `ubuntu`, `debian`, `centos`, `rockylinux`
- Minimal: `alpine`
- Language runtimes: `python`, `node`, `golang`, `openjdk`

### 4.2 `scratch` Image

`scratch` is an empty image – no shell, no package manager.

```dockerfile
FROM scratch
COPY my-binary /my-binary
ENTRYPOINT ["/my-binary"]
```

Used for:

- Minimal, tiny images
- Static binaries (e.g., Go apps)
- Security-hardening (small attack surface)

---

## 5. Understanding Docker Image Names & Tags

Images are identified as:

```text
[registry/][namespace/]repository[:tag]
```

Examples:

- `nginx:latest`
- `nginx:1.27-alpine`
- `mycompany/myapp:1.0.0`
- `registry.example.com/team/app:prod`

Parts:

- **Registry** (optional): `docker.io`, `ghcr.io`, `registry.example.com`
- **Namespace**: user or org (`library` for official images)
- **Repository**: project name (`nginx`, `ubuntu`, `myapp`)
- **Tag** (optional, default `latest`): version/variant

### 5.1 Tags

Tags are just **labels pointing to an image digest**:

```bash
docker pull nginx:1.27
docker pull nginx:1.27-alpine

# Tag same image with another name
docker tag myapp:1.0 myrepo/myapp:stable
```

Prefer **explicit version tags** over `latest` in production.

---

## 6. Dockerfile & Image Build Process

A **Dockerfile** defines how to build the image.

### 6.1 Simple Example

```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000
CMD ["python", "app.py"]
```

Build image:

```bash
docker build -t myapp:1.0 .
```

Run container:

```bash
docker run --name myapp-container -p 8000:8000 myapp:1.0
```

### 6.2 Build Context

When you run:

```bash
docker build -t myapp:1.0 .
```

The last `.` is the **build context**:

- Docker sends all files in that directory (respecting `.dockerignore`) to the Docker engine.
- `COPY` and `ADD` commands in the Dockerfile can only access files **inside the build context**.

Use `.dockerignore` to avoid sending unnecessary files (logs, `.git`, etc.).

Example `.dockerignore`:

```gitignore
.git
*.log
node_modules
__pycache__/
.env
```

---

## 7. Common Dockerfile Instructions Affecting Images

- `FROM` – base image
- `RUN` – execute command, result stored as new layer
- `COPY` / `ADD` – copy files into image
- `ENV` – set environment variables
- `EXPOSE` – document container port (for humans and some tools)
- `CMD` – default command to run
- `ENTRYPOINT` – main executable for container
- `WORKDIR` – set working directory

Example:

```dockerfile
FROM node:22-alpine

WORKDIR /app
COPY package*.json ./

RUN npm install --production

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

## 8. Multi-Stage Builds

**Multi-stage builds** help you create **small, production-ready images** by separating build and runtime stages.

Example for a Go application:

```dockerfile
# Stage 1 – Build
FROM golang:1.23-alpine AS builder

WORKDIR /src
COPY . .
RUN go build -o myapp

# Stage 2 – Runtime
FROM alpine:3.20

WORKDIR /app
COPY --from=builder /src/myapp .

EXPOSE 8080
ENTRYPOINT ["./myapp"]
```

Benefits:

- Build tools (`go`, `gcc`, etc.) don’t exist in final image
- Final image is smaller and more secure

---

## 9. Image Caching & Build Optimization

Docker uses layer caching to speed up builds.  

**Cache rule:** if a Dockerfile instruction and its context are unchanged, Docker reuses the cached layer.

Typical pattern:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# 1. Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 2. Copy the rest of the source code
COPY . .

CMD ["python", "app.py"]
```

If you change only `app.py`, layers for `requirements.txt` and `pip install` are reused.

**Bad pattern:**

```dockerfile
COPY . .
RUN pip install --no-cache-dir -r requirements.txt
```

Any change in the source will invalidate the cache and re-run `pip install`.

---

## 10. Inspecting Images

### 10.1 List Images

```bash
# List local images
docker images

# or
docker image ls
```

Example output:

```text
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
myapp        1.0       a1b2c3d4e5f6   2 minutes ago   210MB
nginx        1.27      123abc456def   3 weeks ago     142MB
```

### 10.2 Inspect Image Details

```bash
docker inspect myapp:1.0
```

Shows:

- Layers
- Environment variables
- Entrypoint / command
- Exposed ports
- Working directory

### 10.3 See History (Layers)

```bash
docker history myapp:1.0
```

Shows each layer and the Dockerfile instruction that created it.

---

## 11. Managing Images

### 11.1 Removing Images

```bash
# Remove a single image
docker rmi myapp:1.0

# Remove by image ID
docker rmi a1b2c3d4e5f6

# Force remove (containers using it will also be removed)
docker rmi -f myapp:1.0
```

### 11.2 Cleaning Up Unused Images

```bash
# Remove dangling images (no tag, not used)
docker image prune

# Remove all unused images (careful)
docker image prune -a
```

### 11.3 Removing Both Containers & Images

```bash
# Remove all stopped containers
docker container prune

# Remove all dangling or unused resources (containers, images, networks, build cache)
docker system prune

# More aggressive: removes unused images too
docker system prune -a
```

---

## 12. Saving, Loading, Importing & Exporting Images

### 12.1 Save / Load (Images)

```bash
# Save image to tar file
docker save -o myapp.tar myapp:1.0

# Load from tar file
docker load -i myapp.tar
```

Use when you want to:

- Move images between machines without registry
- Archive image versions

### 12.2 Export / Import (Containers)

```bash
# Export a container's filesystem
docker export -o mycontainer.tar mycontainer

# Import as image
docker import mycontainer.tar mynewimage:1.0
```

Difference:

- `save/load` → works with **images & layers**
- `export/import` → works with **container filesystem only** (no history, no metadata)

---

## 13. Working with Docker Registries

A **registry** stores images. Examples:

- Docker Hub (default): `docker.io`
- GitHub Container Registry: `ghcr.io`
- GitLab Container Registry
- Private registries: `registry.example.com`

### 13.1 Login

```bash
docker login
# or
docker login registry.example.com
```

### 13.2 Pulling Images

```bash
docker pull nginx:1.27
docker pull registry.example.com/team/app:prod
```

### 13.3 Pushing Your Own Images

```bash
# Tag image with registry and repo
docker tag myapp:1.0 myusername/myapp:1.0

# Push to Docker Hub
docker push myusername/myapp:1.0

# Push to custom registry
docker tag myapp:1.0 registry.example.com/team/myapp:1.0
docker push registry.example.com/team/myapp:1.0
```

---

## 14. Image Security & Best Practices

### 14.1 Use Minimal Base Images

Prefer:

- `alpine`, `debian:bookworm-slim`, `ubuntu:24.04` minimal
- Language-specific slim images: `python:3.11-slim`, `node:22-alpine`, etc.

Benefits:

- Smaller size
- Lower attack surface
- Faster pull

### 14.2 Don’t Run as Root (When Possible)

```dockerfile
FROM node:22-alpine

# Create user
RUN addgroup -S app && adduser -S app -G app

WORKDIR /app
COPY . .

RUN npm install --production

USER app

EXPOSE 3000
CMD ["npm", "start"]
```

### 14.3 Don’t Store Secrets in Images

Avoid:

- Hardcoding passwords/API keys in `Dockerfile`
- Copying `.env` into the image

Instead:

- Pass secrets via environment variables, secret managers, or runtime config

### 14.4 Keep Images Updated

- Rebuild images regularly with updated base images
- Use tools like `trivy` to scan for vulnerabilities

```bash
trivy image myapp:1.0
```

*(Tool usage depends on your environment.)*

---

## 15. Practical Hands-On Examples

### 15.1 Build and Run a Simple Python App Image

**Step 1: Project Structure**

```text
myapp/
├─ app.py
├─ requirements.txt
└─ Dockerfile
```

**`app.py`:**

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker image!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

**`requirements.txt`:**

```text
flask==3.0.0
```

**`Dockerfile`:**

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

**Build the image:**

```bash
cd myapp
docker build -t flask-hello:1.0 .
```

**Run the container:**

```bash
docker run --name flask-hello -p 5000:5000 flask-hello:1.0
```

Open `http://localhost:5000` to test.

### 15.2 Check Layers and History

```bash
docker history flask-hello:1.0
docker inspect flask-hello:1.0
```

### 15.3 Push to Docker Hub (Example)

```bash
# Login once
docker login

# Tag for Docker Hub
docker tag flask-hello:1.0 yourdockerhubusername/flask-hello:1.0

# Push
docker push yourdockerhubusername/flask-hello:1.0
```

---

## 16. Common Docker Image Commands Cheat Sheet

```bash
# Build image
docker build -t name:tag .

# List images
docker images
docker image ls

# Tag image
docker tag source-image:tag target-repo:tag

# Remove image
docker rmi image:tag
docker rmi image_id

# Pull / push
docker pull repo/image:tag
docker push repo/image:tag

# Save / load
docker save -o image.tar image:tag
docker load -i image.tar

# Prune images
docker image prune        # remove dangling images
docker image prune -a     # remove unused images
```

---

## 17. Summary

- Docker images are **immutable, layered templates** for creating containers.
- They are built from **Dockerfiles**, where each instruction usually creates a new layer.
- Layers provide **caching, sharing, and storage efficiency**.
- Tags, registries, and proper versioning are critical for managing images in real-world projects.
- Use **multi-stage builds**, **minimal base images**, and **non-root users** to create secure, efficient images.
- Regularly **inspect, prune, scan, and update** images as part of your container lifecycle.


