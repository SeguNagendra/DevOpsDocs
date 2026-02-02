---
sidebar_position: 10
title: Database Summary and Comparison
---

# Database Summary and Comparison

This page is a **decision-focused summary** of AWS databases.
It helps you answer one critical question quickly:

> **Which database should I use, and why?**

This is useful for:
- Architecture design
- Interviews
- Quick revision
- Real-world decision making

---

## SQL vs NoSQL (High-Level)

### SQL (Relational Databases)
- Fixed schema
- ACID transactions
- Strong consistency
- Complex queries and joins

Examples:
- RDS (MySQL, PostgreSQL)
- Aurora

Best for:
- Transactional systems
- Financial applications
- Structured data

---

### NoSQL (Non-Relational Databases)
- Flexible schema
- Horizontal scaling
- High availability
- Simple query patterns

Examples:
- DynamoDB

Best for:
- Massive scale
- Low-latency workloads
- Event-driven systems

---

## RDS vs Aurora vs DynamoDB

| Feature | RDS | Aurora | DynamoDB |
|------|-----|--------|----------|
| Database type | SQL | SQL | NoSQL |
| Schema | Fixed | Fixed | Flexible |
| Scaling | Vertical + replicas | Massive read scaling | Automatic |
| Availability | Multi-AZ | Built-in multi-AZ | Built-in |
| Performance | Standard | High | Very high |
| Operations | Managed | Highly managed | Serverless |
| Cost | Lower | Higher | Usage-based |
| Use case | Traditional apps | High-scale SQL | Internet-scale apps |

---

## When to Choose RDS

Choose RDS when:
- You need a traditional SQL database
- ACID transactions are required
- Schema is well-defined
- Moderate scale is sufficient

Examples:
- CMS platforms
- ERP systems
- Internal business apps

---

## When to Choose Aurora

Choose Aurora when:
- You need high performance SQL
- Fast failover is critical
- Read scaling is required
- You want cloud-native SQL

Examples:
- SaaS platforms
- High-traffic web apps
- Mission-critical systems

---

## When to Choose DynamoDB

Choose DynamoDB when:
- You need massive scale
- Low-latency is required
- Access patterns are predictable
- You want serverless operations

Examples:
- User sessions
- Shopping carts
- IoT data
- Gaming backends

---

## Availability and DR Comparison

| Feature | RDS | Aurora | DynamoDB |
|------|-----|--------|----------|
| Multi-AZ | Optional | Default | Default |
| Read replicas | Yes | Yes (fast) | Not needed |
| PITR | Yes | Yes | Yes |
| Global replication | Limited | Global DB | Global Tables |

---

## Cost Considerations (Simplified)

- RDS → Instance + storage cost
- Aurora → Higher cost, better performance
- DynamoDB → Pay per request or capacity

Rule of thumb:
- Start simple
- Optimize when needed

---

## Common Wrong Choices

- Using DynamoDB for relational queries ❌
- Using RDS for massive scale ❌
- Choosing Aurora too early ❌
- Ignoring access patterns ❌

---

## Interview Quick Answers

**Q: Which AWS database is serverless?**  
A: DynamoDB.

**Q: Which database provides fastest failover?**  
A: Aurora.

**Q: Which database is best for ACID transactions?**  
A: RDS or Aurora.

---

## Final Takeaway

There is no “best” database.
There is only the **right database for the workload**.

Correct choice leads to:
- Better performance
- Lower cost
- Simpler architecture

---

📌 **Next:** Phase 07 – Security (KMS, Secrets Manager, WAF, Shield)
