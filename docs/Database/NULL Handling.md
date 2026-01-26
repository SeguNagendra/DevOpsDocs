---
sidebar_position: 9
---

## SQL NULL Handling (IS NULL / IS NOT NULL) – Automation Tester Guide

NULL handling is one of the **most common causes of wrong DB validations** in automation.
Understanding NULL correctly prevents:
- False failures
- Missed bugs
- Incorrect assertions

---

## What is NULL?

`NULL` means **no value / unknown / not applicable**.

Important:
- NULL ≠ empty string (`''`)
- NULL ≠ zero (`0`)
- NULL ≠ false

> NULL represents **absence of a value**, not a value itself.

---

## Why NULL Matters in Automation Testing

In real applications:
- Optional fields are often NULL
- Status fields change from NULL → value
- Backend bugs often show up as unexpected NULLs

Automation validations must handle this correctly.

---

## ❌ Wrong Way to Check NULL

```sql
SELECT * FROM users WHERE email = NULL;
```

This query will **never return rows**.

Why?
- NULL cannot be compared using `=`

---

## ✅ Correct Way: IS NULL

```sql
SELECT * FROM users WHERE email IS NULL;
```

Use cases:
- Field not populated
- Optional data missing
- Backend failure scenarios

---

## ✅ IS NOT NULL

```sql
SELECT * FROM users WHERE email IS NOT NULL;
```

Use cases:
- Ensure value is stored
- Validate mandatory fields
- Check data persistence

---

## NULL Handling in Conditions

```sql
SELECT * FROM orders
WHERE delivered_date IS NULL
AND status = 'SHIPPED';
```

Automation meaning:
- Order is shipped
- But not delivered yet

---

## NULL in Aggregations (Important)

```sql
SELECT COUNT(delivered_date) FROM orders;
```

- COUNT(column) **ignores NULL values**
- COUNT(*) counts rows regardless of NULLs

Tester tip:
- Choose COUNT carefully based on validation

---

## NULL vs Empty String

| Case | Meaning |
|---|---|
| NULL | No value |
| '' | Empty value |
| ' ' | Space |

Automation bug example:
- UI shows blank
- DB value is NULL
- Assertion fails if misunderstood

---

## Using COALESCE (Awareness)

```sql
SELECT COALESCE(email, 'NOT_PROVIDED') FROM users;
```

- Replaces NULL with default value
- Useful in reports
- Rarely used in automation assertions

---

## Common Automation Mistakes ❌

- Using `=` instead of IS NULL
- Assuming empty string means NULL
- Not validating NULL transitions
- Ignoring NULL in optional fields

---

## Best Practices for Automation Testers ✅

- Always use IS NULL / IS NOT NULL
- Validate NULL explicitly when expected
- Document NULL expectations in tests
- Don’t assume defaults exist

---

## Key Takeaways 🎯

- NULL means absence of value
- Never compare NULL using `=`
- Use IS NULL / IS NOT NULL
- COUNT(column) ignores NULL
- Correct NULL handling avoids flaky tests
