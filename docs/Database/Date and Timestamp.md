---
sidebar_position: 12
---

## Date & Timestamp Handling in SQL (Automation Tester Guide)

Date and time validations are a **major source of flaky tests**.
Automation testers must understand how dates are stored, compared, and queried in databases.

This guide focuses on **practical pitfalls and safe patterns**.

---

## Why Date & Time Are Tricky in Automation

Common problems:
- Different time zones
- UI shows formatted date, DB stores raw timestamp
- Delays between UI action and DB commit
- Comparing strings instead of dates

---

## Date vs Timestamp

| Type | Meaning |
|---|---|
| DATE | Date only (sometimes with time 00:00) |
| TIMESTAMP | Date + time (down to seconds/milliseconds) |

Example values:
- DATE → `2026-01-05`
- TIMESTAMP → `2026-01-05 14:32:10`

---

## How Databases Store Date & Time

- Stored in **DB-specific internal format**
- Display format depends on DB/session
- Never assume UI format == DB format

Tester rule:
> **Compare using DB date logic, not strings**

---

## Basic Date Comparison

```sql
SELECT * FROM orders
WHERE created_date = DATE '2026-01-05';
```

Avoid:
```sql
WHERE created_date = '05-01-2026'
```

---

## Comparing Date Ranges (MOST USED)

```sql
SELECT * FROM orders
WHERE created_date BETWEEN 
      DATE '2026-01-01' AND DATE '2026-01-31';
```

Automation use:
- Validate records created today
- Validate monthly reports
- Validate batch jobs

---

## Handling Timestamp Comparisons

Exact timestamp match is risky.

❌ Bad:
```sql
WHERE created_ts = TIMESTAMP '2026-01-05 14:32:10'
```

✅ Better:
```sql
WHERE created_ts >= CURRENT_TIMESTAMP - INTERVAL '5' MINUTE
```

Use tolerance windows.

---

## Getting Current Date & Time

(DB-dependent examples)

```sql
CURRENT_DATE
CURRENT_TIMESTAMP
```

Automation use:
- Validate “created today”
- Validate recent transactions

---

## Date Functions (Awareness)

Common functions:
- `TRUNC(date)` – remove time
- `EXTRACT(YEAR FROM date)`
- `NOW()` / `SYSDATE` (DB specific)

Example:
```sql
SELECT * FROM orders
WHERE TRUNC(created_date) = CURRENT_DATE;
```

---

## Timezone Issues (IMPORTANT)

- Application may use UTC
- DB may use server timezone
- UI may use local timezone

Automation best practice:
- Validate **relative time**, not exact time
- Use time windows

---

## Common Automation Mistakes ❌

- Comparing date as string
- Expecting exact timestamps
- Ignoring timezone differences
- Not waiting for DB commit
- Hardcoding today’s date

---

## Best Practices for Automation Testers ✅

- Use date ranges instead of exact match
- Compare dates using DB functions
- Allow tolerance for timestamps
- Log DB time during failures
- Coordinate timezone strategy with team

---

## Real Automation Scenarios

- Order created within last 5 minutes
- Payment processed today
- Status updated after action
- Batch job ran overnight

---

## Key Takeaways 🎯

- Dates are tricky but manageable
- Avoid exact timestamp comparisons
- Use ranges and tolerances
- Understand timezone behavior
- Date bugs cause flaky tests