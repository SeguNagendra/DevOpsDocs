---
sidebar_position: 6
---

# Dockerfile

## 1. What Is a Dockerfile?

A **Dockerfile** is a text file that contains a set of instructions on how to build a Docker **image**.

You can think of it as:

- A **recipe** to bake an image
- A **build script** executed by the Docker engine
- A **declarative definition** of your environment

Command to build an image from a Dockerfile:

```bash
docker build -t myimage:1.0 .
```

Here:
- `-t myimage:1.0` → name and tag
- `.` → build context (directory containing Dockerfile and app files)

By default, Docker looks for a file named **`Dockerfile`** in the build context.

---

## 2. Dockerfile Basic Structure

Typical Dockerfile layout:

```dockerfile
# 1. Base image
FROM ubuntu:24.04

# 2. Metadata (optional)
LABEL maintainer="dev@example.com"

# 3. Environment setup
WORKDIR /app
ENV APP_ENV=production

# 4. Copy dependencies and install
COPY requirements.txt .
RUN apt-get update && apt-get install -y python3-pip     && pip3 install --no-cache-dir -r requirements.txt

# 5. Copy application code
COPY . .

# 6. Expose ports (for info)
EXPOSE 8000

# 7. Define default command
CMD ["python3", "app.py"]
```

Execution happens **top to bottom**, each instruction creates (or modifies) a layer.

---

## 3. Build Context and `.dockerignore`

### 3.1 Build Context

When you run:

```bash
docker build -t myimage:1.0 .
```

The last `.` is the **build context directory**. Docker:

1. Packs that directory
2. Sends it to the Docker daemon
3. Dockerfile instructions like `COPY` and `ADD` can only access files **inside** this context.

### 3.2 `.dockerignore`

To avoid sending unnecessary files (large, secret, or irrelevant), use a `.dockerignore` file.

Example `.dockerignore`:

```gitignore
.git
*.log
node_modules
__pycache__/
.env
Dockerfile*
*.md
```

Benefits:
- Faster builds (smaller context)
- More secure (do not send secrets)
- Cleaner images

---

## 4. Common Dockerfile Instructions

### 4.1 `FROM` – Base Image

Every Dockerfile (except those using multi-stage continuation) must start with `FROM`.

```dockerfile
FROM ubuntu:24.04
FROM python:3.11-slim
FROM node:22-alpine
```

Special base image: **scratch** (empty image)

```dockerfile
FROM scratch
COPY my-binary /my-binary
ENTRYPOINT ["/my-binary"]
```

### 4.2 `RUN` – Execute Commands During Build

Used to install packages, configure the OS, etc.

```dockerfile
RUN apt-get update && apt-get install -y curl
RUN pip install --no-cache-dir flask
```

Best practice: combine related commands to reduce layers:

```dockerfile
RUN apt-get update && apt-get install -y curl git     && rm -rf /var/lib/apt/lists/*
```

You can use **shell form** or **exec form**:

```dockerfile
RUN apt-get update        # shell form
RUN ["apt-get", "update"] # exec form
```

### 4.3 `COPY` – Copy Files from Build Context

```dockerfile
COPY . /app
COPY requirements.txt /app/requirements.txt
COPY src/ /app/src/
```

- Source is relative to **build context**
- Destination is inside the **image filesystem**

You can also use file permissions (in newer Docker versions):

```dockerfile
COPY --chmod=755 script.sh /usr/local/bin/script.sh
```

### 4.4 `ADD` – Like COPY, But More Features

`ADD` can:
- Copy local files like `COPY`
- Automatically extract local tar archives
- Download from URLs (not recommended)

Example:

```dockerfile
ADD app.tar.gz /app/
```

**Best practice:** Use `COPY` unless you need the extra features of `ADD`.

### 4.5 `WORKDIR` – Set Working Directory

```dockerfile
WORKDIR /app
COPY . .
RUN ls
```

If the directory does not exist, Docker creates it.

**Better than** using `RUN cd /app` (which only affects that command).

### 4.6 `CMD` – Default Command

Defines the **default command** when a container starts.

```dockerfile
CMD ["python", "app.py"]
```

You can override it at runtime:

```bash
docker run myimage:1.0 python other_script.py
```

Forms:

- **Exec form (recommended)**:
  ```dockerfile
  CMD ["nginx", "-g", "daemon off;"]
  ```

- **Shell form**:
  ```dockerfile
  CMD nginx -g "daemon off;"
  ```

### 4.7 `ENTRYPOINT` – Main Executable

Defines the **main process** of the container.

```dockerfile
ENTRYPOINT ["python", "app.py"]
```

