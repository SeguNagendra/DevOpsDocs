---
sidebar_position: 13
title: Module 13 - Real-World Production Scenarios & Interview (Zero to
  Hero)
---

# Module 13 -- Real-World Production Scenarios & Interview (Zero → Hero)

This is the final module.

Here we combine everything you have learned and apply it to:

-   Real production incidents
-   2 AM outage situations
-   Practical debugging mindset
-   Common DevOps interview questions
-   Scenario-based answers

This module prepares you for both: ✔ Real-world responsibility\
✔ Practical DevOps interviews

------------------------------------------------------------------------

# 1. Scenario: 502 Bad Gateway

Problem: Users see "502 Bad Gateway".

What it usually means: Reverse proxy (Nginx / Load Balancer) cannot
reach Tomcat.

Step-by-step debugging:

1.  Check if Tomcat process running: ps -ef \| grep tomcat

2.  Check port listening: ss -lntp \| grep 8080

3.  Check firewall rules.

4.  Check logs: tail -f logs/catalina.out

5.  Check if app crashed due to memory error.

Root cause possibilities:

-   Tomcat stopped
-   Port changed
-   Firewall blocked
-   Application crash

Never restart blindly. Always identify cause.

------------------------------------------------------------------------

# 2. Scenario: High CPU Usage

Symptoms:

-   Server slow
-   top shows 100% CPU
-   Response time high

Debug flow:

1.  Identify Tomcat PID.
2.  Use top to check CPU usage per thread.
3.  Take thread dump: 
```
jstack `<PID>`{=html} \> dump.txt
```
4.  Check GC logs.
5.  Check if traffic spike occurred.

Possible causes:

-   Infinite loop in application
-   Too many threads
-   GC overhead
-   Heavy DB query

Do not immediately increase maxThreads. Understand bottleneck first.

------------------------------------------------------------------------

# 3. Scenario: OutOfMemoryError

Error in logs:

java.lang.OutOfMemoryError

Steps:

1.  Check heap settings (-Xms / -Xmx).
2.  Take heap dump: jmap -dump:live,format=b,file=heap.hprof
```
    `<PID>`{=html}
```
3.  Check number of sessions.
4.  Check memory leak possibility.

Temporary fix: Increase heap.

Permanent fix: Identify memory leak.

------------------------------------------------------------------------

# 4. Scenario: Random User Logout

Users report:

"After login, suddenly logged out."

Possible causes:

-   No sticky session
-   Load balancer misconfiguration
-   Session timeout too low
-   Tomcat restart

Check:

-   Load balancer configuration
-   Session timeout in web.xml
-   Tomcat restart logs

------------------------------------------------------------------------

# 5. Scenario: Port Not Accessible

User cannot access http://server:8080

Checklist:

1.  Is Tomcat running?
2.  Is port listening?
3.  Is firewall blocking?
4.  Is server.xml port correct?
5.  Is security group allowing port?

Layer-by-layer debugging is key.

------------------------------------------------------------------------

# 6. Scenario: SSL Expired

Users see browser warning.

Steps:

1.  Check certificate expiry.
2.  Renew certificate.
3.  Update keystore or load balancer.
4.  Restart service (if required).

Always monitor certificate expiry in advance.

------------------------------------------------------------------------

# 7. Scenario: Application Very Slow

Symptoms:

-   High response time
-   No crash
-   CPU moderate

Check:

1.  Thread pool usage.
2.  DB performance.
3.  GC frequency.
4.  Network latency.
5.  External API delays.

Performance is multi-layer problem.

------------------------------------------------------------------------

# 8. Common DevOps Interview Questions

Q1: Difference between maxThreads and maxConnections?

maxThreads: Number of threads processing requests.

maxConnections: Maximum simultaneous connections allowed.

------------------------------------------------------------------------

Q2: What happens if maxThreads is too low?

Requests queue up. Response time increases.

------------------------------------------------------------------------

Q3: How do you troubleshoot 502 error?

Check Tomcat process, port, logs, and load balancer connectivity.

------------------------------------------------------------------------

Q4: How to perform zero-downtime deployment?

Use multiple instances behind load balancer. Remove one instance →
deploy → add back → repeat.

------------------------------------------------------------------------

Q5: What is difference between sticky session and session replication?

Sticky session: User routed to same instance.

Session replication: Session copied across instances.

------------------------------------------------------------------------

Q6: What is difference between horizontal and vertical scaling?

Vertical: Increase server resources.

Horizontal: Add more servers.

------------------------------------------------------------------------

# 9. Production Mindset Checklist

During outage:

✔ Stay calm\
✔ Do not panic restart\
✔ Identify layer of failure\
✔ Check logs first\
✔ Validate recent changes\
✔ Communicate clearly

Good DevOps engineers think logically under pressure.

------------------------------------------------------------------------

# 10. Final Outcome of This Roadmap

After completing all modules, you can:

✔ Install and configure Tomcat\
✔ Deploy applications safely\
✔ Tune performance\
✔ Secure production environment\
✔ Scale using HA setup\
✔ Integrate with CI/CD\
✔ Run in containers & Kubernetes\
✔ Perform upgrades and backups\
✔ Handle real-world incidents confidently

You now have complete Zero → Hero practical Tomcat knowledge for a
DevOps engineer (0--5 Years level).

Continue practicing in real lab environments to build mastery.
