---
sidebar_position: 2
title: Apache Tomcat Architecture
---

# Apache Tomcat Architecture

In Module 01, you learned how web traffic flows from client to server.

Now we go inside Apache Tomcat and understand:

-   What Tomcat really is
-   How it handles a request internally
-   What Catalina, Coyote, and Jasper are
-   How threads work
-   How sessions are stored
-   How applications are isolated
-   What a DevOps engineer must monitor

This module is designed to remove confusion completely.

------------------------------------------------------------------------

# 1. What Exactly is Apache Tomcat?

Apache Tomcat is a Java Servlet Container.

It is NOT just a web server.

Tomcat is responsible for:

-   Running Java web applications (WAR files)
-   Executing Servlets
-   Processing JSP files
-   Managing sessions
-   Handling HTTP requests
-   Managing thread pools

In production architecture:

Client → Load Balancer → Web Server → Tomcat → Database

Tomcat sits in the application layer.

------------------------------------------------------------------------

# 2. High-Level Internal Components

Tomcat internally has three main components:

1.  Coyote -- Connector layer
2.  Catalina -- Servlet container
3.  Jasper -- JSP engine

Let us understand them clearly.

------------------------------------------------------------------------

# 3. Coyote -- The Connector Layer

Coyote is responsible for:

-   Listening on configured port (default 8080)
-   Accepting HTTP requests
-   Converting HTTP data into internal request format
-   Sending response back to client

If port 8080 is not accessible, issue is usually here.

Common connector types:

HTTP/1.1\
AJP\
HTTP/2

If Tomcat is running but browser cannot connect: - Check port - Check
firewall - Check connector configuration in server.xml

------------------------------------------------------------------------

# 4. Catalina -- The Servlet Container

Catalina is the heart of Tomcat.

Responsibilities:

-   Loads web applications
-   Manages servlet lifecycle
-   Routes request to correct application
-   Executes business logic
-   Manages sessions

When a request reaches Tomcat:

1.  Catalina checks context path
2.  Identifies correct web application
3.  Finds matching servlet
4.  Executes it
5.  Sends response back

If application throws error, issue is usually inside Catalina layer.

------------------------------------------------------------------------

# 5. Jasper -- The JSP Engine

Jasper handles JSP files.

When a JSP is accessed:

1.  JSP is converted into a Servlet (Java class)
2.  It is compiled
3.  Executed like normal servlet

If JSP fails, error often happens during compilation.

Most modern applications use fewer JSPs and more REST APIs.

------------------------------------------------------------------------

# 6. Complete Request Flow Inside Tomcat

Let's trace one request step-by-step:

1.  Client sends HTTP request.
2.  Coyote receives request on port 8080.
3.  Request converted into Servlet request object.
4.  Catalina finds correct application.
5.  Filter chain executes (if any filters configured).
6.  Servlet executes business logic.
7.  Response generated.
8.  Coyote converts response into HTTP format.
9.  Response sent back to client.

If application is slow, problem could be:

-   Thread pool exhausted
-   Database slow
-   High CPU usage
-   Garbage collection pause

------------------------------------------------------------------------

# 7. Connector I/O Models (BIO vs NIO vs NIO2)

Tomcat supports different I/O models.

BIO (Blocking I/O) - One thread per connection - Not scalable - Old
model

NIO (Non-Blocking I/O) - Better scalability - Uses selector mechanism -
Default in modern Tomcat

NIO2 - Advanced asynchronous model - Good for high concurrency systems

In most cases, NIO is recommended.

------------------------------------------------------------------------

# 8. Thread Pool -- How Tomcat Handles Multiple Requests

Tomcat uses worker threads.

Important parameters in server.xml:

maxThreads\
minSpareThreads\
acceptCount\
maxConnections

How it works:

-   Each request gets assigned to a thread.
-   Thread executes servlet.
-   After completion, thread returns to pool.

If maxThreads is too low: Requests wait → Slow response.

If too high: High memory usage → Possible crash.

Understanding thread pool is critical for performance tuning.

------------------------------------------------------------------------

# 9. Web Applications and Context Path

Tomcat can run multiple applications.

Example:

http://server:8080/app1\
http://server:8080/app2

Each application runs in its own context.

If one application crashes, others may continue working.

------------------------------------------------------------------------

# 10. ClassLoader Concept (Simplified)

Tomcat uses hierarchical class loading.

Why?

To isolate applications from each other.

Each web application has its own classloader.

This prevents:

-   Library conflicts
-   Version clashes between apps

If you see ClassNotFoundException: Often related to classpath or wrong
JAR placement.

------------------------------------------------------------------------

# 11. Session Management Internals

When user logs in:

-   Tomcat creates HttpSession object.
-   Generates unique session ID (JSESSIONID).
-   Session ID stored in browser cookie.
-   Session data stored in server memory.

Important:

By default, sessions are in memory.

If Tomcat restarts: Sessions are lost.

In clustered setup: You need session replication or sticky sessions.

------------------------------------------------------------------------

# 12. Important Configuration Files

server.xml → Defines connectors, ports, thread settings

context.xml → Application-level configuration

web.xml → Global deployment descriptor

Understanding these files is critical before moving to installation and
deployment.

------------------------------------------------------------------------

# Summary

After completing this module, you should clearly understand:

✔ What Tomcat really is\
✔ Difference between Coyote, Catalina, Jasper\
✔ Internal request lifecycle\
✔ Thread pool behavior\
✔ Connector types\
✔ Session handling\
✔ Application isolation\
✔ Important configuration files

Next module: Installation & Environment Setup (Zero → Hero).