Difference vs `CMD`:

- `ENTRYPOINT` → defines the **fixed** executable
- `CMD` → provides **default arguments** or fallback command

Combine them:

```dockerfile
ENTRYPOINT ["python", "app.py"]
CMD ["--port", "8080"]
```

At runtime:

```bash
docker run myimage:1.0 --port 9000
```

### 4.8 `ENV` – Environment Variables

Set environment variables inside the image:

```dockerfile
ENV APP_ENV=production
ENV DB_HOST=db DB_PORT=5432
```

Used later by the app or other instructions.

Env variables can be overridden at runtime:

```bash
docker run -e APP_ENV=dev myimage:1.0
```

### 4.9 `ARG` – Build-Time Variables

Available only at **build time**, not at container runtime.

```dockerfile
ARG APP_VERSION=1.0.0
RUN echo "Building version $APP_VERSION"
```

Pass during build:

```bash
docker build --build-arg APP_VERSION=2.0.0 -t myimage:2.0 .
```

You can combine `ARG` and `ENV`:

```dockerfile
ARG APP_VERSION=1.0.0
ENV APP_VERSION=${APP_VERSION}
```

Now available at runtime as env var.

### 4.10 `EXPOSE` – Document Ports

Informs others which ports the container listens on:

```dockerfile
EXPOSE 80
EXPOSE 8080/tcp
```

It does **not** publish ports automatically; you still need `-p` in `docker run`.

### 4.11 `VOLUME` – Declare Mount Points

Declares that a path is meant to be a volume:

```dockerfile
VOLUME ["/var/lib/mysql"]
```

Useful to remind users that data should be persisted outside the container.

### 4.12 `USER` – Set User

Run subsequent instructions and container processes as a non-root user:

```dockerfile
RUN useradd -m appuser
USER appuser
```

Helps security by avoiding root in containers.

### 4.13 `HEALTHCHECK` – Container Health

Define how to check if container is healthy:

```dockerfile
HEALTHCHECK --interval=30s --timeout=5s --retries=3   CMD curl -f http://localhost:8080/health || exit 1
```

States: `starting`, `healthy`, `unhealthy`.

### 4.14 `LABEL` – Metadata

Add key-value metadata to images:

```dockerfile
LABEL maintainer="dev@example.com"
LABEL org.opencontainers.image.source="https://github.com/org/repo"
```

Useful for automation, scanning, and documentation.

### 4.15 `ONBUILD` – Triggers for Child Images

`ONBUILD` adds instructions that will run **when the image is used as a base image**.

```dockerfile
ONBUILD COPY . /app
ONBUILD RUN npm install
```

Generally less used today; multi-stage builds are preferred.

### 4.16 `STOPSIGNAL` – Stop Signal

Specify system signal used to stop the container:

```dockerfile
STOPSIGNAL SIGTERM
```

### 4.17 `SHELL` – Default Shell

Change default shell used by `RUN`, `CMD`, `ENTRYPOINT` (shell form):

```dockerfile
SHELL ["powershell", "-Command"]
```

Useful for Windows-based images.

---

## 5. Multi-Stage Builds

**Multi-stage builds** make images **smaller and more secure** by separating build and run stages.

### 5.1 Example: Go Application

```dockerfile
# Stage 1: Build
FROM golang:1.23-alpine AS builder

WORKDIR /src
COPY . .
RUN go build -o myapp

# Stage 2: Runtime (minimal image)
FROM alpine:3.20

WORKDIR /app
COPY --from=builder /src/myapp .

EXPOSE 8080
ENTRYPOINT ["./myapp"]
```

Benefits:
- Build tools (`go`, compilers, etc.) are not in final image
- Smaller image size
- Reduced attack surface

### 5.2 Multi-Stage for Node.js

```dockerfile
# Stage 1: Build
FROM node:22-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve
FROM nginx:1.27-alpine

COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

## 6. Layer Caching & Build Optimization

Every instruction creates a **layer**. Docker caches these layers.

**Rule:** If an instruction and its context (inputs) do not change, Docker reuses the cached layer.

### 6.1 Good Pattern for Caching

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# 1. Copy only requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 2. Copy the rest of the source code
COPY . .

CMD ["python", "app.py"]
```

If you change only `app.py`, the `pip install` layer is reused.

