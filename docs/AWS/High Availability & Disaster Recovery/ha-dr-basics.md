---
sidebar_position: 1
title: High Availability and Disaster Recovery Basics
---

# High Availability and Disaster Recovery (HA & DR) – Basics

Failures are inevitable.
What matters is **how your system behaves when failure happens**.

High Availability (HA) and Disaster Recovery (DR) are core pillars of **reliable cloud architecture**.

---

## What Is High Availability (HA)?

High Availability means:
- Systems remain available
- Even when components fail

HA focuses on:
- Minimizing downtime
- Automatic recovery
- Fault tolerance

Example:
- Application stays up even if one server fails

---

## What Is Disaster Recovery (DR)?

Disaster Recovery focuses on:
- Recovering from major failures
- Region-wide outages
- Data corruption incidents

DR answers:
> **How fast can we recover, and how much data can we afford to lose?**

---

## HA vs DR (Clear Difference)

| Aspect | High Availability | Disaster Recovery |
|-----|------------------|------------------|
| Scope | Local failures | Large-scale failures |
| Downtime | Seconds to minutes | Minutes to hours |
| Focus | Staying online | Recovering service |
| Example | Multi-AZ | Cross-region setup |

👉 HA handles **small failures**, DR handles **big failures**.

---

## Failure Domains in AWS

AWS designs for isolation using:
- Availability Zones (AZs)
- Regions

Understanding failure domains is critical for HA/DR design.

---

## Availability Zones (AZs)

An AZ is:
- One or more data centers
- Independent power, cooling, and networking

Best practice:
- Deploy across **multiple AZs**

---

## Regions

A region:
- Contains multiple AZs
- Is geographically isolated

Use regions for:
- Disaster recovery
- Compliance
- Latency optimization

---

## Fault Tolerance

Fault tolerance means:
- System continues operating
- Even when components fail

Achieved by:
- Redundancy
- Automatic failover

---

## Redundancy (Key Concept)

Redundancy means:
- Multiple copies of components

Examples:
- Multiple EC2 instances
- Multiple databases replicas

Redundancy is the **foundation of HA**.

---

## RTO and RPO (Must Know)

### RTO – Recovery Time Objective
- Maximum acceptable downtime

### RPO – Recovery Point Objective
- Maximum acceptable data loss

Lower RTO/RPO:
- Higher cost
- More complex architecture

---

## Common HA Patterns in AWS

- Load balancers across AZs
- Auto Scaling groups
- Managed multi-AZ databases

These patterns are **built-in** to many AWS services.

---

## Common DR Strategies

- Backup and restore
- Pilot light
- Warm standby
- Active-active

We’ll cover these **in detail next**.

---

## Common Beginner Mistakes

- Single-AZ deployments
- No backups
- Confusing HA with DR
- Never testing failover

These mistakes cause:
- Long outages

---

## Interview Tip

If asked:
> “How do you design highly available systems in AWS?”

Strong answer:
> By using multi-AZ architectures, redundancy, and managed services with automatic failover.

---

## Key Takeaways

- Failures are expected
- HA minimizes downtime
- DR enables recovery
- AZs and regions are core building blocks
- RTO and RPO guide design

---

📌 **Next:** Disaster Recovery Strategies in AWS
