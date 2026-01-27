---
sidebar_position: 6
title: Amazon EFS (Elastic File System)
---

# Amazon EFS (Elastic File System)

Amazon EFS provides **shared file storage** for AWS workloads.
If EBS is a hard disk attached to one server,
👉 **EFS is a shared network file system that many servers can use at the same time**.

EFS is designed for applications that need:
- Shared access
- High availability
- Automatic scaling

---

## What Is Amazon EFS? (Simple Explanation)

Amazon EFS is a **managed file storage service** that:
- Uses the NFS protocol
- Can be mounted on multiple EC2 instances
- Automatically scales storage up and down

In simple terms:
> **EFS = shared file system in AWS**

---

## Why EFS Exists

Without EFS:
- Sharing files between EC2 instances is complex
- Manual NFS setup is error-prone
- Scaling shared storage is difficult

EFS solves this by:
- Being fully managed
- Scaling automatically
- Providing built-in high availability

👉 EFS removes operational complexity for shared storage.

---

## Core EFS Concepts

### File System
- The main storage resource
- Automatically replicated across AZs
- No need to manage capacity

### Mount Targets
- Network endpoints in each AZ
- EC2 instances connect via mount targets
- Required for access

---

## How EFS Achieves High Availability

EFS:
- Replicates data across multiple AZs
- Survives AZ failures
- Is accessible from any AZ in the VPC

👉 This makes EFS **highly available by default**.

---

## EFS Performance Modes

### General Purpose
- Low latency
- Suitable for most workloads

### Max I/O
- Higher throughput
- Slightly higher latency

👉 Most workloads should use **General Purpose**.

---

## EFS Throughput Modes

### Bursting
- Throughput scales with storage size
- Default option

### Provisioned
- Fixed throughput regardless of size
- Used for predictable workloads

---

## Common EFS Use Cases

- Shared application files
- Content management systems
- Home directories
- Container shared storage
- Media processing

EFS is commonly used with:
- Auto Scaling Groups
- ECS / EKS
- Multi-AZ applications

---

## EFS vs EBS vs S3 (Quick Comparison)

| Feature | EFS | EBS | S3 |
|------|----|----|----|
| Storage type | File | Block | Object |
| Multi-instance access | Yes | No | Yes (API) |
| AZ scope | Multi-AZ | Single AZ | Multi-AZ |
| Use case | Shared files | Databases | Object data |

---

## Security in EFS

EFS security includes:
- IAM access control
- Security Groups
- Encryption at rest and in transit

Always:
- Restrict access using Security Groups
- Enable encryption

---

## Common Mistakes

- Using EFS for databases
- Ignoring performance mode selection
- Exposing mount targets publicly

These mistakes lead to:
- Poor performance
- Security risks

---

## Interview Tip

If asked:
> “How do multiple EC2 instances share files?”

Strong answer:
> By using Amazon EFS, which provides a shared file system accessible across multiple AZs.

That answer shows **clear AWS storage understanding**.

---

## Key Takeaways

- EFS is shared file storage
- Multi-AZ and highly available
- Scales automatically
- Ideal for shared workloads
- Not a replacement for EBS or S3

---

📌 **Next:** Amazon FSx
