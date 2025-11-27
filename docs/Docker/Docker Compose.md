---
sidebar_position: 7
---

# Docker Compose 

## 1. What Is Docker Compose?

**Docker Compose** is a tool used to define and run **multi-container Docker applications** using a single YAML file.

With Docker Compose, you can:
- Define multiple services (containers)
- Configure networks and volumes
- Start everything using **one command**
- Manage application lifecycle easily

Instead of running multiple `docker run` commands, you use:

```bash
docker compose up
```

---

## 2. Why Docker Compose?

Without Docker Compose:
```bash
docker run -d --name db mysql
docker run -d --name backend backend-image
docker run -d --name frontend frontend-image
```

With Docker Compose:
```bash
docker compose up
```

### Key Use Cases
- Microservices-based applications
- Local development environments
- Integration testing
- CI/CD pipelines

---

## 3. Docker Compose Architecture

Docker Compose works on top of the Docker Engine.

Components:
1. **docker-compose.yml**
2. Docker Engine
3. Containers
4. Networks
5. Volumes

Flow:
- Compose reads the YAML file
- Creates networks and volumes
- Builds images (if required)
- Starts containers in correct order

---

## 4. Docker Compose File (`docker-compose.yml`)

Docker Compose configuration uses **YAML** format.

### Basic Structure

```yaml
version: "3.9"

services:
  service1:
    image: image-name
  service2:
    build: .

networks:
  default:

volumes:
  data:
```

---

## 5. Version in Docker Compose

Compose file versions define supported features.

Common versions:
- `2.x`
- `3.x` (most widely used)

Recommended:
```yaml
version: "3.9"
```

> Note: Docker Compose v2 (plugin) no longer requires `version` but it’s still good for clarity.

---

## 6. Services

A **service** represents a container definition.

Example:

```yaml
services:
  web:
    image: nginx:1.27
    ports:
      - "8080:80"
```

Each service can have:
- Image or build context
- Environment variables
- Volumes
- Networks
- Dependencies

---

## 7. Build vs Image

### Using Pre-built Image
```yaml
services:
  app:
    image: node:22-alpine
```

### Building Image with Dockerfile
```yaml
services:
  app:
    build: .
```

Advanced build:
```yaml
build:
  context: .
  dockerfile: Dockerfile
  args:
    APP_ENV: production
```

---

## 8. Ports Mapping

```yaml
ports:
  - "8080:80"
```

Format:
```text
HOST_PORT:CONTAINER_PORT
```

Multiple ports supported:
```yaml
ports:
  - "8080:80"
  - "8443:443"
```

---

## 9. Environment Variables

### Inline Environment Variables

```yaml
environment:
  APP_ENV: production
  DEBUG: "false"
```

### Using `.env` File

```yaml
env_file:
  - .env
```

`.env` example:
```text
DB_HOST=db
DB_PORT=5432
```

---

## 10. Volumes (Persistent Storage)

Volumes ensure data persists even if containers are removed.

### Named Volumes

```yaml
services:
  db:
    image: mysql:8.0
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

### Bind Mounts

```yaml
volumes:
  - ./code:/app
```

---

## 11. Networks

By default, Docker Compose creates a **bridge network**.

### Default Network

```yaml
services:
  web:
    image: nginx
```

Containers communicate using **service names**.

### Custom Network

```yaml
networks:
  backend:

services:
  api:
    image: api
    networks:
      - backend
```

---

## 12. depends_on (Service Dependencies)

```yaml
services:
  app:
    depends_on:
      - db
```

Controls **startup order only**, NOT readiness.

For health-based dependency, use `healthcheck`.

---

## 13. Healthcheck

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost"]
  interval: 30s
  timeout: 5s
  retries: 3
```

Check health:
```bash
docker compose ps
```

---

## 14. Restart Policies

```yaml
restart: always
```

Options:
- `no`
- `always`
- `on-failure`
- `unless-stopped`

---

## 15. Resource Limits

```yaml
deploy:
  resources:
    limits:
      cpus: "1.0"
      memory: 512M
```

> For non-Swarm local usage:
```yaml
mem_limit: 512m
cpus: 1.0
```

---

## 16. Scaling Services

```bash
docker compose up --scale web=3
```

Only works if:
- No static port bindings
- Load balancing via internal network

---

## 17. Docker Compose Commands

### Basic Commands

```bash
docker compose up
docker compose up -d
docker compose down
```

### Other Useful Commands

```bash
docker compose build
docker compose ps
docker compose logs
docker compose logs -f
docker compose restart
docker compose stop
docker compose start
docker compose exec service bash
```

---

## 18. Complete Example – Web + DB

```yaml
version: "3.9"

services:
  web:
    image: nginx:1.27
    ports:
      - "8080:80"
    depends_on:
      - app

  app:
    build: ./app
    environment:
      DB_HOST: db
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

Start:
```bash
docker compose up -d
```

Stop & cleanup:
```bash
docker compose down -v
```

---

## 19. Best Practices

- Use explicit image versions
- Keep services small and focused
- Use volumes for database storage
- Avoid hardcoding secrets
- Use `.env` files
- Use healthchecks for readiness
- Break large apps into multiple Compose files

---

## 20. Compose Override Files

Docker Compose automatically loads:

```text
docker-compose.yml
docker-compose.override.yml
```

Used for environment-specific overrides.

Example:
```yaml
services:
  web:
    environment:
      DEBUG: "true"
```

---

## 21. Docker Compose vs Kubernetes

| Feature | Docker Compose | Kubernetes |
|------|----------------|------------|
| Setup | Simple | Complex |
| Use case | Dev / Small apps | Production / Large scale |
| Learning curve | Easy | Steep |
| Scaling | Limited | Advanced |
| Networking | Simple | Advanced |

---

## 22. Docker Compose Cheat Sheet

```bash
docker compose up -d
docker compose down
docker compose build
docker compose ps
docker compose logs -f
docker compose exec web bash
docker compose restart
```

---

## 23. Summary

- Docker Compose simplifies **multi-container application management**
- Uses a single YAML file
- Handles services, networks, and volumes
- Ideal for development, testing, and CI/CD
- Not meant to replace Kubernetes for large-scale production

This document is suitable for **training, documentation, and interview preparation**.


