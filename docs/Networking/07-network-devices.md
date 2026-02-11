---
sidebar_position: 7
title: Network Devices 
description: Understand core network devices the way DevOps engineers actually use them — logically, not physically.
---

# Network Devices (Cloud-Mapped, No Hardware Pain)

## Mentor Perspective

You do **not** need to become a hardware engineer to understand networking.

As a DevOps engineer, your job is to understand:
- What role a device plays
- How traffic flows through it
- What happens when it’s misconfigured

Cloud turns physical boxes into **managed services**, but the logic stays the same.

---

## The Big Picture

Think of network devices as **traffic managers**.

Each one answers a simple question:
- Where should traffic go?
- Should traffic be allowed?
- How should traffic be distributed?

If you understand those answers, you understand the device.

---

## Switch (Layer 2)

### What a Switch Does
A switch connects machines **inside the same network**.

- It does not think about IPs
- It forwards traffic based on MAC addresses

### DevOps Reality
In cloud:
- Switches are abstracted away
- You rarely configure them directly

If a VM is attached to a subnet, the switch part already works.

---

## Router (Layer 3)

### What a Router Does
A router connects **different networks**.

It decides:
> “This traffic belongs there.”

Routers understand IP addresses and routing tables.

### DevOps Reality
In cloud:
- Routing is controlled by **route tables**
- You define where traffic should go

Wrong route = traffic disappears silently.

---

## Firewall

### What a Firewall Does
A firewall decides:
> “Is this traffic allowed or denied?”

It checks:
- Source
- Destination
- Port
- Protocol

Firewalls don’t care if your app is correct.

---

### Stateful vs Stateless (Simple View)

- **Stateful**: remembers previous traffic (Security Groups)
- **Stateless**: checks every packet independently (NACLs)

Both exist in cloud, both matter.

---

## Load Balancer

### What a Load Balancer Does
A load balancer:
- Distributes traffic
- Removes unhealthy servers
- Hides failures from users

Users never talk to servers directly.

### DevOps Reality
In cloud:
- Load balancers are managed
- Misconfiguration causes random failures

If traffic feels inconsistent, check the load balancer.

---

## Gateway

### What a Gateway Does
A gateway connects your network to:
- Internet
- Other networks
- External services

Without a gateway, traffic has nowhere to exit.

---

## NAT (Network Address Translation)

### Why NAT Exists
Private IPs cannot talk to the internet directly.

NAT:
- Translates private IP → public IP
- Allows outbound access
- Blocks inbound access

This is how private subnets reach updates and APIs.

---

## Physical vs Cloud Mapping (Very Important)

| Physical Concept | Cloud Equivalent |
|-----------------|------------------|
| Switch | Subnet networking |
| Router | Route table |
| Firewall | Security Group / NACL |
| Load Balancer | ALB / NLB |
| Gateway | Internet / NAT Gateway |

Cloud changes names, not logic.

---

## Common Real-World Failures

I’ve seen these many times:

- Route table missing entry
- Firewall allows inbound but blocks outbound
- Load balancer health check wrong
- NAT missing for private subnet

Everything looks healthy — traffic still fails.

---

## Mentor Debugging Tip

When traffic fails, ask:
1. Which device handles this traffic?
2. What decision does it make?
3. Is that decision correct?

Devices don’t fail randomly.
They fail because rules are wrong.

---

## Key Takeaway

Network devices are not scary.
They are **decision points**.

If you understand what decision each device makes,
you can debug even complex cloud architectures calmly.
