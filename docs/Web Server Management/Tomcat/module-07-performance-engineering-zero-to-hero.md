---
sidebar_position: 7
title: Performance Engineering
---

# Performance Engineering

Performance problems are common in production.

Users say: - "Application is slow" - "Requests are timing out" - "Server
CPU is high"

As a DevOps engineer, you must understand:

-   How Tomcat handles load
-   How thread pools work
-   How JVM memory works
-   How to tune basic performance safely
-   How to identify bottlenecks

This module builds that clarity.

------------------------------------------------------------------------

# 1. How Tomcat Handles Load

When multiple users send requests:

-   Each request is handled by a worker thread
-   Threads come from a thread pool
-   If all threads are busy → requests wait in queue

Performance issues usually relate to:

-   Thread exhaustion
-   Memory pressure
-   Slow database
-   High traffic spikes

------------------------------------------------------------------------

# 2. Understanding Thread Pool in Detail

Important Connector settings in server.xml:

maxThreads minSpareThreads acceptCount maxConnections

maxThreads → Maximum number of request-processing threads.

If 300 users hit server and maxThreads=200: 200 handled immediately 100
wait in queue

acceptCount → Size of waiting queue when all threads are busy.

If queue is full: New connections get rejected.

maxConnections → Maximum simultaneous connections allowed.

Important: Increasing maxThreads increases memory usage.

Each thread consumes stack memory.

Never blindly increase values.

------------------------------------------------------------------------

# 3. Practical Thread Tuning Strategy

Step 1: Check CPU cores

    nproc

Step 2: Start with reasonable maxThreads (e.g., 200--300)

Step 3: Monitor:

-   CPU usage
-   Response time
-   Thread count
-   Memory usage

If CPU constantly 100%: More threads will not help.

------------------------------------------------------------------------

# 4. JVM Memory Basics (Very Important)

Tomcat runs inside JVM.

Two important memory settings:

-Xms → Initial heap size -Xmx → Maximum heap size

Example in setenv.sh:

    export CATALINA_OPTS="-Xms512m -Xmx1024m"

If Xmx too low: OutOfMemoryError

If Xmx too high: OS may suffer memory pressure

Rule of thumb: Do not allocate 100% system memory to JVM.

Leave memory for: - OS - Other processes - Buffer/cache

------------------------------------------------------------------------

# 5. Garbage Collection (Basic Understanding)

JVM automatically cleans unused memory.

This process is called Garbage Collection (GC).

If GC runs too frequently: Application becomes slow.

Signs of GC issue:

-   High CPU
-   Frequent Full GC logs
-   Long response time spikes

Modern Java versions use G1GC by default.

You can enable GC logs to monitor behavior.

------------------------------------------------------------------------

# 6. Database Connection Pooling

Applications connect to database using connection pool.

If DB pool size is small: Requests wait → Slow response.

If too large: DB overloaded.

Connection pool is usually configured in:

context.xml (JNDI Resource)

Important parameters:

maxTotal maxIdle

Performance tuning must consider both:

-   Tomcat threads
-   DB connections

------------------------------------------------------------------------

# 7. Identifying Bottlenecks

If application slow, check in this order:

1.  CPU usage (top)
2.  Memory usage (free -m)
3.  Thread pool usage
4.  GC logs
5.  Database response time
6.  Network latency

Performance is always a chain. Weakest link causes slowdown.

------------------------------------------------------------------------

# 8. Load Testing Basics

Before production release, test load.

Common metrics:

Response Time Throughput (requests per second) Error Rate CPU usage
Memory usage

Simple tools:

-   Apache JMeter
-   curl loop testing
-   Basic stress testing

Load testing helps identify limits before users do.

------------------------------------------------------------------------

# 9. Capacity Planning (Beginner Level)

Ask questions:

-   How many users expected?
-   Peak traffic time?
-   Average response time?
-   Hardware capacity?

Plan:

CPU cores Memory Thread pool size DB capacity

Never wait for failure to scale.

------------------------------------------------------------------------

# 10. Common Performance Mistakes

❌ Increasing maxThreads blindly\
❌ Allocating too much heap memory\
❌ Ignoring GC logs\
❌ Not monitoring DB performance\
❌ No load testing before release

Performance tuning requires balance.

------------------------------------------------------------------------

# Summary

After this module, you should:

✔ Understand thread pool behavior\
✔ Tune maxThreads safely\
✔ Understand JVM heap basics\
✔ Recognize GC impact\
✔ Understand DB connection pooling\
✔ Identify bottlenecks logically\
✔ Understand load testing basics\
✔ Plan basic capacity

Next: Security Hardening (Zero → Hero).
