---
sidebar_position: 6
title: Load Balancing & High Availability
---

# Load Balancing & High Availability

High traffic systems cannot rely on a single backend server.

NGINX helps distribute traffic across multiple backend servers.

In this module, we cover:

-   Why load balancing is needed
-   Upstream load balancing algorithms
-   Round robin
-   least_conn
-   ip_hash
-   Basic failover behavior
-   Health check basics
-   Sticky session concept
-   NGINX in front of Tomcat cluster
-   Architect-level HA thinking

Layered format:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

# 1. Why Load Balancing is Needed

## 🟢 Beginner Understanding

If 1 server handles 10,000 users, it may crash.

Solution: Use multiple backend servers.

NGINX distributes requests between them.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:

upstream backend server 10.0.0.1:8080; server 10.0.0.2:8080; 

location /  proxy_pass http://backend; 

Traffic is automatically distributed.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Load balancing provides:

-   Horizontal scaling
-   Fault tolerance
-   Better resource utilization

But it introduces new challenges:

-   Session management
-   Data consistency
-   Monitoring complexity

------------------------------------------------------------------------

## ⚫ Real Production Scenario

During peak sale event, single server CPU hits 100%.

After enabling load balancing with 3 servers, traffic distributed
evenly.

------------------------------------------------------------------------

# 2. Round Robin (Default Algorithm)

## 🟢 Beginner Understanding

Requests distributed sequentially:

Server A → Server B → Server A → Server B

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Round robin works well when:

-   Backend servers have similar capacity
-   Request processing time is similar

No extra configuration required.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Round robin does not consider:

-   Current load
-   Active connections
-   CPU usage

Not ideal if backend performance varies.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

One backend slower than others.

Round robin still sends equal traffic → slow responses.

------------------------------------------------------------------------

# 3. least_conn Algorithm

## 🟢 Beginner Understanding

Sends request to server with least active connections.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Configuration:
```
upstream backend { least_conn; server 10.0.0.1:8080; server
10.0.0.2:8080; }
```
Better for uneven workloads.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Works well when:

-   Long-lived connections
-   Variable request times

More intelligent than round robin.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

One request takes 5 seconds, others take 100ms.

least_conn prevents overloading slow server.

------------------------------------------------------------------------

# 4. ip_hash Algorithm

## 🟢 Beginner Understanding

Routes same client IP to same backend server.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Configuration:
```
upstream backend { ip_hash; server 10.0.0.1:8080; server 10.0.0.2:8080; }
```

Used for basic session stickiness.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

ip_hash depends on client IP.

Problems:

-   NAT environments
-   Corporate networks
-   Shared IP users

Not perfect solution for session handling.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Multiple users behind same office IP all routed to same backend → uneven
load.

------------------------------------------------------------------------

# 5. Failover Behavior

## 🟢 Beginner Understanding

If one server goes down, NGINX can route traffic to healthy server.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:
```
upstream backend { server 10.0.0.1:8080 max_fails=3 fail_timeout=30s;
server 10.0.0.2:8080; }
```
After 3 failed attempts, NGINX marks server temporarily unavailable.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Failover is passive by default.

NGINX detects failure only after request fails.

Active health checks require additional modules (NGINX Plus).

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Backend crashed.

First few requests fail with 502, then traffic routed to healthy server.

------------------------------------------------------------------------

# 6. Sticky Sessions Concept

## 🟢 Beginner Understanding

User should stay connected to same backend server.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Methods:

-   ip_hash
-   Cookie-based routing (advanced setups)
-   External session store (Redis)

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Sticky sessions limit scalability.

Better approach: Design stateless applications.

Store sessions in external store.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

User logs in, next request routed to different server → logout.

Solution: Sticky session or centralized session store.

------------------------------------------------------------------------

# 7. NGINX in Front of Tomcat Cluster

## 🟢 Beginner Understanding

NGINX distributes traffic across multiple Tomcat instances.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Architecture:

Internet\
→ NGINX\
→ Tomcat-1\
→ Tomcat-2

Tomcat handles business logic.

NGINX handles routing & load balancing.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Important considerations:

-   Session replication vs sticky session
-   Health check monitoring
-   Backend scaling limits
-   DB bottlenecks

Load balancing only solves web tier scaling, not database scaling.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Traffic doubled.

Added 2 more Tomcat servers. Updated upstream block. Reloaded NGINX.
System handled load successfully.

------------------------------------------------------------------------

# 8. High Availability Thinking

## 🟢 Beginner Understanding

Avoid single point of failure.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Use:

-   Multiple backend servers
-   Monitoring
-   Auto-restart mechanisms

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

NGINX itself can become single point of failure.

Solution:

-   Multiple NGINX instances
-   Cloud load balancer in front
-   Keepalived (virtual IP failover)

HA must consider entire stack.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

NGINX server crashed.

Entire application became unavailable.

Lesson: NGINX also needs redundancy.

------------------------------------------------------------------------

# Summary

After this module, you should understand:

✔ Why load balancing is needed\
✔ Round robin vs least_conn vs ip_hash\
✔ Failover behavior\
✔ Sticky session concept\
✔ NGINX + Tomcat cluster setup\
✔ High availability thinking

Next module: SSL / HTTPS & Security Hardening (Layered).
