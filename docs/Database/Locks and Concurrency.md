---
sidebar_position: 17
---

## Locks & Concurrency (Parallel Test Impact – Automation Tester Guide)

Locks and concurrency explain **why parallel tests interfere with each other** and why
DB validations sometimes **hang, fail intermittently, or return unexpected results**.

This guide gives **tester-level clarity** without deep DBA theory.

---

## What is a Lock?

A **lock** is a mechanism used by the database to **protect data integrity** when multiple
operations access the same data at the same time.

Think of it as:
> **Only one person can edit a document at a time**

---

## Why Locks Exist

Without locks:
- Two users update the same row simultaneously
- Data becomes inconsistent or corrupted

Locks ensure:
- Safe updates
- Consistent reads
- Transaction integrity

---

## Types of Locks (Tester Awareness)

### 1️⃣ Read Lock
- Prevents data from being modified
- Allows multiple readers

### 2️⃣ Write Lock
- Prevents other reads/writes
- Used during UPDATE/DELETE

Automation implication:
- One test updating data can block another test reading it

---

## How Parallel Tests Cause Lock Issues

### Typical Scenario

```
Test A (Thread 1) → UPDATE order status
           ↓ (lock held)
Test B (Thread 2) → SELECT same order
           ↓
        WAIT / TIMEOUT
```

Result:
- Test B fails or times out
- Looks like random failure

---

## Locks + Transactions (Important Link)

Locks are held:
- From start of transaction
- Until COMMIT or ROLLBACK

If COMMIT is delayed:
- Lock stays longer
- Other tests get blocked

---

## Common Automation Lock Issues ❌

- Parallel tests updating same data
- Cleanup scripts running in parallel
- Long-running transactions
- Forgetting to commit or rollback
- Using shared test accounts

---

## Symptoms Seen in Automation

- Tests hanging indefinitely
- DB queries timing out
- Random failures in CI only
- Tests pass locally but fail in pipeline

---

## Best Practices to Avoid Lock Issues ✅

- Use **unique test data per test**
- Avoid UPDATE/DELETE in parallel tests
- Keep transactions short
- Validate using SELECT only
- Run DB-modifying tests sequentially
- Clean up data carefully

---

## Concurrency vs Isolation (Conceptual)

- Concurrency = multiple operations at once
- Isolation controls **visibility of changes**

Automation takeaway:
> Higher parallelism = higher risk of interference

---

## Automation Strategy for Parallel Execution

Recommended:
- Parallelize at **test level**, not data level
- Isolate data per test
- Avoid shared records
- Use retry only for transient issues

---

## Real Project Example

### Problem
- Parallel tests updating same user
- Random failures in CI

### Fix
- Create user per test
- Remove shared UPDATE
- Reduce parallel scope

---

## Key Takeaways 🎯

- Locks protect data but cause blocking
- Parallel tests amplify lock issues
- Most DB flakiness = lock + transaction problems
- Isolation of test data is critical
- Understanding locks saves hours of debugging
