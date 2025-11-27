---
sidebar_position: 5
---

# Docker Containers

## 1. What Is a Docker Container?

A **Docker container** is a lightweight, portable, and isolated runtime environment created from a **Docker image**.

In simple terms:
- **Image** → Blueprint (read-only)
- **Container** → Running instance of that blueprint

A container includes:
- Application code
- Dependencies
- Runtime environment
- A writable layer on top of the image

Containers allow applications to run **consistently across environments** (dev, test, prod).

---

## 2. Container vs Virtual Machine

| Feature            | Docker Container                         | Virtual Machine                     |
|--------------------|------------------------------------------|-------------------------------------|
| OS Kernel          | Shares host OS kernel                    | Has its own guest OS                |
| Startup Time       | Seconds or less                          | Minutes                             |
| Resource Usage     | Lightweight                              | Heavy (RAM + disk)                  |
| Isolation          | Process-level isolation                 | Hardware-level isolation            |
| Performance        | Near native                              | Slight overhead                     |
| Portability        | Very high                                | Medium                              |

Containers are **not mini VMs** — they are isolated processes.

---

## 3. Docker Container Architecture

When you run a container:

1. Docker uses an **image** (read-only layers)
2. Adds a **writable container layer** on top
3. Executes the configured command
4. Uses Linux features:
   - Namespaces (isolation)
   - cgroups (resource limits)
   - Union filesystem (layers)

**Key Point:**  
All file changes inside a container are written to the container’s writable layer.

---

## 4. Container Lifecycle

A Docker container moves through several states:

```text
Created → Running → Paused → Stopped → Deleted
```

### 4.1 Lifecycle Commands

```bash
docker create     # create container (not started)
docker start      # start container
docker stop       # stop container gracefully
docker kill       # force stop
docker restart    # stop + start
docker pause      # pause processes
docker unpause    # resume processes
docker rm         # delete container
```

A **stopped container still exists** until removed.

---

## 5. Creating and Running Containers

### 5.1 Run a Container

```bash
docker run nginx
```

This does:
1. Pull image (if not present)
2. Create container
3. Start container

### 5.2 Common `docker run` Options

```bash
docker run   --name mynginx   -d   -p 8080:80   nginx:1.27
```

Explanation:
- `--name` – container name
- `-d` – detached (background)
- `-p` – port mapping (host:container)
- `nginx:1.27` – image

### 5.3 Interactive Containers

```bash
docker run -it ubuntu bash
```

- `-i` – interactive
- `-t` – pseudo-TTY

Good for debugging and learning.

---

## 6. Listing and Inspecting Containers

### 6.1 List Containers

```bash
docker ps        # running containers
docker ps -a     # all containers
```

### 6.2 Inspect a Container

```bash
docker inspect mynginx
```

Shows:
- IP address
- Mounted volumes
- Environment variables
- Command & entrypoint
- Network settings

### 6.3 Container Logs

```bash
docker logs mynginx
docker logs -f mynginx   # follow logs
```

Logs come from **STDOUT/STDERR** of the main process.

---

## 7. Container Networking

Every container:

- Gets its own network namespace
- Has its own IP address (inside Docker network)

### 7.1 Port Mapping

```bash
docker run -p 8080:80 nginx
```

- Host port: `8080`
- Container port: `80`

Access via:
```text
http://localhost:8080
```

### 7.2 Container-to-Container Communication

Best practice:
- Put containers in the **same user-defined network**
- Use **container names** as hostnames

```bash
docker network create mynet

docker run -d --name web --network mynet nginx
docker run -d --name app --network mynet busybox sleep 1000
```

Inside `app`, you can reach `web` via:
```text
http://web
```

---

## 8. Container Storage & Writable Layer

### 8.1 Container Writable Layer

- Each container has a **private writable layer**
- Changes are lost when the container is deleted

Bad practice:
```bash
docker run mysql   # data lost if container removed
```

### 8.2 Persistent Storage (Volumes)

Use volumes for persistent data.

```bash
docker volume create mysql-data

docker run -d   --name mysql   -v mysql-data:/var/lib/mysql   mysql:8.0
```

Volumes:
- Survive container deletion
- Are managed by Docker

---

## 9. Executing Commands Inside Containers

### 9.1 `docker exec`

```bash
docker exec -it mynginx bash
```

Use cases:
- Debug issues
- Check files
- Inspect running processes

### 9.2 Difference: `run` vs `exec`

| Command       | Purpose                             |
|--------------|-------------------------------------|
| `docker run` | Create + start a new container      |
| `docker exec`| Run command inside existing container |

---

## 10. Environment Variables in Containers

### 10.1 Passing Env Variables

```bash
docker run -e ENV=production nginx
```

### 10.2 Using Env File

```bash
docker run --env-file .env myapp
```

Example `.env`:
```text
DB_HOST=db
DB_PORT=5432
```

Avoid hardcoding secrets inside images.

---

## 11. Resource Limits (CPU & Memory)

### 11.1 Memory Limits

```bash
docker run -m 512m nginx
```

### 11.2 CPU Limits

```bash
docker run --cpus=1.5 nginx
```

### 11.3 Check Resource Usage

```bash
docker stats
```

Shows live:
- CPU usage
- Memory usage
- Network IO

---

## 12. Container Restart Policies

Restart policies control container behavior on failure.

```bash
docker run --restart always nginx
```

Available policies:
- `no` (default)
- `always`
- `on-failure`
- `unless-stopped`

Used heavily in production.

---

## 13. Stopping and Removing Containers

### 13.1 Stop Containers

```bash
docker stop mynginx
docker kill mynginx
```

### 13.2 Remove Containers

```bash
docker rm mynginx
docker rm -f mynginx    # force remove
```

### 13.3 Cleanup

```bash
docker container prune   # remove stopped containers
```

---

## 14. Container Security Best Practices

- Run containers as **non-root**
- Use minimal images
- Limit resources
- Avoid privileged containers
- Scan images for vulnerabilities

Bad practice:
```bash
docker run --privileged nginx
```

Good practice:
```dockerfile
USER appuser
```

---

## 15. Practical Hands-On Example

### 15.1 Run a Web Server Container

```bash
docker run -d   --name web   -p 8080:80   nginx
```

Check:
```text
http://localhost:8080
```

### 15.2 Exec into Container

```bash
docker exec -it web bash
ls /usr/share/nginx/html
```

### 15.3 Stop and Remove

```bash
docker stop web
docker rm web
```

---

## 16. Common Docker Container Commands Cheat Sheet

```bash
docker run image
docker ps
docker ps -a
docker start container
docker stop container
docker restart container
docker rm container
docker logs container
docker exec -it container bash
docker inspect container
docker stats
```

---

## 17. Summary

- Docker containers are **isolated runtime instances** of images
- They share the host kernel but run independently
- Containers start fast and use minimal resources
- Data inside containers is ephemeral unless volumes are used
- Proper networking, storage, and security practices are essential
- Containers are the foundation of modern microservices and DevOps workflows


