---
sidebar_position: 5
title: Amazon EBS (Elastic Block Store)
---

# Amazon EBS (Elastic Block Store)

Amazon EBS provides **block-level storage** for EC2 instances.
If S3 is object storage,
👉 **EBS is like a hard disk attached to a server**.

EBS is used when applications need:
- Low-latency access
- File-system level storage
- Persistent data attached to EC2

---

## What Is Amazon EBS? (Simple Explanation)

Amazon EBS is a **managed block storage service** that:
- Attaches to EC2 instances
- Persists data independently of the instance lifecycle
- Scales in size and performance

In simple terms:
> **EBS = virtual hard drive for EC2**

---

## Why EBS Exists

Without EBS:
- EC2 data would be lost on termination
- Storage performance would be inconsistent
- Databases would be unreliable

EBS solves this by:
- Separating compute and storage
- Providing consistent performance
- Enabling backups via snapshots

---

## Core EBS Concepts

### Volume
- A block storage device
- Created in a specific AZ
- Attached to one EC2 instance at a time (most cases)

### Snapshot
- Point-in-time backup of an EBS volume
- Stored in S3 (managed by AWS)
- Used for backup and recovery

---

## Types of EBS Volumes (Important)

AWS offers different EBS volume types based on performance needs.

---

## ⚡ SSD-backed Volumes

### gp3 / gp2 (General Purpose SSD)
- Balanced performance and cost
- Used for most workloads

### io1 / io2 (Provisioned IOPS SSD)
- High, consistent IOPS
- Used for databases and critical workloads

---

## 💾 HDD-backed Volumes

### st1 (Throughput Optimized HDD)
- Large, sequential workloads
- Big data, log processing

### sc1 (Cold HDD)
- Infrequently accessed data
- Lowest cost EBS option

---

## Choosing the Right EBS Volume

Ask:
1. Is my workload IOPS-intensive?
2. Is it throughput-heavy?
3. Is cost a concern?
4. Is this production or dev/test?

👉 Most workloads start with **gp3**.

---

## EBS Availability & AZ Limitation

Important rule:
- EBS volumes live in **one Availability Zone**
- Cannot be attached across AZs

To move data across AZs:
- Create snapshot
- Restore in another AZ

---

## EBS Snapshots (Very Important)

Snapshots:
- Are incremental
- Only store changed blocks
- Enable backups and disaster recovery

Common use cases:
- Backup before upgrades
- Cloning environments
- Disaster recovery

---

## EBS vs Instance Store (Common Confusion)

| Feature | EBS | Instance Store |
|------|----|----------------|
| Persistence | Yes | No |
| Backup | Snapshots | No |
| Use case | Databases, OS | Temporary data |
| AZ bound | Yes | Yes |

👉 Instance store data is **lost on stop/terminate**.

---

## Common Mistakes

- Using HDD volumes for databases
- Forgetting to snapshot volumes
- Over-provisioning IOPS unnecessarily
- Ignoring AZ constraints

These mistakes cause:
- Poor performance
- Data loss
- Higher costs

---

## Interview Tip

If asked:
> “What storage do you use for EC2 databases?”

Strong answer:
> Amazon EBS with SSD-backed volumes and regular snapshots.

That shows **practical AWS knowledge**.

---

## Key Takeaways

- EBS is block storage for EC2
- Persistent and reliable
- Multiple volume types for different workloads
- Snapshots are critical
- Core service for stateful workloads

---

📌 **Next:** Amazon EFS (Elastic File System)
