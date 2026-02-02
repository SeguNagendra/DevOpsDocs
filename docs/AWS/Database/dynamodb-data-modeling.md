---
sidebar_position: 6
title: DynamoDB Data Modeling and Keys
---

# DynamoDB Data Modeling and Keys

In DynamoDB, **data modeling is everything**.
Unlike relational databases, you cannot rely on joins or ad-hoc queries.

👉 In DynamoDB, you design your table **around access patterns**.

---

## Why Data Modeling Matters in DynamoDB

Poor data modeling leads to:
- Hot partitions
- High latency
- High cost
- Scaling failures

Good data modeling provides:
- Predictable performance
- Efficient queries
- Massive scalability

👉 DynamoDB success = good key design.

---

## Access Patterns First (Golden Rule)

Before creating a table, always answer:
- What queries will my application run?
- How often?
- At what scale?

Examples:
- Get user by userId
- List orders for a user
- Get latest events

👉 DynamoDB tables are designed **backwards from queries**.

---

## Partition Key (PK)

Partition key:
- Determines where data is stored
- Controls data distribution
- Must have high cardinality

Good partition key:
- Many unique values
- Even traffic distribution

Bad partition key:
- Few values
- Causes hot partitions

---

## Sort Key (SK)

Sort key:
- Orders items within a partition
- Enables range queries

Examples:
- timestamp
- orderId
- createdAt

Using PK + SK allows:
- One-to-many relationships
- Efficient querying

---

## Composite Primary Key (PK + SK)

With a composite key:
- PK groups related items
- SK differentiates items

Example:
- PK = userId
- SK = orderTimestamp

This supports:
- Get all orders for a user
- Get orders in time range

---

## Single-Table Design (Important Concept)

DynamoDB encourages:
- One table for many entities
- Different item types in one table

Why?
- Faster queries
- Fewer tables
- Better performance

This is a shift from SQL thinking.

---

## Secondary Indexes

Indexes enable additional access patterns.

### Global Secondary Index (GSI)
- Different partition and sort key
- Independent scaling

### Local Secondary Index (LSI)
- Same partition key
- Different sort key
- Defined at table creation

👉 GSIs are more flexible and commonly used.

---

## When to Use Indexes

Use indexes when:
- Access pattern cannot be satisfied by primary key
- Querying by alternative attributes

Avoid:
- Creating many unused GSIs (costly)

---

## Queries vs Scans (Critical Difference)

### Query
- Uses partition key
- Fast and efficient
- Preferred

### Scan
- Reads entire table
- Slow and expensive
- Avoid in production

👉 Scans do not scale.

---

## Hot Partitions (Common Problem)

Hot partitions occur when:
- Too many requests hit same partition key

Avoid by:
- Better key design
- Adding randomness
- Using time-based bucketing

---

## Real-World Example

Access patterns:
- Get user profile
- Get all orders for user
- Get latest order

Design:
- PK = USER#userId
- SK = ORDER#timestamp

This supports all patterns efficiently.

---

## Common Beginner Mistakes

- Designing tables like SQL
- Ignoring access patterns
- Overusing GSIs
- Using scans in production

These mistakes cause:
- Performance degradation
- Cost explosion

---

## Interview Tip

If asked:
> “How do you design DynamoDB tables?”

Strong answer:
> By identifying access patterns first and designing partition and sort keys to support efficient queries without scans.

---

## Key Takeaways

- Data modeling is critical in DynamoDB
- Access patterns drive design
- Partition keys control scaling
- Sort keys enable range queries
- Queries scale, scans do not

---

📌 **Next:** DynamoDB Indexes and Capacity Planning
