---
sidebar_position: 18
---

## Common Database Errors & Automation Debugging Patterns

Even well-written automation tests fail due to **database-related issues**.
Senior automation testers don’t panic — they **recognize patterns** and debug efficiently.

This section consolidates **real-world DB errors** and how automation testers should respond.

---

## Why DB Errors Matter in Automation

DB issues often appear as:
- UI failures
- API errors
- Random CI failures

But the **root cause lives in the database**.

Understanding common DB errors saves:
- Debugging time
- False defect reports
- CI pipeline instability

---

## 1️⃣ No Rows Found (Empty Result)

### Symptom
```sql
SELECT * FROM orders WHERE order_id = 5001;
-- returns 0 rows
```

### Possible Causes
- Transaction not committed yet
- Incorrect test data
- Wrong environment
- Timing issue

### Tester Actions
- Verify commit
- Add wait/retry with timeout
- Confirm environment & data
- Check WHERE clause accuracy

---

## 2️⃣ Multiple Rows Returned (Expected One)

### Symptom
```sql
SELECT * FROM users WHERE email = 'test@gmail.com';
-- returns multiple rows
```

### Possible Causes
- Duplicate data
- Weak WHERE clause
- Missing primary key filter

### Tester Actions
- Validate data uniqueness
- Switch to primary key
- Raise data integrity issue

---

## 3️⃣ Permission Denied / Insufficient Privileges

### Symptom
```
ORA-01031: insufficient privileges
```

### Possible Causes
- DB user has read-only access
- Missing SELECT permission
- CI user differs from local user

### Tester Actions
- Verify DB credentials
- Request SELECT access
- Do NOT ask for DML access casually

---

## 4️⃣ Query Timeout / Slow Execution

### Symptom
- Test hangs
- CI timeout
- DB validation very slow

### Possible Causes
- Full table scan
- Missing WHERE clause
- Non-indexed column
- Lock contention

### Tester Actions
- Simplify query
- Filter using indexed columns
- Limit result set
- Check for locks

---

## 5️⃣ Data Not Visible Immediately

### Symptom
- UI/API success
- DB validation fails

### Possible Causes
- Transaction delay
- Asynchronous processing
- Eventual consistency

### Tester Actions
- Add smart waits
- Validate using time window
- Avoid immediate DB assertion

---

## 6️⃣ NULL vs Empty Value Confusion

### Symptom
- Assertion fails
- DB value looks “blank”

### Possible Causes
- NULL stored instead of empty string
- Incorrect comparison

### Tester Actions
- Use IS NULL / IS NOT NULL
- Align expectation with backend logic

---

## 7️⃣ Lock Wait / Deadlock Issues

### Symptom
- Random failures
- Tests stuck in WAITING state

### Possible Causes
- Parallel tests updating same data
- Long-running transactions

### Tester Actions
- Isolate test data
- Reduce parallelism
- Avoid DB writes in tests

---

## Debugging Checklist (Automation Tester)

Before raising a bug:
- Is the query correct?
- Is data committed?
- Is test data unique?
- Is environment correct?
- Is this a timing issue?
- Is this reproducible?

---

## Logging Best Practices

- Log SQL queries
- Log query results
- Log timestamps
- Log DB user/environment
- Attach logs to test reports

Good logs = faster root cause analysis.

---

## Senior-Level Debugging Pattern

```
Test Failure
   ↓
Check UI/API response
   ↓
Run DB query manually
   ↓
Analyze data, timing, locks
   ↓
Decide: Bug / Test issue / Env issue
```

---

## Common Mistakes ❌

- Blaming UI immediately
- Writing flaky DB assertions
- Hardcoding sleep
- Ignoring transaction boundaries
- Using shared test data

---

## Key Takeaways 🎯

- Most automation failures have DB roots
- Patterns repeat across projects
- Calm analysis beats quick assumptions
- DB awareness = senior automation skill
