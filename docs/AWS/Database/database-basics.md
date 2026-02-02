---
sidebar_position: 1
title: Database Basics
---

# Database Basics

Every application needs a place to **store and retrieve data**.
Databases are the backbone of **almost every system** you build in AWS.

Before jumping into RDS, DynamoDB, or Aurora,
👉 you must understand **database fundamentals** clearly.

---

## What Is a Database? (Simple Explanation)

A database is:
- An organized collection of data
- Stored electronically
- Designed for fast read and write operations

In simple terms:
> **Database = structured data storage with efficient access**

---

## Why Databases Exist

Without databases:
- Data would be stored in files
- Searching would be slow
- Concurrency would break systems

Databases exist to:
- Store data reliably
- Support concurrent users
- Ensure consistency and durability

---

## Core Database Concepts (Must Know)

### Data
- Information stored (users, orders, logs)

### Schema
- Structure of the data
- Tables, columns, types

### Query
- Request to read or modify data

### Index
- Improves query performance

---

## Types of Databases

Databases are broadly classified into:

1. Relational Databases (SQL)
2. Non-Relational Databases (NoSQL)

Each solves **different problems**.

---

## Relational Databases (SQL)

Characteristics:
- Table-based structure
- Fixed schema
- ACID transactions
- Strong consistency

Examples:
- MySQL
- PostgreSQL
- Oracle

Best for:
- Transactions
- Structured data
- Complex queries

---

## ACID Properties (Very Important)

Relational databases follow ACID:

- **Atomicity** → All or nothing
- **Consistency** → Valid state always
- **Isolation** → Concurrent safety
- **Durability** → Data survives failures

👉 ACID is critical for financial systems.

---

## Non-Relational Databases (NoSQL)

Characteristics:
- Flexible schema
- Horizontally scalable
- High performance

Types:
- Key-value
- Document
- Column
- Graph

Best for:
- Massive scale
- Variable data
- Low latency

---

## CAP Theorem (Basic Understanding)

CAP theorem states:
- Consistency
- Availability
- Partition tolerance

A distributed system can fully guarantee **only two**.

This influences:
- Database choice
- Architecture design

---

## OLTP vs OLAP

### OLTP (Online Transaction Processing)
- Many small transactions
- User-facing applications

### OLAP (Online Analytical Processing)
- Large read-heavy queries
- Reporting and analytics

Different workloads → different databases.

---

## Scaling Databases

Two common approaches:

### Vertical Scaling
- Bigger instance
- Limited scalability

### Horizontal Scaling
- Add more nodes
- Requires distributed design

Cloud databases favor **horizontal scaling**.

---

## AWS and Databases

AWS provides:
- Managed relational databases (RDS, Aurora)
- NoSQL databases (DynamoDB)
- Specialized databases (Redshift, Neptune)

👉 You rarely manage database servers directly.

---

## Common Beginner Mistakes

- Using relational DB for everything
- Ignoring scaling needs
- No backups
- No monitoring

These mistakes cause:
- Performance issues
- Data loss

---

## Interview Tip

If asked:
> “How do you choose a database?”

Strong answer:
> Based on data structure, consistency requirements, scalability, and access patterns.

---

## Key Takeaways

- Databases store and manage data
- SQL and NoSQL solve different problems
- ACID and CAP influence design
- Workload matters more than technology
- AWS offers fully managed databases

---

📌 **Next:** Relational Databases Overview (RDS)
