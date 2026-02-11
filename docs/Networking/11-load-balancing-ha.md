---
sidebar_position: 11
title: Load Balancing & High Availability (Keeping Apps Alive)
description: Learn how load balancers and HA actually keep applications running, explained calmly like a mentor.
---

# Load Balancing & High Availability (Keeping Apps Alive)

## Mentor Truth

Users don’t care **which server** handled their request.
They only care that the app works.

Load balancing and high availability exist to:
- Hide failures
- Spread traffic
- Keep systems alive when things break

Failures are normal. Downtime is optional.

---

## Why One Server Is Never Enough

Even the best server can fail:
- Hardware issues
- Kernel panic
- Memory leaks
- Deployments gone wrong

If you have only one server:
> Failure = outage

High availability exists to avoid that.

---

## What a Load Balancer Really Does

A load balancer sits **in front of servers** and:
- Accepts client traffic
- Chooses a healthy backend
- Forwards requests
- Stops sending traffic to unhealthy servers

Clients never see backend servers directly.

---

## Layer 4 vs Layer 7 (Simple View)

### Layer 4 (Transport)
- Works with TCP/UDP
- Faster
- No understanding of HTTP

Used when:
- You want speed
- You don’t care about URLs

### Layer 7 (Application)
- Understands HTTP/HTTPS
- Can route by path, host, headers
- Slightly slower

Used when:
- You need smart routing
- Microservices are involved

Choose based on need, not trend.

---

## Load Balancing Algorithms (Only the Important Ones)

### Round Robin
- Each server gets a turn
- Simple and common

### Least Connections
- Server with least active connections wins
- Good for uneven workloads

### IP Hash
- Same client goes to same server
- Used for session stickiness

No algorithm fixes a bad app.

---

## Health Checks (Most Important Feature)

Health checks decide:
> “Is this server alive enough to receive traffic?”

If health checks are wrong:
- Good servers look bad
- Bad servers receive traffic

This causes random failures.

---

## Session Stickiness (Use Carefully)

Sticky sessions keep a user on one server.

Problems:
- Breaks scaling
- Causes uneven load

Better approach:
- External session stores
- Stateless applications

Stickiness should be a last resort.

---

## High Availability Beyond Load Balancers

HA also includes:
- Multiple availability zones
- Redundant networking
- Failover mechanisms

Load balancer alone is not HA.

---

## Real-World Failure Patterns

Seen many times:

- Health check path wrong
- Firewall blocks health checks
- Backend listens on wrong port
- Load balancer protocol mismatch
- One AZ outage without redundancy

Apps look “partially down” — hardest to debug.

---

## How DevOps Engineers Debug LB Issues

Mentor checklist:

1. Does LB receive traffic?
2. Are backends healthy?
3. Is health check correct?
4. Is firewall allowing LB traffic?
5. Is protocol consistent end-to-end?

Never assume defaults.

---

## Cloud Reality (AWS Example)

In cloud:
- Load balancers are managed
- Scaling is automatic
- Misconfiguration is the main risk

Understanding concepts matters more than UI clicks.

---

## Key Takeaway

Load balancers don’t prevent failures.
They **absorb failures**.

If you design for failure:
- Systems stay alive
- Users stay happy
- Engineers sleep better

---

### End of Module 11
