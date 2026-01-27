---
sidebar_position: 2
title: CIDR and Subnets
---

# CIDR and Subnets

CIDR and subnets are the **most confusing part of AWS networking** for many learners.
Once you understand this topic properly, **VPC networking becomes much easier**.

This page explains CIDR and subnets in a **clear, human-friendly way**, without unnecessary math.

---

## Why CIDR and Subnets Matter

CIDR and subnetting define:
- How many IP addresses you have
- How resources are grouped
- How traffic flows inside a VPC

Bad CIDR planning leads to:
- IP exhaustion
- Re-architecture
- Production issues

👉 This is why **architects plan CIDR carefully**.

---

## What Is CIDR? (Simple Explanation)

CIDR (Classless Inter-Domain Routing) defines a **range of IP addresses**.

Example:
```
10.0.0.0/16
```

This means:
- Network range starts at `10.0.0.0`
- `/16` defines how many IPs are available

You don’t need to memorize formulas — just understand **size meaning**.

---

## Common CIDR Sizes (Practical View)

| CIDR | Approx IPs | Use Case |
|----|-----------|---------|
| /16 | ~65,000 | Large VPC |
| /20 | ~4,000 | Medium subnet |
| /24 | 256 | Small subnet |
| /28 | 16 | Special cases |

👉 `/16` for VPC, `/24` for subnets is very common.

---

## What Is a Subnet?

A subnet is:
- A smaller IP range carved out of a VPC
- Always tied to **one Availability Zone**

Subnets help you:
- Organize resources
- Control routing
- Achieve high availability

---

## Public vs Private Subnets (Very Important)

### Public Subnet
A subnet is **public** if:
- Its route table has a route to an Internet Gateway

Used for:
- Load balancers
- Bastion hosts
- Public-facing services

---

### Private Subnet
A subnet is **private** if:
- It does NOT have a route to an Internet Gateway

Used for:
- Application servers
- Databases
- Internal services

👉 **Most workloads should live in private subnets**.

---

## Example VPC Design (Common Pattern)

VPC CIDR:
```
10.0.0.0/16
```

Subnets:
- Public Subnet AZ-A → `10.0.1.0/24`
- Public Subnet AZ-B → `10.0.2.0/24`
- Private Subnet AZ-A → `10.0.11.0/24`
- Private Subnet AZ-B → `10.0.12.0/24`

This design provides:
- High availability
- Clear separation
- Secure architecture

---

## Reserved IP Addresses (AWS-Specific)

In every subnet, AWS reserves **5 IP addresses**:
- Network address
- VPC router
- DNS
- Future use
- Broadcast (not used, but reserved)

👉 Don’t expect all 256 IPs in a `/24` subnet.

---

## Common Beginner Mistakes

- Creating very small subnets
- Mixing public and private resources
- Forgetting AWS reserved IPs
- Poor AZ planning

These mistakes cause:
- Scaling limits
- Security issues

---

## Interview Tip

If asked:
> “How do you design subnets in a VPC?”

Strong answer:
> By choosing a large enough CIDR for the VPC and creating public and private subnets across multiple AZs for high availability.

That shows **architect-level thinking**.

---

## Key Takeaways

- CIDR defines IP range size
- Subnets divide VPC logically
- Public vs private is defined by routing
- AZ-based subnets enable HA
- Planning early avoids rework

---

📌 **Next:** Route Tables
