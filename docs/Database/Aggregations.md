---
sidebar_position: 11
---

## SQL Aggregations (COUNT, SUM, GROUP BY) – Automation Tester Guide

Aggregation functions are used to **summarize data**.
Automation testers use them to **verify counts, totals, and duplicates**, not for analytics.

This section focuses only on **practical validation use cases**.

---

## What are Aggregate Functions?

Aggregate functions operate on **multiple rows** and return **one result**.

Common aggregates:
- `COUNT`
- `SUM`
- `MAX`
- `MIN`
- `AVG`

---

## 1️⃣ COUNT – MOST USED ⭐⭐⭐

`COUNT` is used to **count rows**.

### Count all rows
```sql
SELECT COUNT(*) FROM users;
```

### Count specific column
```sql
SELECT COUNT(email) FROM users;
```

Important:
- `COUNT(column)` ignores NULL values
- `COUNT(*)` counts all rows

---

## Automation Use Cases for COUNT

- Verify record is created
- Ensure only one record exists
- Detect duplicate records

Example:
```sql
SELECT COUNT(*) 
FROM orders 
WHERE order_id = 5001;
```

Expected result:
- `1` → Pass
- `0` or `>1` → Fail

---

## 2️⃣ SUM – Total Validation

`SUM` is used to **add numeric values**.

```sql
SELECT SUM(amount) FROM payments WHERE order_id = 5001;
```

Automation examples:
- Validate total payment amount
- Verify invoice totals
- Validate refund calculations

---

## 3️⃣ MAX / MIN – Latest & Oldest Records

### MAX
```sql
SELECT MAX(created_date) FROM orders;
```

### MIN
```sql
SELECT MIN(created_date) FROM orders;
```

Automation use:
- Fetch latest record timestamp
- Validate most recent transaction

---

## 4️⃣ GROUP BY – Grouping Records ⭐⭐

`GROUP BY` groups rows based on a column.

```sql
SELECT status, COUNT(*) 
FROM users 
GROUP BY status;
```

Automation examples:
- Count users by status
- Validate distribution logic
- Detect unexpected data patterns

---

## GROUP BY + HAVING (Awareness)

`HAVING` filters aggregated results.

```sql
SELECT user_id, COUNT(*) 
FROM orders 
GROUP BY user_id
HAVING COUNT(*) > 1;
```

Automation use:
- Detect duplicate records

---

## Common Automation Mistakes ❌

- Forgetting GROUP BY with aggregates
- Using WHERE instead of HAVING
- Misunderstanding COUNT(column)
- Expecting single row but getting many

---

## Best Practices for Automation Testers ✅

- Use COUNT for existence checks
- Prefer COUNT(*) unless NULL matters
- Use GROUP BY only when required
- Validate exact expected numbers
- Log aggregate queries on failure

---

## Key Takeaways 🎯

- Aggregates summarize data
- COUNT is the most important aggregate
- SUM validates totals
- GROUP BY helps detect duplicates
- Essential for backend validation