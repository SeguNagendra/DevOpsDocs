---
sidebar_position: 4
title: Amazon Aurora
---

# Amazon Aurora

Amazon Aurora is AWS’s **cloud-native relational database**.
It is designed to provide:
- Higher performance
- Better availability
- Faster recovery

Aurora looks like a traditional SQL database,
👉 but internally it is **very different from RDS**.

---

## What Is Amazon Aurora? (Simple Explanation)

Amazon Aurora is:
- A MySQL- and PostgreSQL-compatible database
- Built specifically for the cloud
- Fully managed by AWS

In simple terms:
> **Aurora = high-performance, cloud-optimized SQL database**

---

## Why Aurora Exists

Traditional RDS databases:
- Use EBS storage
- Replicate data at the instance level
- Have slower failover

Aurora was built to:
- Separate compute and storage
- Replicate data at the storage layer
- Improve availability and recovery

👉 Aurora is designed for **cloud scale and resilience**.

---

## Aurora Architecture (High Level)

Aurora architecture includes:
- One or more DB instances (compute)
- A shared distributed storage layer

Storage characteristics:
- Automatically scales
- Replicated across 6 copies
- Spread across 3 Availability Zones

👉 Storage is **fault-tolerant by design**.

---

## Read and Write Model

Aurora has:
- One primary writer instance
- Multiple reader instances

Reads:
- Served by reader replicas

Writes:
- Handled only by the writer

This allows:
- High read scalability
- Fast failover

---

## Aurora Replicas (Important)

Aurora supports:
- Up to 15 read replicas
- Very fast replication

Failover:
- One replica is promoted automatically
- Takes seconds

👉 Faster than traditional RDS Multi-AZ.

---

## Aurora Endpoints

Aurora provides multiple endpoints:

- Writer endpoint → write operations
- Reader endpoint → load-balanced reads
- Instance endpoint → specific instance

Endpoints simplify:
- Application configuration
- Scaling

---

## Aurora Storage Scaling

Aurora storage:
- Starts small
- Automatically grows (up to 128 TB)
- No manual resizing

👉 Storage scaling is **automatic and online**.

---

## Aurora vs RDS (Must Know)

| Feature | Aurora | RDS |
|------|--------|-----|
| Performance | Higher | Standard |
| Storage | Distributed | EBS |
| Replication | Storage-level | Instance-level |
| Failover | Very fast | Slower |
| Cost | Higher | Lower |

👉 Choose based on **performance and availability needs**.

---

## Aurora Use Cases

Aurora is ideal for:
- High-traffic web applications
- SaaS platforms
- Microservices architectures
- Mission-critical workloads

Use Aurora when:
- Performance matters
- Downtime must be minimal

---

## Aurora Serverless (Brief Intro)

Aurora Serverless:
- Auto-scales compute
- No fixed instance size
- Pay-per-use model

Best for:
- Spiky workloads
- Infrequent usage

---

## Common Beginner Mistakes

- Using Aurora unnecessarily for small apps
- Ignoring cost implications
- Confusing Aurora replicas with RDS read replicas
- Overengineering early

Aurora is powerful, but **not always required**.

---

## Interview Tip

If asked:
> “Why would you choose Aurora over RDS?”

Strong answer:
> Because Aurora offers higher performance, faster failover, and better availability due to its distributed storage architecture.

---

## Key Takeaways

- Aurora is a cloud-native SQL database
- Storage is distributed and highly available
- Faster failover than RDS
- Supports massive read scaling
- Best for high-performance workloads

---

📌 **Next:** DynamoDB Overview
