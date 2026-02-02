---
sidebar_position: 7
title: DynamoDB Indexes and Capacity Planning
---

# DynamoDB Indexes and Capacity Planning

Designing DynamoDB tables does not stop at keys.
To run DynamoDB **efficiently in production**, you must understand:
- Indexes (GSI vs LSI)
- Capacity models
- Cost and throttling behavior

This topic separates **basic users from real DynamoDB engineers**.

---

## Secondary Indexes in DynamoDB

Indexes allow you to support **additional access patterns** without scanning the table.

DynamoDB provides:
- Global Secondary Indexes (GSI)
- Local Secondary Indexes (LSI)

---

## Global Secondary Index (GSI)

A GSI:
- Has its **own partition key and optional sort key**
- Can differ from the base table keys
- Scales independently

### Characteristics
- Created anytime
- Has separate read/write capacity
- Most commonly used index type

👉 GSIs are the **default choice** for new access patterns.

---

## Local Secondary Index (LSI)

An LSI:
- Uses the **same partition key** as the base table
- Has a different sort key
- Must be created at table creation time

### Limitations
- Max 5 LSIs per table
- Shares capacity with base table

👉 LSIs are less flexible and rarely used.

---

## GSI vs LSI (Comparison)

| Feature | GSI | LSI |
|------|-----|-----|
| Partition key | Different | Same as table |
| Sort key | Optional | Required |
| Created after table | Yes | No |
| Capacity | Separate | Shared |
| Usage | Very common | Rare |

---

## When to Use Indexes

Use indexes when:
- Queries cannot be satisfied by primary key
- Access patterns are known and stable

Avoid:
- Creating indexes “just in case”
- Too many GSIs (high cost)

---

## Capacity Modes in DynamoDB

DynamoDB supports two capacity modes:

---

## On-Demand Capacity

On-Demand:
- No capacity planning
- Pay per request
- Scales automatically

Best for:
- Spiky workloads
- Unpredictable traffic
- New applications

👉 Simplest and safest starting point.

---

## Provisioned Capacity

Provisioned:
- You define RCUs and WCUs
- Predictable cost
- Requires planning

Best for:
- Steady workloads
- High, predictable traffic

Use with:
- Auto Scaling

---

## Read and Write Capacity Units

### Read Capacity Unit (RCU)
- 1 RCU = 1 strongly consistent read (4 KB)
- 2 eventually consistent reads

### Write Capacity Unit (WCU)
- 1 WCU = 1 write (1 KB)

Understanding this helps control **cost and throttling**.

---

## Throttling (Important)

Throttling occurs when:
- Requests exceed provisioned capacity
- Hot partitions are hit

Symptoms:
- Increased latency
- ProvisionedThroughputExceeded errors

---

## Preventing Throttling

Best practices:
- Good partition key design
- Use on-demand initially
- Enable auto scaling
- Monitor CloudWatch metrics

---

## Index Capacity Planning

Important rule:
- GSIs need **their own capacity planning**
- GSI throttling affects queries using the index

Common mistake:
- Scaling table but not GSIs ❌

---

## Common Beginner Mistakes

- Too many GSIs
- Ignoring GSI costs
- Under-provisioning indexes
- Using scans instead of queries

These mistakes cause:
- High cost
- Poor performance

---

## Interview Tip

If asked:
> “How do you scale DynamoDB?”

Strong answer:
> By designing good partition keys, using GSIs for access patterns, and choosing on-demand or provisioned capacity with auto scaling.

---

## Key Takeaways

- GSIs are flexible and widely used
- LSIs are limited and less common
- Capacity mode affects cost and scaling
- Throttling is avoidable with good design
- Index planning is critical in production

---

📌 **Next:** DynamoDB Advanced Features
