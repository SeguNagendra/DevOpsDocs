---
sidebar_position: 9
title: High Availability & Scaling
---

# High Availability & Scaling

In real production environments, one Tomcat server is NOT enough.

Why?

Because:

-   Servers can crash
-   Hardware can fail
-   Traffic can suddenly increase
-   Maintenance may require restart

If you have only one Tomcat instance, that becomes a Single Point of
Failure (SPOF).

In this module, you will clearly understand:

-   What High Availability (HA) means
-   What is Single Point of Failure
-   How Load Balancer works with Tomcat
-   Sticky sessions explained simply
-   Session replication basics
-   Stateless vs Stateful applications
-   Horizontal vs Vertical scaling

This module builds your production architecture thinking.

------------------------------------------------------------------------

# 1. What is High Availability (HA)?

High Availability means:

Your application remains accessible even if one server fails.

Goal:

-   Minimum downtime
-   No data loss
-   Seamless user experience

If one Tomcat crashes, another should handle traffic.

------------------------------------------------------------------------

# 2. Single Point of Failure (SPOF)

Single Point of Failure is any component that can bring down entire
system if it fails.

Example:

Client → Tomcat → Database

If only one Tomcat exists, and it crashes, application becomes
unavailable.

Solution: Add redundancy.

------------------------------------------------------------------------

# 3. Basic HA Architecture with Tomcat

Production-style architecture:

Internet → Load Balancer → Tomcat-1 → Tomcat-2 → Database

Load Balancer distributes traffic between Tomcat instances.

If Tomcat-1 fails, Load Balancer automatically sends traffic to
Tomcat-2.

------------------------------------------------------------------------

# 4. What is a Load Balancer?

Load Balancer distributes incoming requests across multiple servers.

It:

-   Performs health checks
-   Distributes traffic
-   Improves availability
-   Improves scalability

If one instance becomes unhealthy, Load Balancer stops sending traffic
to it.

------------------------------------------------------------------------

# 5. Sticky Sessions Explained

Problem:

Tomcat stores session in memory.

If user logs in on Tomcat-1, and next request goes to Tomcat-2, session
will not exist.

User may get logged out.

Solution 1: Sticky Sessions

Load Balancer ensures:

User always routed to same Tomcat instance.

This is simple and commonly used.

Downside: If that instance crashes, session is lost.

------------------------------------------------------------------------

# 6. Session Replication (Basic Idea)

Instead of keeping session in only one server, Tomcat can replicate
session to other instance.

If Tomcat-1 fails, Tomcat-2 has session copy.

This provides better fault tolerance.

Downside: - More network overhead - More memory usage - Complex
configuration

Many modern systems prefer stateless design instead.

------------------------------------------------------------------------

# 7. Stateless vs Stateful Applications

Stateful Application: Stores session in server memory.

Stateless Application: Does not store session in server. Uses:

-   JWT tokens
-   External session store (Redis)
-   Database

Stateless design is better for scaling.

Why?

Any request can go to any server.

------------------------------------------------------------------------

# 8. Horizontal vs Vertical Scaling

Vertical Scaling: Increase CPU/RAM of same server.

Example: 4GB → 16GB RAM

Limit: Hardware has upper limit.

Horizontal Scaling: Add more servers.

Example: 1 Tomcat → 3 Tomcat instances

Better for high traffic applications.

Modern cloud systems prefer horizontal scaling.

------------------------------------------------------------------------

# 9. Basic Clustering Concept

Tomcat supports clustering.

Clustering allows:

-   Session replication
-   Node discovery
-   Failover

However:

Clustering requires careful configuration. Not always needed for small
setups.

------------------------------------------------------------------------

# 10. Real-World HA Debug Scenario

Scenario: Users report random logout.

Possible causes:

-   No sticky session
-   Load balancer misconfiguration
-   Session replication disabled

Scenario: Traffic spike causing slow response.

Solution:

-   Add more Tomcat instances
-   Increase thread pool
-   Check DB performance

------------------------------------------------------------------------

# 11. Production HA Checklist

Before going live, verify:

✔ Minimum 2 Tomcat instances\
✔ Load balancer health check enabled\
✔ Sticky session configured (if needed)\
✔ Firewall rules correct\
✔ Database highly available\
✔ Proper monitoring setup

High availability is about removing weak links.

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Understand High Availability concept\
✔ Identify single point of failure\
✔ Understand load balancer role\
✔ Understand sticky sessions clearly\
✔ Understand session replication basics\
✔ Know stateless vs stateful difference\
✔ Understand horizontal vs vertical scaling

Next: DevOps & Automation Integration (Zero → Hero).
