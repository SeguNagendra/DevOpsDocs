---
sidebar_position: 8
title: Performance & Caching 
---

# Performance & Caching 

Performance tuning is where NGINX truly shines.

Many people install NGINX... Few understand how to tune it properly.

In this module, we cover:

-   worker_processes tuning
-   worker_connections math (real calculation)
-   sendfile
-   keepalive
-   gzip compression
-   proxy_cache explained clearly
-   Cache invalidation thinking
-   Rate limiting deep dive
-   OS-level tuning basics

Layered format:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

# 1. worker_processes

## 🟢 Beginner Understanding

Defines number of worker processes.

Example:

worker_processes auto;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Best practice:

Set equal to number of CPU cores.

Check cores:

    nproc

Example:

4 CPU cores → worker_processes 4;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Each worker handles independent event loop.

Too many workers: Context switching overhead.

Too few workers: CPU underutilized.

Balance based on CPU architecture.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

8-core server running with worker_processes 1.

CPU underutilized → throughput limited.

Increasing workers improved performance.

------------------------------------------------------------------------

# 2. worker_connections (Real Math)

## 🟢 Beginner Understanding

Max connections per worker.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:

worker_processes 4; worker_connections 2048;

Theoretical max connections:

4 × 2048 = 8192

But remember:

Each proxy request may use 2 connections (Client + Upstream).

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Effective max connections ≠ theoretical value.

Must consider:

-   File descriptor limits
-   Keepalive connections
-   WebSocket connections
-   Upstream connections

Also tune:

worker_rlimit_nofile ulimit -n

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Traffic spike caused "Too many open files".

Solution:

Increase OS file descriptor limits.

------------------------------------------------------------------------

# 3. sendfile

## 🟢 Beginner Understanding

Improves static file serving.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Enable:

sendfile on;

Allows kernel to send files directly without copying to user space.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Reduces CPU usage for static files.

Works best for:

-   Images
-   Videos
-   CSS/JS

------------------------------------------------------------------------

## ⚫ Real Production Scenario

High static traffic consuming CPU.

Enabling sendfile reduced CPU usage significantly.

------------------------------------------------------------------------

# 4. keepalive_timeout

## 🟢 Beginner Understanding

Keeps connection open for reuse.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:

keepalive_timeout 65;

Short timeout → more connection overhead\
Long timeout → more open connections

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Must balance between:

-   Latency improvement
-   File descriptor usage
-   Memory usage

High traffic systems need careful tuning.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Too high keepalive → exhausted file descriptors.

Reduced timeout improved stability.

------------------------------------------------------------------------

# 5. GZIP Compression

## 🟢 Beginner Understanding

Compresses response to reduce size.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Enable:

gzip on; gzip_types text/plain text/css application/json;

Reduces bandwidth usage.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Trade-off:

-   CPU cost for compression
-   Bandwidth savings

Beneficial for text content. Not useful for already compressed images.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Enabling gzip reduced page load time by 40%.

------------------------------------------------------------------------

# 6. proxy_cache (Important)

## 🟢 Beginner Understanding

NGINX stores backend responses temporarily.

Next request served from cache.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Basic example:
```
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=mycache:10m
max_size=1g;

location / { proxy_cache mycache; proxy_pass http://backend; }
```
------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Cache design questions:

-   What should be cached?
-   For how long?
-   What should never be cached? (login, personalized pages)

Cache invalidation is hard.

Avoid caching dynamic user-specific content.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

API traffic reduced 70% after caching common responses.

Backend CPU dropped drastically.

------------------------------------------------------------------------

# 7. Rate Limiting (Deep Dive)

## 🟢 Beginner Understanding

Limit number of requests per IP.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:
```
limit_req_zone \$binary_remote_addr zone=api:10m rate=10r/s;

location /api { limit_req zone=api burst=20 nodelay; }
```
------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Rate limiting protects against:

-   Brute force
-   API abuse
-   Simple DDoS

Burst allows short traffic spikes.

Without burst → legitimate users may be blocked.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Login endpoint under attack.

Rate limiting stabilized system.

------------------------------------------------------------------------

# 8. OS-Level Tuning Basics

## 🟢 Beginner Understanding

System settings affect NGINX performance.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Tune:

ulimit -n\
net.core.somaxconn\
net.ipv4.ip_local_port_range

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

High concurrency systems require:

-   Increased file descriptor limits
-   Proper TCP tuning
-   Monitoring of TIME_WAIT sockets

NGINX performance depends on kernel tuning.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

High traffic system limited by kernel parameters, not NGINX config.

After sysctl tuning, performance improved.

------------------------------------------------------------------------

# Summary

After this module, you understand:

✔ worker_processes tuning\
✔ worker_connections math\
✔ sendfile usage\
✔ keepalive tuning\
✔ gzip compression\
✔ proxy_cache basics\
✔ Rate limiting strategy\
✔ OS-level tuning awareness

Next: Logging & Observability (Layered).
