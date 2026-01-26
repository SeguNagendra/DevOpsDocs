---
sidebar_position: 16
---

## Indexes & Query Performance (Automation Tester Perspective)

Indexes explain **why some SQL queries are fast and others are painfully slow**.
For automation testers, this knowledge helps:
- Avoid slow DB validations
- Reduce CI timeouts
- Write efficient, safe queries

You are **not tuning indexes** — you are **writing index-friendly queries**.

---

## What is an Index?

An **index** is a data structure that allows the database to **find rows faster**.

Think of it like:
> **Index in a book → jump directly to the page**

Without an index:
- DB scans every row (full table scan)

With an index:
- DB jumps directly to matching rows

---

## Why Indexes Matter in Automation

Automation DB checks often run:
- Frequently
- In parallel
- In CI pipelines

Slow queries cause:
- Test timeouts
- Pipeline failures
- False negatives

---

## Columns Commonly Indexed

Typically indexed columns:
- Primary keys
- Foreign keys
- Frequently used WHERE columns

Example:
```sql
WHERE user_id = 101
```

This is fast if `user_id` is indexed.

---

## Index-Friendly Queries (IMPORTANT)

### ✅ Good (Uses index)
```sql
SELECT * FROM users WHERE user_id = 101;
```

### ❌ Bad (Index not used)
```sql
SELECT * FROM users WHERE UPPER(username) = 'JOHN';
```

Why?
- Functions on indexed columns disable index usage

---

## LIKE and Indexes

### Fast
```sql
WHERE email LIKE 'john%'
```

### Slow
```sql
WHERE email LIKE '%gmail.com'
```

Leading `%` prevents index usage.

---

## ORDER BY and Indexes

```sql
ORDER BY created_date DESC
```

Fast if `created_date` is indexed.

Otherwise:
- DB must sort results
- Slow for large tables

---

## Aggregations & Index Impact

```sql
SELECT COUNT(*) FROM orders WHERE status = 'SUCCESS';
```

Fast if `status` is indexed.

---

## Common Automation Performance Mistakes ❌

- Using SELECT *
- Filtering on non-indexed columns
- Applying functions in WHERE
- Using LIKE '%value%'
- Joining large tables unnecessarily

---

## How to Write Performance-Safe Queries (Tester Rules)

- Filter using primary keys
- Avoid functions in WHERE
- Limit result set
- Use ORDER BY only when required
- Keep joins minimal
- Prefer EXISTS over IN for large tables

---

## Do Testers Create Indexes?

❌ No.  
Index creation is DBA responsibility.

What testers SHOULD do:
- Understand why a query is slow
- Raise performance concerns
- Optimize query logic

---

## Real Automation Scenario

### Problem
DB validation query times out in CI.

### Likely Causes
- Full table scan
- Missing WHERE clause
- Function on indexed column
- Too many joins

Solution:
- Rewrite query
- Reduce scope
- Use indexed columns

---

## Key Takeaways 🎯

- Indexes speed up queries
- Query structure affects index usage
- Performance issues cause flaky tests
- Write efficient SELECT queries
- Tester awareness prevents CI failures
