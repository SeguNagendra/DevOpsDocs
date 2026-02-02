---
sidebar_position: 2
title: Amazon RDS Overview
---

# Amazon RDS – Overview

Relational databases are still the **default choice** for most applications.
AWS makes them easier to run using **Amazon RDS (Relational Database Service)**.

RDS removes most of the **operational pain** while keeping the power of SQL databases.

---

## What Is Amazon RDS? (Simple Explanation)

Amazon RDS is a **managed relational database service** that:
- Runs common SQL engines
- Handles backups, patching, and maintenance
- Provides high availability options

In simple terms:
> **RDS = managed SQL databases on AWS**

---

## Why Amazon RDS Exists

Running databases yourself means:
- OS patching
- Backups
- Monitoring
- Failover planning

RDS exists to:
- Reduce operational overhead
- Improve reliability
- Let teams focus on applications

👉 You manage **data and schema**, AWS manages **infrastructure**.

---

## Supported Database Engines

Amazon RDS supports:

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server

👉 Engine choice depends on **application needs and licensing**.

---

## RDS Architecture (High Level)

An RDS setup includes:
- DB instance (compute + memory)
- Storage (EBS-backed)
- Network (VPC, subnets, security groups)

You access RDS using:
- Endpoint (DNS name)
- Standard database clients

---

## Single-AZ vs Multi-AZ

### Single-AZ
- One database instance
- Lower cost
- Suitable for dev/test

### Multi-AZ (Very Important)
- Synchronous standby replica
- Automatic failover
- High availability

👉 Multi-AZ is **for availability**, not scaling.

---

## Read Replicas (Scaling Reads)

Read replicas:
- Asynchronous copies
- Used for read scaling
- Reduce load on primary DB

Supported for:
- MySQL
- PostgreSQL
- MariaDB

👉 Read replicas are **not for failover**.

---

## Backups and Snapshots

### Automated Backups
- Enabled by default
- Point-in-time recovery
- Retention configurable

### Manual Snapshots
- User-triggered
- Persist until deleted

👉 Backups are **non-negotiable**.

---

## Storage Types

RDS offers:
- General Purpose SSD (gp)
- Provisioned IOPS (io)

Choose based on:
- Performance needs
- Cost considerations

---

## Security in RDS

RDS security includes:
- VPC isolation
- Security groups
- Encryption at rest (KMS)
- Encryption in transit (SSL)

IAM controls:
- Who can manage RDS
- Not database users

---

## Maintenance and Patching

AWS handles:
- OS patching
- Database engine updates (configurable window)

You control:
- Maintenance window
- Upgrade timing

---

## Common RDS Use Cases

- Web application databases
- ERP systems
- CMS platforms
- Transactional workloads

RDS is ideal for:
- Structured data
- ACID compliance

---

## Common Beginner Mistakes

- Using Single-AZ in production
- Confusing Multi-AZ with read replicas
- No monitoring or alarms
- Underestimating storage growth

These mistakes cause:
- Downtime
- Performance issues

---

## Interview Tip

If asked:
> “What is Amazon RDS?”

Strong answer:
> Amazon RDS is a managed relational database service that supports multiple SQL engines and handles backups, patching, and high availability.

---

## Key Takeaways

- RDS is a managed SQL database service
- Supports multiple engines
- Multi-AZ provides high availability
- Read replicas provide read scaling
- Ideal for transactional workloads

---

📌 **Next:** RDS High Availability and Scaling
