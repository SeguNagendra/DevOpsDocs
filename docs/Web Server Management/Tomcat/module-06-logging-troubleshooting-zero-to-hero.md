---
sidebar_position: 6
title: Logging & Troubleshooting
---

# Logging & Troubleshooting

This is one of the MOST important modules for a DevOps engineer.

Installing Tomcat is easy. Deploying WAR is easy.

But when production breaks at 2 AM --- your ability to read logs and
troubleshoot correctly is what matters.

In this module, you will clearly understand:

-   All important Tomcat log files
-   Where errors appear
-   How to read stack traces
-   How to take thread dumps
-   Basic heap dump understanding
-   jstack and jmap basics
-   Linux-level debugging commands
-   Step-by-step production troubleshooting method

------------------------------------------------------------------------

# 1. Where Are Tomcat Logs Located?

Default location:

    /opt/tomcat/logs/

Important log files:

catalina.out\
localhost.log\
manager.log\
host-manager.log\
access_log.\*

Understanding which log to check saves time.

------------------------------------------------------------------------

# 2. catalina.out (Main Log File)

This is the primary runtime log.

It contains:

-   Application errors
-   Stack traces
-   Startup logs
-   Shutdown logs
-   OutOfMemory errors

To monitor logs in real-time:

    tail -f logs/catalina.out

If application returns 500 error: This is the first file to check.

------------------------------------------------------------------------

# 3. localhost.log

Contains logs related to specific web applications.

Useful when:

-   One application failing
-   Multiple apps deployed

Helps isolate which app caused problem.

------------------------------------------------------------------------

# 4. Access Logs

Access logs show:

-   Who accessed
-   Which URL
-   Response status code
-   Response time

Example entry:

127.0.0.1 - - \[10/Feb/2026:10:20:30\] "GET /app HTTP/1.1" 200 1024

If users report slowness: Check response time in access logs.

Access log configuration is in server.xml.

------------------------------------------------------------------------

# 5. Understanding Java Stack Trace

When error happens, you see something like:

java.lang.NullPointerException at
com.example.MyClass.method(MyClass.java:25)

How to read it:

-   Top line = actual error
-   Next lines = call sequence
-   First application class = where issue originated

DevOps Role:

You may not fix code, but you must identify whether issue is:

-   Code issue
-   Configuration issue
-   Infrastructure issue

------------------------------------------------------------------------

# 6. Thread Dump -- When Application is Slow

If application hangs or CPU is high, take thread dump.

Command:

    jstack $PID > threaddump.txt

First find PID:

    ps -ef | grep tomcat

Thread dump helps identify:

-   Deadlocks
-   Stuck threads
-   High CPU threads

Basic pattern to check:

Look for many threads in BLOCKED state.

------------------------------------------------------------------------

# 7. Heap Dump -- Memory Issues

If you see:

java.lang.OutOfMemoryError

Take heap dump:

    jmap -dump:live,format=b,file=heap.hprof $PID

Heap dump is large file. Used with tools like Eclipse MAT for analysis.

Common causes:

-   Memory leak
-   Too many sessions
-   High thread count

------------------------------------------------------------------------

# 8. GC Logs (Basic Idea)

Garbage Collection cleans unused memory.

If GC is frequent: Application may slow down.

Enable GC logging in setenv.sh:

    export CATALINA_OPTS="-Xlog:gc*"

Signs of GC problem:

-   CPU high
-   Long pause times
-   Frequent full GC

------------------------------------------------------------------------

# 9. Linux-Level Debugging (Very Important)

Tomcat runs on Linux.

You must know these commands:

Check port listening:

    netstat -tulnp | grep 8080
    or
    ss -lntp | grep 8080

Check CPU usage:

    top
    htop

Check memory usage:

    free -m

Check open files:

    lsof -p $PID

Check disk space:

    df -h

Sometimes problem is NOT Tomcat. It is OS-level issue.

------------------------------------------------------------------------

# 10. Step-by-Step Production Troubleshooting Flow

If application is DOWN:

Step 1: Check if server reachable (ping / SSH) Step 2: Check Tomcat
process running Step 3: Check port listening Step 4: Check logs
(catalina.out) Step 5: Check CPU & memory Step 6: Check DB connectivity
Step 7: Check Load Balancer health

Never panic. Always debug layer by layer.

------------------------------------------------------------------------

# 11. Common Real-World Scenarios

Scenario 1: 502 Bad Gateway Cause: Reverse proxy cannot reach Tomcat.

Scenario 2: High CPU Cause: Thread loop / GC issue / high traffic.

Scenario 3: Application very slow Cause: Thread pool exhausted / DB
slow.

Scenario 4: Frequent restarts Cause: Memory crash / OOM.

------------------------------------------------------------------------

# Summary

After this module, you should confidently:

✔ Locate and read Tomcat logs\
✔ Understand stack traces\
✔ Take thread dumps\
✔ Take heap dumps\
✔ Perform basic GC analysis\
✔ Use Linux debugging commands\
✔ Follow structured troubleshooting process

Next: Performance Engineering (Zero → Hero).
