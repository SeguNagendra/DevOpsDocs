---
sidebar_position: 9
---

# Docker Volumes

## 1. What are Docker Volumes?

A **Docker volume** is a mechanism for **persisting data generated and used by containers**, outside the container’s writable layer.

In simple words:
> **Volumes store data permanently, independent of container lifecycle.**

Key points:
- Volumes are managed by Docker
- Data lives outside containers
- Safe from container deletion
- Can be shared between multiple containers

---

## 2. Why Do Containers Need Volumes?

By default, containers are **ephemeral**.

Example:
```bash
docker run mysql
docker rm mysql
```

➡️ **All data is lost**

### Problems Without Volumes
- Database data disappears when container is removed
- Logs vanish after restart
- Files disappear on image update
- No easy data sharing between containers

👉 **Volumes solve these problems**.

---

## 3. Container Storage Without Volumes

Each container has:
- Image layers (read-only)
- One writable container layer

This writable layer:
- Exists only while container exists
- Is slow for heavy I/O
- Is not meant for permanent data

```text
Image Layers (read-only)
-----------------------
Container Writable Layer  <-- deleted with container ❌
```

---

## 4. What Problems Volumes Solve

| Problem | Without Volumes | With Volumes |
|------|-----------------|--------------|
| Container deletion | Data lost | Data persists ✅ |
| App upgrade | Data lost | Safe ✅ |
| Backup | Hard | Easy ✅ |
| Sharing data | Not possible | Easy ✅ |
| DB performance | Poor | Optimized ✅ |

---

## 5. Types of Mounts in Docker

Docker supports **three types** of mounts:

| Type | Description | Managed By Docker | Best Use |
|----|-------------|-------------------|----------|
| Volume | Docker-managed storage | ✅ Yes | Databases, Prod |
| Bind Mount | Host path mounted | ❌ No | Dev/Test |
| tmpfs | Memory-based mount | ✅ Yes | Sensitive temporary data |

---

## 6. Docker Volumes (Preferred)

### 6.1 What Is a Named Volume?

A **named volume** is a persistent storage location managed by Docker.

Example:
```bash
docker volume create mysql_data
```

Run container using volume:
```bash
docker run -d   --name mysql   -v mysql_data:/var/lib/mysql   mysql:8.0
```

✅ Data survives container deletion

---

### 6.2 Anonymous Volumes

Docker automatically creates volumes if no name is specified.

```bash
docker run -v /var/lib/mysql mysql
```

Drawback:
- Hard to track
- Hard to clean up

👉 **Avoid for production**.

---

## 7. Where Are Volumes Stored?

On Linux:
```text
/var/lib/docker/volumes/
```

Each volume:
```text
/var/lib/docker/volumes/mysql_data/_data
```

Docker controls access, security, and structure.

---

## 8. Bind Mounts

Bind mounts attach a **host directory** directly into a container.

```bash
docker run -v /home/user/app:/app node
```

Pros:
- Live code sync
- Helpful for development

Cons:
- Tied to host OS layout
- Less portable
- Security risk

---

## 9. tmpfs Mounts

Memory-based storage (RAM).

```bash
docker run --tmpfs /app nginx
```

Use cases:
- Temporary files
- Secrets
- Cache

⚠️ Data disappears when container stops.

---

## 10. Sharing Volumes Between Containers

Multiple containers can share a volume.

```bash
docker volume create shared_data

docker run -d --name c1 -v shared_data:/data busybox sleep 1000
docker run -d --name c2 -v shared_data:/data busybox sleep 1000
```

✅ Used in:
- Microservices
- Shared logs
- Sidecar containers

---

## 11. Copying Data Using Volumes

If destination directory is empty:
```bash
docker run -v data:/app nginx
```

Docker copies existing container data into volume.

Helpful for:
- Initial DB schema setup
- Default configs

---

## 12. Docker Volumes with Dockerfile

```dockerfile
VOLUME ["/var/lib/mysql"]
```

Purpose:
- Documents expected persistent path
- Does NOT automatically keep data unless volume is attached

---

## 13. Docker Volumes with Docker Compose

```yaml
version: "3.9"

services:
  db:
    image: mysql:8.0
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

Start:
```bash
docker compose up -d
```

---

## 14. Volume Lifecycle

### Create Volume
```bash
docker volume create myvol
```

### List Volumes
```bash
docker volume ls
```

### Inspect Volume
```bash
docker volume inspect myvol
```

### Remove Volume
```bash
docker volume rm myvol
```

⚠️ Remove only when not used by containers.

---

## 15. Backup and Restore Volumes

### Backup Volume Data
```bash
docker run --rm   -v mysql_data:/volume   -v $(pwd):/backup   busybox   tar cvf /backup/mysql_backup.tar /volume
```

### Restore Volume
```bash
docker run --rm   -v mysql_data:/volume   -v $(pwd):/backup   busybox   tar xvf /backup/mysql_backup.tar -C /
```

---

## 16. Performance Benefits of Volumes

- Faster than container writable layer
- Optimized for heavy I/O
- Better suited for databases

👉 **Recommended for DBs like MySQL, PostgreSQL, MongoDB**

---

## 17. Volume Security Best Practices

- Use named volumes for production
- Restrict volume access
- Avoid mounting sensitive host directories
- Use tmpfs for secrets
- Backup volumes regularly

---

## 18. Common Mistakes

1. Not using volumes for databases
2. Using bind mounts in production
3. Deleting volumes accidentally
4. Storing secrets in images
5. Sharing volumes without access control

---

## 19. Volume Prune & Cleanup

### Remove Unused Volumes
```bash
docker volume prune
```

Dangerous:
```bash
docker system prune --volumes
```

⚠️ Deletes unused volumes permanently.

---

## 20. Docker Volumes Cheat Sheet

```bash
docker volume create myvol
docker volume ls
docker volume inspect myvol
docker volume rm myvol
docker volume prune
docker run -v myvol:/path image
```

---

## 21. Why Volumes Are Critical in Real Projects

Without volumes:
- Production DB crashes = data loss
- App upgrade wipes data

With volumes:
- Stateless containers ✅
- Persistent data ✅
- Easy scaling ✅
- Safe updates ✅

👉 **Volumes enable cloud-native, production-ready containers**.

---

## 22. Summary

- Containers are ephemeral; volumes provide persistence
- Volumes are Docker-managed and production-grade
- Bind mounts are for development only
- tmpfs is for temporary sensitive data
- Volumes improve performance, safety, and reliability


