---
sidebar_position: 8
---

# Docker Networking

## 1. What Is Docker Networking?

**Docker networking** enables containers to communicate with:
- Other containers
- The Docker host
- External systems (internet, APIs, databases)

Docker provides networking abstractions so that containers don’t need to worry about:
- IP management
- Routing
- Low-level network configuration

By default, Docker uses **Linux networking features** like:
- Network namespaces
- Virtual Ethernet pairs (veth)
- Bridges
- iptables (NAT & firewall rules)

---

## 2. Why Docker Networking Is Important

Docker networking allows:
- Microservices communication
- Service discovery using container names
- Network isolation for security
- Port publishing for external access
- Multi-host and overlay networking

Without proper networking:
- Containers cannot talk to each other
- Applications cannot expose services
- Scaling becomes complex

---

## 3. Docker Network Architecture (High Level)

Each Docker container:
- Has its own **network namespace**
- Gets its own virtual network interface
- Uses virtual switches/bridges created by Docker

Basic flow:
```text
Container → veth pair → Docker network → Host NIC → External Network
```

Docker manages:
- IP allocation
- DNS resolution
- Routing rules

---

## 4. Types of Docker Networks

Docker supports multiple network drivers.

| Network Driver | Description | Common Use Case |
|---------------|-------------|-----------------|
| bridge | Default, single-host networking | Most local apps |
| host | Share host’s network stack | High performance |
| none | No networking | Security / isolation |
| overlay | Multi-host networking | Swarm / clustering |
| macvlan | Container gets MAC & IP | Legacy apps |

---

## 5. Bridge Network (Default & User-Defined)

### 5.1 Default Bridge Network

Created automatically by Docker.

```bash
docker network ls
```

Default bridge name:
```text
bridge
```

Limitations:
- Containers communicate using IP, not name
- Not recommended for production

Example:
```bash
docker run -d nginx
docker run -d busybox sleep 1000
```

You must find IPs manually.

---

### 5.2 User-Defined Bridge Network (Recommended)

```bash
docker network create mybridge
```

Run containers:

```bash
docker run -d --name web --network mybridge nginx
docker run -d --name app --network mybridge busybox sleep 1000
```

Now containers can communicate using **container names**:
```text
http://web
```

Advantages:
- Built-in DNS
- Better isolation
- Custom subnet support

---

## 6. Host Network

In **host** mode, the container:
- Shares the host's network stack
- Does NOT get its own IP
- Uses host ports directly

```bash
docker run --network host nginx
```

Characteristics:
- No port mapping needed
- High performance
- No network isolation

⚠️ Linux-only (not fully supported on Docker Desktop)

---

## 7. None Network

Completely disables networking inside the container.

```bash
docker run --network none busybox
```

Use cases:
- Maximum isolation
- Security testing
- Batch jobs without network access

---

## 8. Overlay Network

Used for **multi-host Docker Swarm networking**.

Features:
- Containers on different hosts communicate
- Uses VXLAN tunneling
- Requires Swarm mode

Example:
```bash
docker network create   --driver overlay   --attachable myoverlay
```

Commonly used in:
- Docker Swarm
- Large distributed systems

---

## 9. Macvlan Network

Allows containers to appear as **physical devices** on the network.

Features:
- Each container gets its own MAC address
- Direct access to LAN
- No NAT

Example:
```bash
docker network create -d macvlan   --subnet=192.168.1.0/24   --gateway=192.168.1.1   -o parent=eth0 mymacvlan
```

Use cases:
- Legacy applications
- Network monitoring tools
- Apps needing real IPs

---

## 10. Inspecting Docker Networks

### List Networks
```bash
docker network ls
```

### Inspect Network
```bash
docker network inspect mybridge
```

Shows:
- Subnet & gateway
- Connected containers
- Driver type

---

## 11. Connecting & Disconnecting Containers

You can connect containers dynamically.

```bash
docker network connect mybridge mycontainer
docker network disconnect mybridge mycontainer
```

A container can be part of **multiple networks**.

---

## 12. Port Publishing (Exposing Services)

### Publish Container Port

```bash
docker run -p 8080:80 nginx
```

Format:
```text
HOST_PORT:CONTAINER_PORT
```

Multiple ports:
```bash
docker run -p 8080:80 -p 8443:443 nginx
```

---

## 13. Container DNS & Service Discovery

Docker has a built-in DNS server.

Capabilities:
- Containers resolve each other by **name**
- Works only in user-defined networks

Example:
```text
ping db
curl http://api:8080
```

DNS server:
```text
127.0.0.11
```

---

## 14. Network Isolation & Security

Docker networks provide isolation between containers.

Best practices:
- Separate frontend and backend networks
- Don’t expose internal services publicly
- Use firewall rules where required

Example:

```bash
docker network create frontend
docker network create backend
```

```text
frontend → web
backend → app, db
```

---

## 15. Docker Networking with Compose

Example `docker-compose.yml`:

```yaml
version: "3.9"

services:
  web:
    image: nginx
    networks:
      - frontend

  app:
    build: ./app
    networks:
      - frontend
      - backend

  db:
    image: mysql
    networks:
      - backend

networks:
  frontend:
  backend:
```

---

## 16. IP Address Management (IPAM)

Custom subnet example:
```bash
docker network create   --subnet=172.25.0.0/16   --gateway=172.25.0.1   customnet
```

Useful when:
- Integrating with existing infra
- Avoiding IP conflicts

---

## 17. Troubleshooting Docker Networks

### Check Network Reachability
```bash
docker exec -it container ping othercontainer
```

### Check Open Ports
```bash
docker exec -it container netstat -tuln
```

### Docker Network Cleanup
```bash
docker network prune
```

---

## 18. Common Issues & Mistakes

1. Using default bridge for production
2. Hardcoding container IPs
3. Exposing internal services unnecessarily
4. Port conflicts on host
5. Forgetting cleanup

---

## 19. Networking Best Practices

- Always use **user-defined bridge networks**
- Use container/service names for connectivity
- Expose only required ports
- Separate internal & external networks
- Avoid host network unless necessary
- Use overlay networks for multi-host setups

---

## 20. Docker Networking Cheat Sheet

```bash
docker network ls
docker network create mynet
docker network inspect mynet
docker network connect mynet container
docker network disconnect mynet container
docker network prune
```

---

## 21. Summary

- Docker networking enables container communication
- Multiple network drivers offer flexibility
- User-defined bridge networks are best for most apps
- DNS-based service discovery simplifies microservices
- Proper network segmentation improves security and scalability

