---
sidebar_position: 4
title: Server Blocks & Routing
---

# Server Blocks & Routing

Routing is one of the most misunderstood parts of NGINX.

Most production bugs happen because of:

-   Wrong server block match
-   Wrong location priority
-   Incorrect rewrite logic
-   Misuse of root vs alias

This module explains routing clearly in layers:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

# 1. What is a Server Block? (Virtual Host)

## 🟢 Beginner Understanding

A server block allows you to host multiple domains on the same NGINX
server.

Example:

server listen 80; server_name example.com;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

You can configure multiple domains:

server listen 80; server_name app1.com;

server listen 80; server_name app2.com;

NGINX chooses server block based on:

-   listen port
-   server_name match

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Server selection process:

1.  Match listen IP:port
2.  Match server_name
3.  If no match → default server

Order matters when multiple server blocks exist.

Always define a proper default server to avoid unexpected routing.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

If wrong domain shows wrong application:

Likely cause: Default server catching unmatched traffic.

------------------------------------------------------------------------

# 2. listen Directive

## 🟢 Beginner Understanding

listen defines port number.

Example:

listen 80; listen 443 ssl;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

You can specify:

listen 0.0.0.0:80; listen 127.0.0.1:8080;

This allows binding to specific interfaces.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

In high-security environments:

Bind internal apps to localhost only.

Example:

listen 127.0.0.1:8080;

Prevents external access.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

If port open but app not reachable:

Check if NGINX listening on correct interface.

------------------------------------------------------------------------

# 3. server_name Matching

## 🟢 Beginner Understanding

server_name defines domain handled by server block.

Example:

server_name example.com www.example.com;

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Wildcard support:

server_name \*.example.com;

Default server:

server_name \_;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Matching priority:

1.  Exact match
2.  Longest wildcard match
3.  Regex match

Misconfiguration can cause traffic routing errors.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Users accessing subdomain routed incorrectly.

Cause: Wildcard matching misconfigured.

------------------------------------------------------------------------

# 4. Location Block & Matching Priority

Location defines routing rules inside server block.

Example:

location /api proxy_pass http://backend;

------------------------------------------------------------------------

## 🟢 Beginner Understanding

location tells NGINX what to do for specific URL paths.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Location types:

Exact match: location = /login

Prefix match: location /api

Regex match: location \~ .php\$

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Location matching priority:

1.  Exact match (=)
2.  Longest prefix match
3.  Regex match (first match)
4.  Default prefix

Order of regex definitions matters.

Misunderstanding this causes production routing bugs.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Problem: /api/admin routed to wrong backend.

Cause: Regex location overriding prefix.

Fix: Adjust location priority.

------------------------------------------------------------------------

# 5. root vs alias (Common Confusion)

## 🟢 Beginner Understanding

root: Appends request URI to specified path.

alias: Replaces matching path completely.

Example:

location /images root /var/www;

Request: /images/logo.png

File path: /var/www/images/logo.png

------------------------------------------------------------------------

alias example:

location /images alias /var/static/images;

Request: /images/logo.png

File path: /var/static/images/logo.png

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Misusing alias can cause 404 errors.

Ensure trailing slash usage correct.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

root preserves URI structure. alias remaps path.

For large static file setups, alias is often used for performance
clarity.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Static files returning 404 after migration.

Cause: Incorrect alias configuration.

------------------------------------------------------------------------

# 6. rewrite vs return

## 🟢 Beginner Understanding

rewrite modifies URL internally. return sends redirect response
immediately.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example redirect:

return 301 https://example.com\$request_uri;

Example rewrite:

rewrite \^/old/(.\*)\$ /new/\$1 permanent;

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Use return for simple redirects. Use rewrite only when necessary.

Too many rewrites increase processing complexity.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

SEO ranking dropped.

Cause: Incorrect redirect code (302 instead of 301).

------------------------------------------------------------------------

# 7. Redirect Types (301 vs 302)

## 🟢 Beginner Understanding

301 → Permanent redirect\
302 → Temporary redirect

------------------------------------------------------------------------

## 🔵 DevOps Practical View

For HTTP → HTTPS:

Use 301.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Search engines cache 301 permanently.

Wrong usage affects SEO and caching behavior.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Users stuck on wrong domain after migration.

Cause: Improper redirect configuration.

------------------------------------------------------------------------

# 8. Common Routing Bugs

✔ Overlapping location blocks\
✔ Regex overriding prefix\
✔ Missing trailing slash\
✔ Wrong root/alias usage\
✔ Missing default server

Routing must be tested carefully.

------------------------------------------------------------------------

# Summary

After this module, you should understand:

✔ Server block selection logic\
✔ listen directive usage\
✔ server_name matching priority\
✔ Location block priority\
✔ root vs alias difference\
✔ rewrite vs return usage\
✔ How to debug routing problems

Next module: Reverse Proxy & Upstream Deep Dive (Layered).
