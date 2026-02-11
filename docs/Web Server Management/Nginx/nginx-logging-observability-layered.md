---
sidebar_position: 9
title: Logging & Observability
---

# Logging & Observability

When production breaks, logs are your best friend.

A strong DevOps engineer reads logs. A strong Architect designs systems
with observability in mind.

In this module, we cover:

-   access_log explained properly
-   error_log levels
-   Custom log_format
-   Logging upstream response time
-   Debug logging
-   502 / 504 troubleshooting flow
-   Reload vs restart debugging
-   Centralized logging concepts

Layered format:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

# 1. access_log

## 🟢 Beginner Understanding

access_log records every request made to NGINX.

Example location:

/var/log/nginx/access.log

Each line shows:

-   Client IP
-   Request method
-   URL
-   Status code
-   Response size

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Basic configuration:

access_log /var/log/nginx/access.log;

To disable for specific location:

access_log off;

Useful for reducing noise on health checks.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Access logs are critical for:

-   Traffic analysis
-   Security monitoring
-   Capacity planning
-   Debugging latency

Logs should be structured and centralized for large systems.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Users report slowness.

Access logs show increased response time for /api endpoint.

Root cause traced to backend latency.

------------------------------------------------------------------------

# 2. error_log

## 🟢 Beginner Understanding

error_log records issues and warnings.

Example:

error_log /var/log/nginx/error.log;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Log levels:

error\
warn\
info\
debug

Example:

error_log /var/log/nginx/error.log warn;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Higher verbosity (debug) increases disk I/O.

Use debug only temporarily.

Permanent debug logging in production can degrade performance.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

502 errors occurring intermittently.

error_log shows:

"connect() failed (111: Connection refused)"

Backend service was down.

------------------------------------------------------------------------

# 3. Custom log_format

## 🟢 Beginner Understanding

You can customize how logs look.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:

log_format main '\$remote_addr - \$request - \$status - \$request_time';

access_log /var/log/nginx/access.log main;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Include important fields:

-   \$request_time
-   \$upstream_response_time
-   \$upstream_addr
-   \$http_user_agent

This helps diagnose:

-   Backend latency
-   Network issues
-   Client behavior

Structured logs improve monitoring.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Slow requests unclear.

After adding \$upstream_response_time, identified backend DB latency
issue.

------------------------------------------------------------------------

# 4. Logging Upstream Response Time

## 🟢 Beginner Understanding

Shows how long backend took to respond.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Add to log_format:

\$upstream_response_time

Helps separate:

NGINX delay vs Backend delay.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

If:

request_time \>\> upstream_response_time

Problem likely client-side or network.

If:

upstream_response_time high

Problem is backend.

Observability allows correct blame assignment.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Users complain about slowness.

Logs show backend responding in 50ms, but total request_time 3s.

Issue was slow mobile network clients.

------------------------------------------------------------------------

# 5. Debug Logging

## 🟢 Beginner Understanding

Debug logs show detailed processing steps.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Enable temporarily:

error_log /var/log/nginx/error.log debug;

Restart or reload.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Debug logs show:

-   Location matching
-   Rewrite evaluation
-   Upstream selection

Very helpful for routing issues.

Disable after debugging.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Location block behaving unexpectedly.

Enabled debug log to inspect matching order.

Issue resolved.

------------------------------------------------------------------------

# 6. 502 vs 504 Troubleshooting Flow

## 🟢 Beginner Understanding

502 → Backend unreachable\
504 → Backend too slow

------------------------------------------------------------------------

## 🔵 DevOps Practical Flow

Step 1: Check error_log\
Step 2: Check backend service\
Step 3: Check firewall\
Step 4: Check timeouts\
Step 5: Check resource usage

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Frequent 502 may indicate:

-   Backend crashes
-   Port exhaustion
-   Connection pool exhaustion

Frequent 504 may indicate:

-   Slow DB queries
-   Thread starvation
-   Network bottleneck

Systemic issues require architectural fixes.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

504 errors increased during traffic spike.

Backend thread pool saturated.

Solution: scale backend horizontally.

------------------------------------------------------------------------

# 7. Reload vs Restart Debugging

## 🟢 Beginner Understanding

Reload applies config changes gracefully.

Restart stops and starts service.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

If config change not applied:

Check:

nginx -t\
nginx -T

Confirm correct config file loaded.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

In large systems with many include files, misplaced config may silently
override expected behavior.

Configuration version control recommended.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Config updated but behavior unchanged.

Issue: edited wrong included file.

------------------------------------------------------------------------

# 8. Centralized Logging & Observability Thinking

## 🟢 Beginner Understanding

Logs can be stored in one central place.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Send logs to:

-   ELK stack
-   Splunk
-   Cloud logging services

Enables search and monitoring.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Observability includes:

-   Logs
-   Metrics
-   Traces

NGINX logs + backend metrics provide full visibility.

Design systems assuming failure will happen.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Single server logs not enough during outage.

After centralizing logs, faster root cause analysis possible.

------------------------------------------------------------------------

# Summary

After this module, you understand:

✔ access_log usage\
✔ error_log levels\
✔ Custom log_format\
✔ Upstream response time logging\
✔ Debug logging safely\
✔ 502 / 504 troubleshooting flow\
✔ Reload vs restart debugging\
✔ Observability mindset

Next: Containers & Kubernetes Integration (Layered).
