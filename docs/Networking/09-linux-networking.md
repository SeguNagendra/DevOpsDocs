---
sidebar_position: 9
title: Linux Networking 
description: Learn Linux networking the way real DevOps engineers debug issues — calmly, logically, and step by step.
---

# Linux Networking (How Engineers Actually Debug)

## Mentor Truth

Linux networking commands are not something you memorize.

They are **questions you ask the system**.

If you know *what to ask*, Linux will always tell you the truth.

---

## How Engineers Think Before Running Commands

Before typing anything, pause and ask:

- What am I trying to verify?
- Where could traffic be breaking?
- What layer am I checking?

Commands without thinking lead to noise.
Thinking leads to clarity.

---

## Step 1: Check Network Identity

First, confirm:
> “Who am I on this network?”

### Useful Commands
- `ip a`
- `hostname -i`

You are checking:
- Does the machine have an IP?
- Is the interface up?
- Is it the expected subnet?

If there’s no IP, nothing else matters.

---

## Step 2: Check Routing

Next question:
> “Where does traffic go from here?”

### Useful Commands
- `ip r`
- `route -n`

You are checking:
- Default route exists
- Traffic knows where to exit

Missing or wrong route = traffic disappears silently.

---

## Step 3: Check Reachability

Now ask:
> “Can I reach the destination?”

### Useful Commands
- `ping`
- `traceroute`

Important reminder:
- Ping uses ICMP
- Ping success does not guarantee app success

Ping failure helps narrow the problem, not define it completely.

---

## Step 4: Check DNS Resolution

Very common failure point.

### Useful Commands
- `dig`
- `nslookup`
- `cat /etc/resolv.conf`

Questions you answer:
- Does the name resolve?
- Does it resolve to the correct IP?
- Which DNS server is used?

If DNS is wrong, everything above looks broken.

---

## Step 5: Check Listening Ports

Now verify:
> “Is the service actually listening?”

### Useful Commands
- `ss -lntp`
- `netstat -tulnp`
- `lsof -i`

You are checking:
- Correct port
- Correct protocol
- Correct interface (0.0.0.0 vs 127.0.0.1)

Many apps fail here.

---

## Step 6: Test the Connection

Don’t guess — test.

### Useful Commands
- `curl`
- `wget`
- `nc`
- `telnet`

These tell you:
- Can I connect?
- Do I get a response?
- Does it hang or fail fast?

Hanging usually means firewall or routing.

---

## Step 7: Inspect Firewall Rules

Linux itself may block traffic.

### Useful Commands
- `iptables -L`
- `nft list ruleset`
- `ufw status`

Even if cloud firewalls allow traffic,
local firewalls can still block it.

---

## Step 8: Packet-Level Debugging (When Needed)

When nothing makes sense, look at packets.

### Useful Command
- `tcpdump`

You are answering:
- Are packets arriving?
- Are responses leaving?
- Is traffic asymmetric?

This is advanced, but powerful.

---

## Common Real-World Debugging Flow

Mentor-style order:

1. IP & interface
2. Routing
3. DNS
4. Port listening
5. Firewall
6. Application

Skipping steps causes confusion.

---

## Common Beginner Mistake

Beginners:
> Run all commands at once

Mentors:
> Ask one question at a time

Calm debugging beats fast typing.

---

## Key Takeaway

Linux networking tools give you **visibility**.

They don’t fix problems.
They show you **where the problem is**.

Once you see clearly, fixing is easy.

---

### End of Module 09