### 6.2 Bad Pattern (Breaks Cache Easily)

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY . .
RUN pip install --no-cache-dir -r requirements.txt
```

Any file change invalidates the `COPY . .` layer → `pip install` runs again.

### 6.3 Combine Commands

Instead of:

```dockerfile
RUN apt-get update
RUN apt-get install -y curl
```

Prefer:

```dockerfile
RUN apt-get update && apt-get install -y curl     && rm -rf /var/lib/apt/lists/*
```

Fewer layers, smaller images.

---

## 7. Best Practices for Dockerfiles

1. **Use minimal base images**
   - `alpine`, `debian:bookworm-slim`, `ubuntu:24.04` minimal
   - Language images: `python:3.11-slim`, `node:22-alpine`

2. **Pin versions**
   - Avoid `latest` in production
   - Pin OS packages and language deps

3. **Leverage multi-stage builds**
   - Keep final image lean and secure

4. **Reduce layers**
   - Combine related `RUN` commands

5. **Use `.dockerignore`**
   - Exclude `.git`, logs, build artifacts, etc.

6. **Don’t run as root (if possible)**
   ```dockerfile
   RUN useradd -m appuser
   USER appuser
   ```

7. **Don’t store secrets in images**
   - No passwords/API keys in Dockerfile
   - Use env vars, secret managers, external config

8. **Make builds reproducible**
   - Deterministic dependencies and versions

9. **Log to stdout/stderr**
   - So `docker logs` can see them

10. **Use health checks**
    - For better orchestration (Kubernetes, Swarm, etc.)

---

## 8. Practical Example 1 – Python Flask App

**Project Structure:**

```text
flask-app/
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
    return "Hello from Docker!"

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

**Build & Run:**

```bash
docker build -t flask-app:1.0 .
docker run -d --name flask-app -p 5000:5000 flask-app:1.0
```

Open: `http://localhost:5000`

---

## 9. Practical Example 2 – Node.js App with Multi-Stage

**`Dockerfile`:**

```dockerfile
# Stage 1 – Dependencies
FROM node:22-alpine AS deps

WORKDIR /app
COPY package*.json ./
RUN npm install --production

# Stage 2 – Runtime
FROM node:22-alpine

WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

Build & Run:

```bash
docker build -t node-app:1.0 .
docker run -d --name node-app -p 3000:3000 node-app:1.0
```

---

## 10. Practical Example 3 – Nginx Static Site

**`Dockerfile`:**

```dockerfile
FROM nginx:1.27-alpine

COPY ./public /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Build & Run:

```bash
docker build -t static-site:1.0 .
docker run -d --name static-site -p 8080:80 static-site:1.0
```

Open: `http://localhost:8080`

---

## 11. Common Dockerfile Pitfalls

1. **Using `latest` everywhere**
   - Leads to non-reproducible builds

2. **Large images**
   - Installing unnecessary tools
   - Not cleaning cache/temp files

3. **Not using `.dockerignore`**
   - Sending `.git`, `node_modules`, temp files

4. **Copying secrets into images**
   - `.env`, SSH keys, etc.

5. **Too many layers**
   - One `RUN` per tiny command

6. **Running as root**
   - Higher security risk

7. **Heavy build contexts**
   - Running `docker build .` from project root without ignoring

---

## 12. Dockerfile and Image Relationship

- Dockerfile defines **how** to build the image
- Each instruction → **layer** in the image
- Built image is referenced by a **name:tag**

Commands to inspect:

```bash
docker history myimage:1.0
docker inspect myimage:1.0
```

---

## 13. Dockerfile Cheat Sheet

```dockerfile
# Base image
FROM image:tag

# Metadata
LABEL key="value"

# Build args
ARG NAME=value

# Environment vars
ENV NAME=value

# Working directory
WORKDIR /path

# Copy files
COPY src dest
ADD src dest

# Run commands
RUN command

# Expose port
EXPOSE 80

# Volumes
VOLUME ["/data"]

# Healthcheck
HEALTHCHECK --interval=30s --timeout=5s   CMD curl -f http://localhost/ || exit 1

# User
USER appuser

# Entrypoint and CMD
ENTRYPOINT ["executable", "arg1"]
CMD ["arg2"]
```

---

## 14. Summary

- A **Dockerfile** is a script of instructions to build a Docker image.
- Each instruction creates a **layer**, and layer caching speeds up builds.
- Key instructions include `FROM`, `RUN`, `COPY`, `CMD`, `ENTRYPOINT`, `ENV`, `ARG`, `WORKDIR`, `EXPOSE`, `VOLUME`, `USER`, `HEALTHCHECK`, and `LABEL`.
- Use **.dockerignore**, **multi-stage builds**, **minimal base images**, and **non-root users** for efficient and secure images.
- Dockerfiles are central to container-based workflows, CI/CD pipelines, and modern application delivery.

