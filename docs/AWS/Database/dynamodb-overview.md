---
sidebar_position: 5
title: DynamoDB Overview
---

# Amazon DynamoDB – Overview

Not all applications fit well into relational databases.
When scale, performance, and availability matter more than complex joins,
👉 **Amazon DynamoDB is the go-to database in AWS**.

DynamoDB is designed for **massive scale with predictable performance**.

---

## What Is Amazon DynamoDB? (Simple Explanation)

Amazon DynamoDB is:
- A fully managed NoSQL database
- Key-value and document-based
- Serverless and highly scalable

In simple terms:
> **DynamoDB = fast, serverless NoSQL database at any scale**

---

## Why DynamoDB Exists

Relational databases struggle with:
- Massive scale
- High request rates
- Global low-latency access

DynamoDB exists to:
- Handle millions of requests per second
- Scale automatically
- Eliminate infrastructure management

👉 You don’t manage servers, storage, or replication.

---

## Core DynamoDB Concepts (Must Know)

### Table
- Collection of items

### Item
- A single record (like a row)

### Attribute
- A data field (like a column)

Unlike SQL:
- No fixed schema
- Each item can have different attributes

---

## Primary Key (Very Important)

Every DynamoDB table requires a primary key.

Two options:

### 1. Partition Key
- Determines data distribution
- Must be unique

### 2. Partition Key + Sort Key
- Partition key groups items
- Sort key orders items within a partition

👉 Primary key design is **critical for performance**.

---

## How DynamoDB Scales

DynamoDB:
- Automatically partitions data
- Distributes load across partitions
- Scales horizontally

You don’t:
- Add nodes
- Manage sharding

Scaling is **transparent and automatic**.

---

## Consistency Models

DynamoDB supports:

### Eventually Consistent Reads
- Faster
- Default
- Slightly stale data possible

### Strongly Consistent Reads
- Always up to date
- Slightly higher latency

👉 Choose based on application needs.

---

## Read and Write Capacity

DynamoDB supports two capacity modes:

### Provisioned Capacity
- You define read/write capacity
- Predictable workloads

### On-Demand Capacity
- Pay per request
- Spiky or unpredictable workloads

👉 On-demand is simpler for most teams.

---

## DynamoDB vs RDS (High Level)

| Feature | DynamoDB | RDS |
|------|----------|-----|
| Schema | Flexible | Fixed |
| Scaling | Automatic | Manual |
| Joins | No | Yes |
| Performance | Millisecond | Variable |
| Use case | Massive scale | Transactions |

Choose based on **access patterns**, not preference.

---

## Common DynamoDB Use Cases

- User sessions
- Shopping carts
- Gaming leaderboards
- IoT data
- Event metadata

DynamoDB excels at:
- High throughput
- Low latency

---

## Common Beginner Mistakes

- Poor primary key design
- Treating DynamoDB like SQL
- Using scans instead of queries
- Ignoring access patterns

These mistakes cause:
- Hot partitions
- High cost
- Poor performance

---

## Interview Tip

If asked:
> “When would you use DynamoDB?”

Strong answer:
> When you need a highly scalable, low-latency NoSQL database with predictable performance and minimal operational overhead.

---

## Key Takeaways

- DynamoDB is a serverless NoSQL database
- Designed for massive scale
- Primary key design is critical
- Offers flexible consistency models
- Ideal for high-throughput workloads

---

📌 **Next:** DynamoDB Data Modeling and Keys
