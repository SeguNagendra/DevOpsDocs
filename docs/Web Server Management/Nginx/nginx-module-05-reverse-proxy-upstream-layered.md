---
sidebar_position: 5
title: Reverse Proxy & Upstrea (Layered Format)
---

# Reverse Proxy & Upstream

This is one of the MOST important modules.

NGINX is powerful mainly because of its reverse proxy capability.

In real production:

NGINX → Tomcat / Node / Python / Microservices

In this module, we cover:

-   proxy_pass explained correctly
-   proxy_set_header
-   X-Forwarded-For
-   Upstream block
-   Proxy buffering
-   Timeouts (connect/read/send)
-   client_max_body_size
-   Large file uploads
-   WebSocket support
-   502 & 504 debugging

Layered format:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

# 1. What is proxy_pass?

## 🟢 Beginner Understanding

proxy_pass forwards request to backend server.

Example:

location /api proxy_pass http://localhost:8080;

User → NGINX → Backend

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Important behavior:

If location ends with slash and proxy_pass ends without slash, URL
rewriting behaves differently.

Example:

location /app/ proxy_pass http://backend/;

Trailing slash behavior matters.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

proxy_pass does:

-   Opens connection to upstream
-   Sends modified request
-   Waits for response
-   Streams response back

It creates two connections:

Client ↔ NGINX\
NGINX ↔ Backend

This doubles connection handling responsibility.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

If backend slow:

NGINX may return:

504 Gateway Timeout

Because it waited too long for upstream.

------------------------------------------------------------------------

# 2. proxy_set_header

## 🟢 Beginner Understanding

NGINX forwards headers to backend.

Example:

proxy_set_header Host \$host; proxy_set_header X-Forwarded-For
\$proxy_add_x\_forwarded_for;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Important headers:

Host\
X-Real-IP\
X-Forwarded-For\
X-Forwarded-Proto

Without correct headers:

Backend may log wrong client IP.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Reverse proxy hides original client IP.

X-Forwarded-For preserves client identity.

Security systems depend on correct header forwarding.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Security audit shows all requests coming from 127.0.0.1.

Cause: Missing X-Forwarded-For configuration.

------------------------------------------------------------------------

# 3. Upstream Block

## 🟢 Beginner Understanding

Upstream defines backend group.

Example:

upstream backend  server 10.0.0.1:8080; server 10.0.0.2:8080; 

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Used for load balancing.

Then reference:

proxy_pass http://backend;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Upstream enables:

-   Horizontal scaling
-   Failover
-   Traffic distribution

NGINX supports:

Round robin (default)\
Least connections\
IP hash

------------------------------------------------------------------------

## ⚫ Real Production Scenario

If one backend crashes:

NGINX automatically routes to healthy server (if configured properly).

------------------------------------------------------------------------

# 4. Proxy Buffering

## 🟢 Beginner Understanding

NGINX can buffer backend response before sending to client.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

proxy_buffering on;

Improves performance for slow clients.

But may increase memory usage.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Buffering decouples backend from client speed.

Without buffering:

Slow client → Backend thread blocked.

With buffering:

Backend responds fast → NGINX streams slowly.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Application performance improved after enabling buffering.

Because backend threads were previously blocked by slow clients.

------------------------------------------------------------------------

# 5. Timeouts (Very Important)

Key timeout directives:

proxy_connect_timeout proxy_read_timeout proxy_send_timeout

------------------------------------------------------------------------

## 🟢 Beginner Understanding

If backend takes too long, NGINX times out.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

proxy_connect_timeout → time to establish connection\
proxy_read_timeout → wait time for response\
proxy_send_timeout → time to send request to backend

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Timeout tuning depends on:

-   Application response time
-   Network latency
-   SLA expectations

Too low → frequent 504\
Too high → slow failure detection

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Users facing 504 errors.

Cause: proxy_read_timeout too low.

------------------------------------------------------------------------

# 6. client_max_body_size

## 🟢 Beginner Understanding

Limits maximum upload size.

Example:

client_max_body_size 10M;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

If upload exceeds limit:

NGINX returns:

413 Request Entity Too Large

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Large uploads increase:

-   Memory pressure
-   Disk I/O (temporary files)

Limit must align with business needs.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

File upload failing after deployment.

Cause: client_max_body_size not configured.

------------------------------------------------------------------------

# 7. WebSocket Support

## 🟢 Beginner Understanding

WebSocket requires special headers.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Add:

proxy_set_header Upgrade \$http_upgrade; proxy_set_header Connection
"upgrade";

Without this: WebSocket handshake fails.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

WebSocket creates long-lived connections.

Must consider:

-   worker_connections
-   File descriptor limits

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Real-time dashboard not updating.

Cause: Missing WebSocket upgrade headers.

------------------------------------------------------------------------

# 8. 502 vs 504 Explained

502 Bad Gateway: Backend not reachable.

504 Gateway Timeout: Backend took too long.

------------------------------------------------------------------------

## 🟢 Beginner Understanding

502 → Connection problem\
504 → Timeout problem

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Check:

-   Backend running?
-   Port correct?
-   Firewall?
-   Timeouts configured?

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Frequent 502 may indicate:

-   Backend crashes
-   Resource exhaustion
-   Connection pool limit reached

Frequent 504 may indicate:

-   Slow DB queries
-   Thread exhaustion
-   Network latency

------------------------------------------------------------------------

## ⚫ Real Production Scenario

During traffic spike:

504 errors increase.

Cause: Backend thread pool exhausted.

------------------------------------------------------------------------

# Summary

After this module, you should understand:

✔ proxy_pass behavior\
✔ Header forwarding\
✔ Upstream load balancing\
✔ Proxy buffering logic\
✔ Timeout tuning\
✔ Upload size limits\
✔ WebSocket handling\
✔ 502 vs 504 difference

Next module: Load Balancing & High Availability (Layered).
