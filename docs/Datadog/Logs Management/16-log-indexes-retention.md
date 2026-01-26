---
sidebar_position: 3
---

# Log Indexes & Retention

> *“Logs are valuable — but only if you can find them without paying a fortune.”*

This module belongs to **PHASE 8: Logs Management**.  
Here we focus on **how logs are stored, searched, and retained**, and how these choices directly impact **cost and performance**.

---

## What Is a Log Index?

A **log index** is a searchable storage location for logs.

When logs are indexed:
- They become searchable in real time
- They can be used for alerts
- They are available for analytics

When logs are not indexed:
- They are stored only in archives
- They are cheaper
- They are not searchable by default

---

## Why Indexing Matters

Indexing determines:
- What logs you can search
- What alerts you can create
- How fast investigations happen

Indexing everything:
- Is expensive
- Is rarely necessary

Best practice:
> Index what you need, archive the rest.

---

## Index Selection Strategy

Good indexing strategy starts with questions:
- What logs are critical during incidents?
- What logs are required for compliance?
- What logs are rarely accessed?

Common indexed logs:
- Application errors
- Security events
- API access logs (filtered)

---

## Multiple Indexes (Why They Exist)

Datadog allows multiple indexes to:
- Separate concerns
- Apply different retention policies
- Control costs

Examples:
- `prod-errors`
- `security-logs`
- `audit-events`

Each index can have:
- Its own filter
- Its own retention period

---

## Retention Periods

Retention defines:
- How long indexed logs are kept
- How long they are searchable

Shorter retention:
- Lower cost
- Less historical data

Longer retention:
- Higher cost
- Better historical analysis

Choose retention based on:
- Business needs
- Compliance requirements
- Cost constraints

---

## Archives (Cost-Saving Strategy)

Archives store logs in:
- Object storage (like S3)
- At much lower cost

Archived logs:
- Are not immediately searchable
- Can be rehydrated when needed

Best practice:
> Archive everything, index selectively.

---

## Rehydration (Conceptual)

Rehydration means:
- Temporarily making archived logs searchable

Used for:
- Post-incident analysis
- Audits
- Forensics

This avoids:
> Paying high indexing cost for rarely used logs.

---

## Indexing & Security

Indexing sensitive data:
- Increases risk
- Increases compliance scope

Best practices:
- Mask sensitive fields before indexing
- Limit access to security-related indexes
- Audit index usage

---

## Common Indexing Mistakes

❌ One index for all logs  
❌ Long retention for low-value logs  
❌ Indexing debug logs  
❌ No archive strategy  

---

## Why This Module Matters

Poor indexing strategy leads to:
- High Datadog bills
- Slow searches
- Unusable logs

Good indexing strategy leads to:
- Fast investigations
- Predictable costs
- Better observability

---

## Key Takeaways

- Indexing controls searchability
- Retention controls cost
- Multiple indexes add flexibility
- Archives save money

---

➡️ **Next Phase:** Tracing, APM & Profiling
