---
sidebar_position: 6
title: Ports & Sockets
description: Understand ports and sockets the practical way — so you can explain why apps look healthy but still fail.
---

# Ports & Sockets (Why Apps Are Running but Not Reachable)

## Mentor Reality Check

One of the most common things you’ll hear is:

> “The application is running, but it’s not accessible.”

Nine out of ten times, this is **not a code issue**.
It’s a **ports or sockets issue**.

Understanding this topic will save you from endless confusion.

---

## First: What a Port Really Is

A port is simply:
> “A door on a machine.”

- The machine is identified by an IP address
- The service is identified by a port

Example:
```
10.0.1.5:80   → Web service
10.0.1.5:22   → SSH
10.0.1.5:5432 → Database
```

Same machine, different services, different doors.

---

## Why Ports Exist at All

Imagine a server without ports.
It wouldn’t know which application should receive the traffic.

Ports allow:
- One machine
- To run many services
- At the same time

Ports keep things organized.

---

## Well-Known Ports (You Should Recognize These)

You don’t need to memorize all ports.
Just recognize the common ones:

- 22  → SSH
- 80  → HTTP
- 443 → HTTPS
- 3306 → MySQL
- 5432 → PostgreSQL
- 6379 → Redis

Seeing these in configs should feel familiar.

---

## What Is a Socket (Simple Explanation)

A socket is:
> “An active connection between two endpoints.”

It combines:
- IP address
- Port
- Protocol

Until a socket exists, communication does not exist.

---

## Why Apps Can Be Running but Not Reachable

This is where things usually break.

Common reasons:
- App listens on wrong port
- App listens on localhost only
- Firewall blocks the port
- Load balancer points to wrong port
- Security group missing rule

The app is healthy — traffic just can’t reach it.

---

## Listening vs Connected (Important Difference)

- **Listening port** → App is waiting for connections
- **Connected socket** → Active communication

You must have:
- A listening port
- And allowed traffic

One without the other is useless.

---

## TCP vs UDP (Port Behavior Difference)

### TCP
- Reliable
- Connection-based
- Most apps use this

### UDP
- Fast
- No connection guarantee
- Used for DNS, streaming

If protocol mismatches, traffic fails silently.

---

## Ephemeral Ports (Hidden but Important)

Clients also use ports.
They are called **ephemeral ports**.

If outbound traffic is blocked:
- Requests go out
- Responses never return
- App times out

This causes very confusing bugs.

---

## How DevOps Engineers Debug Port Issues

Mentor checklist:

1. Is app running?
2. Is it listening on expected port?
3. Is it bound to correct interface?
4. Is firewall allowing traffic?
5. Is load balancer targeting right port?

Always verify, never assume.

---

## Tools You’ll Use Often

- `ss -lntp`
- `netstat -tulnp`
- `lsof -i`
- `curl`
- `telnet` / `nc`

These tools answer:
> “Is something actually listening?”

---

## Common Beginner Mistake

Beginners say:
> “Service is up, I restarted it.”

Mentors ask:
> “Which port is it listening on?”

That question changes everything.

---

## Key Takeaway

Ports and sockets decide **reachability**.

Apps don’t fail loudly when ports are wrong.
They fail quietly.

If you understand ports well, you’ll debug faster than most engineers.
