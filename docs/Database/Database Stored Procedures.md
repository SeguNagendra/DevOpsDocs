---
sidebar_position: 21
---

## Stored Procedures & Functions (Awareness for Automation Testers)

Stored Procedures and Functions are **frequently used in enterprise applications**, but often misunderstood by automation testers.
This page explains **what they are, why teams use them, and how testers should think about them** — without DBA or backend overload.

---

## What is a Stored Procedure?

A **stored procedure** is a set of SQL statements stored and executed inside the database.

Think of it as:
> **Backend logic living inside the database**

Example (conceptual):
```sql
CALL create_order(user_id, amount);
```

---

## What is a Database Function?

A **function** is similar to a procedure but:
- Returns a value
- Often used inside SELECT queries

Example:
```sql
SELECT calculate_tax(amount) FROM orders;
```

---

## Why Teams Use Stored Procedures

Stored procedures are used to:
- Centralize business logic
- Improve performance
- Reduce network calls
- Enforce security rules

Common real-world usage:
- Order creation
- Payment processing
- Account state changes
- Batch jobs

---

## Where Stored Procedures Fit in Application Flow

```
Automation Test
     ↓
UI / API Call
     ↓
Application Layer
     ↓
Stored Procedure
     ↓
Database Tables
```

Important:
> Automation tests **do not call procedures directly** in most projects.

---

## Automation Tester Perspective (CRITICAL)

As an automation tester:
- ❌ You do NOT write stored procedures
- ❌ You do NOT debug procedure logic
- ✅ You validate **effects of procedures**
- ✅ You verify data using SELECT queries

Example:
- UI triggers “Create Order”
- Backend calls stored procedure
- Tester validates:
  - Order row created
  - Status correct
  - Amount correct

---

## Should Automation Call Stored Procedures Directly?

**Usually NO** ❌

Why:
- Breaks black-box testing
- Bypasses real application flow
- Causes environment coupling

Only exceptions:
- Dedicated DB automation tests
- Explicit team agreement

---

## Common Automation Mistakes ❌

- Trying to test procedure logic directly
- Calling procedures in test scripts
- Assuming procedure execution is instant
- Blaming UI when procedure fails silently

---

## How Stored Procedures Affect DB Validation

Important implications:
- Transactions may span multiple tables
- Commit may happen inside procedure
- Timing delays are common
- Errors may rollback silently

Tester strategy:
- Add wait/retry logic
- Validate final committed state
- Never assume immediate DB update

---

## Error Handling & Debugging (Awareness)

When something fails:
- UI/API may show generic error
- Root cause may be inside procedure

Tester actions:
- Capture DB state before & after
- Check affected tables
- Share evidence with backend team

---

## Interview-Ready Explanations

**Q: What is a stored procedure?**  
A: A set of SQL statements stored and executed inside the database.

**Q: Do automation testers write stored procedures?**  
A: No, testers validate their effects through UI/API and DB queries.

**Q: Why are stored procedures used?**  
A: Performance, security, and centralized business logic.

---

## Key Takeaways 🎯

- Stored procedures run inside DB
- Automation tests them indirectly
- Validation is done via SELECT
- Timing & transactions matter
- Awareness is enough for testers