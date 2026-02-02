---
sidebar_position: 3
title: RDS High Availability and Scaling
---

# RDS High Availability and Scaling

Databases are **stateful systems**.
When they fail, applications usually fail with them.

Amazon RDS provides built-in features to handle:
- High availability (HA)
- Failures
- Read scaling

Understanding these correctly is **critical for production systems**.

---

## Why High Availability Matters for Databases

Without HA:
- Database failure = application downtime
- Manual recovery takes time
- Data loss risk increases

HA ensures:
- Minimal downtime
- Automatic recovery
- Business continuity

👉 HA is about **availability**, not performance.

---

## RDS Multi-AZ (High Availability)

### What Is Multi-AZ?

Multi-AZ:
- Creates a primary DB instance
- Maintains a synchronous standby in another AZ
- Automatically fails over when needed

In simple terms:
> **Multi-AZ = standby database for failover**

---

## How Multi-AZ Works

High-level flow:
1. Application writes to primary DB
2. Data is synchronously replicated to standby
3. If primary fails → AWS promotes standby
4. Endpoint remains the same

👉 Failover is automatic and transparent.

---

## When to Use Multi-AZ

Use Multi-AZ for:
- Production databases
- Mission-critical workloads
- Applications requiring high uptime

Avoid Multi-AZ for:
- Dev/test environments
- Cost-sensitive non-critical systems

---

## What Multi-AZ Does NOT Do

Important clarifications:
- ❌ Does NOT improve read performance
- ❌ Does NOT provide read scaling
- ❌ Standby is NOT accessible

👉 Multi-AZ is **only for availability**.

---

## RDS Read Replicas (Read Scaling)

### What Is a Read Replica?

Read replicas:
- Are asynchronous copies of primary DB
- Used to handle read-heavy workloads

In simple terms:
> **Read replicas = scale reads, not writes**

---

## How Read Replicas Work

- Primary DB handles writes
- Replicas serve read queries
- Replication is asynchronous

Used for:
- Analytics
- Reporting
- Read-heavy APIs

---

## When to Use Read Replicas

Use read replicas when:
- Read traffic is high
- Primary DB CPU is saturated
- Analytics queries impact performance

👉 Read replicas improve **performance**, not availability.

---

## Read Replicas vs Multi-AZ (Must Know)

| Feature | Multi-AZ | Read Replica |
|------|---------|--------------|
| Purpose | Availability | Read scaling |
| Replication | Synchronous | Asynchronous |
| Failover | Automatic | Manual |
| Read access | No | Yes |
| Cost | Higher | Lower |

👉 They solve **different problems**.

---

## Combining Multi-AZ and Read Replicas

Best practice for production:
- Enable Multi-AZ for HA
- Add read replicas for scaling

This provides:
- High availability
- High performance

---

## Failover Behavior (Important)

During failover:
- Endpoint DNS remains same
- Short downtime (seconds to minutes)
- Connections are reset

Applications must:
- Handle reconnects gracefully

---

## Scaling RDS Instances

### Vertical Scaling
- Change instance type
- Requires downtime (usually)

### Storage Scaling
- Increase storage size
- Often done online

Plan scaling:
- Before limits are reached

---

## Monitoring RDS Availability and Performance

Monitor using:
- CloudWatch metrics (CPU, connections, latency)
- Alarms on critical thresholds

Monitoring helps:
- Predict failures
- Plan scaling

---

## Common Beginner Mistakes

- Thinking Multi-AZ improves performance
- Using read replicas for HA
- No retry logic in applications
- No alarms on DB metrics

These mistakes cause:
- Downtime
- Poor performance

---

## Interview Tip

If asked:
> “How do you design a highly available RDS database?”

Strong answer:
> By enabling Multi-AZ for high availability and using read replicas for read scaling if needed.

This shows **production-grade database understanding**.

---

## Key Takeaways

- Multi-AZ provides high availability
- Read replicas provide read scaling
- They solve different problems
- Use both in production when required
- Monitoring and retries are essential

---

📌 **Next:** Amazon Aurora
