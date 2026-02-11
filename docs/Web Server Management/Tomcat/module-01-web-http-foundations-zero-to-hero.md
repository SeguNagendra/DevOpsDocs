---
sidebar_position: 1
title: Web & HTTP Foundations
---

# Web & HTTP Foundations

Before learning Apache Tomcat, a DevOps engineer must clearly understand
how the web works.

This module builds your foundation step-by-step in simple language.

------------------------------------------------------------------------

# 1.1 How the Web Actually Works

When you open a browser and type:

    https://example.com

The following happens behind the scenes:

1.  Browser converts domain to IP (DNS lookup)
2.  Browser connects to server IP on port 80 (HTTP) or 443 (HTTPS)
3.  Browser sends HTTP request
4.  Server processes request
5.  Server sends HTTP response
6.  Browser renders content

Flow in real production:

Client → Load Balancer → Web Server → Application Server (Tomcat) →
Database

As a DevOps engineer, you must know this entire flow.

------------------------------------------------------------------------

# 1.2 What is a Web Server?

A web server handles static content such as:

-   HTML
-   CSS
-   JavaScript
-   Images
-   Downloads

Examples: - Apache HTTP Server - Nginx

Main responsibilities:

-   Listen on port 80/443
-   Accept HTTP requests
-   Serve static files
-   Forward dynamic requests to backend

Important: Web server does NOT execute Java code.

------------------------------------------------------------------------

# 1.3 What is an Application Server?

An application server runs business logic.

Apache Tomcat is a Java Servlet container.

It: - Executes Java code - Processes dynamic requests - Connects to
database - Returns generated HTML/JSON

Example:

When user logs in → Tomcat verifies credentials → fetches data → returns
response.

------------------------------------------------------------------------

# 1.4 Understanding HTTP Protocol (Very Important)

HTTP = HyperText Transfer Protocol

It is stateless (server does not remember previous requests).

## HTTP Methods

GET -- Fetch data\
POST -- Send data\
PUT -- Update data\
DELETE -- Remove data\
PATCH -- Partial update\
OPTIONS -- Check allowed methods

------------------------------------------------------------------------

## HTTP Status Codes

2xx -- Success\
200 OK\
201 Created

3xx -- Redirection\
301 Permanent redirect\
302 Temporary redirect

4xx -- Client error\
400 Bad Request\
401 Unauthorized\
403 Forbidden\
404 Not Found

5xx -- Server error\
500 Internal Server Error\
502 Bad Gateway\
503 Service Unavailable

DevOps must quickly identify 4xx vs 5xx problems.

------------------------------------------------------------------------

# 1.5 Important HTTP Headers

Headers control how request/response behaves.

Common headers:

Host\
Content-Type\
Authorization\
User-Agent\
Cookie\
Set-Cookie\
Cache-Control

Understanding headers helps debug issues using curl.

------------------------------------------------------------------------

# 1.6 Cookies and Sessions

HTTP is stateless.

So how does website remember login?

Using sessions.

Flow:

1.  User logs in
2.  Server creates session ID
3.  Session ID stored in browser cookie
4.  Every request sends session ID
5.  Server maps session ID to user data

Important for DevOps:

-   Session timeout configuration
-   Sticky sessions in load balancer
-   Session replication in cluster

------------------------------------------------------------------------

# 1.7 Reverse Proxy Concept

A reverse proxy sits between client and backend servers.

Example:

Client → Nginx → Tomcat

Why use reverse proxy?

-   SSL termination
-   Security filtering
-   Load balancing
-   Hiding internal servers

In production, users rarely access Tomcat directly.

------------------------------------------------------------------------

# 1.8 Load Balancing Basics

Load balancer distributes traffic across multiple servers.

Common algorithms:

Round Robin\
Least Connections\
IP Hash

Benefits:

-   High availability
-   Scalability
-   Fault tolerance

Without load balancing, single Tomcat = single point of failure.

------------------------------------------------------------------------

# 1.9 HTTPS and TLS Basics

HTTPS = HTTP + Encryption

Encryption uses TLS.

Key terms:

Public key\
Private key\
Certificate\
Keystore\
SSL handshake

DevOps responsibilities:

-   Install certificate
-   Renew before expiry
-   Configure HTTPS in server.xml
-   Debug certificate issues

------------------------------------------------------------------------

# 1.10 Real Production Architecture Example

Typical enterprise setup:

Internet\
↓\
Load Balancer\
↓\
Web Server (Nginx / Apache)\
↓\
Tomcat\
↓\
Database

As a DevOps engineer, your job is to:

-   Ensure connectivity between layers
-   Open correct firewall ports
-   Monitor health
-   Debug failures quickly

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Understand how web traffic flows\
✔ Know difference between web server and app server\
✔ Understand HTTP protocol deeply\
✔ Know how sessions work\
✔ Understand reverse proxy and load balancing\
✔ Understand HTTPS basics

This foundation is mandatory before diving into Tomcat internals.

Next module: Apache Tomcat Architecture Deep Dive.
