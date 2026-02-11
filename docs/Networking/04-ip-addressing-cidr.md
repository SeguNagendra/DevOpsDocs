---
sidebar_position: 4
title: IP Addressing & CIDR
description: Understand IP addresses and CIDR the calm, practical way — enough to design, debug, and explain real systems.
---

# IP Addressing & CIDR (No Math Panic)

## Mentor Note Before We Start

Most people fear IP addressing because they think:
> “This is math-heavy.”

It isn’t.

For DevOps engineers, IP addressing is about **identity and boundaries**, not calculations.
If you understand *who can talk to whom*, you already understand 80% of this topic.

---

## What an IP Address Really Is

An IP address is simply:
> “The identity of a machine on a network.”

Just like two people can’t share the same phone number,
two machines on the same network can’t share the same IP.

Example:
```
192.168.1.10
```

This uniquely identifies one machine **inside a network**.

---

## IPv4 vs IPv6 (Practical View)

### IPv4
- Most commonly used
- Looks like: `192.168.1.10`
- Limited number of addresses

### IPv6
- Created because IPv4 ran out
- Looks long and scary
- Mostly hidden behind cloud services

**Mentor truth:**  
You’ll *see* IPv6, but you’ll mostly *work* with IPv4.

---

## Public IP vs Private IP (Very Important)

This is one of the most important networking concepts.

### Public IP
- Reachable from the internet
- Used by websites, load balancers
- Must be protected

### Private IP
- Used inside internal networks
- Not reachable from internet directly
- Used by databases, internal services

Example private ranges:
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

If you expose private services publicly, you create security risks.

---

## Static IP vs Dynamic IP

### Static IP
- Never changes
- Used for servers, gateways, DNS records

### Dynamic IP
- Assigned automatically
- Can change
- Used by laptops, pods, temporary workloads

Cloud heavily relies on **dynamic IPs**.

---

## What Is a Subnet (Human Explanation)

A subnet is just:
> “A smaller network inside a bigger network.”

Why do we do this?
- Security isolation
- Traffic control
- Clean architecture

You don’t put databases and web servers in the same open area.
Subnets help you separate them logically.

---

## CIDR Notation (The Calm Explanation)

CIDR looks like this:
```
10.0.0.0/16
```

The part after `/` answers one question:
> “How big is this network?”

You don’t need to memorize address counts.

Just remember common patterns:
- `/32` → single machine
- `/24` → small subnet
- `/16` → large subnet

That’s enough for DevOps work.

---

## Why CIDR Matters in Cloud

Cloud platforms ask:
- VPC CIDR
- Subnet CIDR
- Pod CIDR
- Service CIDR

CIDR defines **how much space you have to grow**.

Bad CIDR planning = painful migrations later.

---

## Real-World Failure Example

Common mistake:
- Overlapping CIDR ranges
- VPC peering fails
- VPN doesn’t work

Everything looks fine — until traffic starts flowing.

CIDR planning prevents future outages.

---

## How DevOps Engineers Use This Daily

You’ll use IP concepts when:
- Designing VPCs
- Creating subnets
- Debugging connectivity issues
- Reading Kubernetes configs
- Reviewing security rules

You won’t calculate — you’ll **reason**.

---

## Mentor Rule to Remember

Never ask:
> “What is the formula?”

Always ask:
> “Who needs to talk to whom, and should they?”

That question solves most IP problems.

---

## Key Takeaway

IP addressing is not scary.
CIDR is not magic.

They are tools to:
- Identify machines
- Draw boundaries
- Keep systems safe and scalable

Understand the intent, and the rest follows naturally.

