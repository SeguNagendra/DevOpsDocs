---
sidebar_position: 14
---

## DML – INSERT / UPDATE / DELETE (Automation Tester Awareness & Safety)

DML commands modify **actual data** in the database.
For automation testers, this section is about **understanding risks and safe usage**, not frequent execution.

> **Golden Rule:** Automation tests should be **read-heavy, write-light**.

---

## What is DML?

**DML (Data Manipulation Language)** works with data inside tables.

Core DML commands:
- `SELECT` (read)
- `INSERT` (add data)
- `UPDATE` (modify data)
- `DELETE` (remove data)

Testers primarily use **SELECT**.  
Other DML commands are used **sparingly** and **only in test environments**.

---

## 1️⃣ INSERT – Adding Data (Limited Use)

### Example
```sql
INSERT INTO users (user_id, username, status)
VALUES (201, 'test_user', 'ACTIVE');
```

### When Testers Use INSERT
- Test data setup
- Preconditioning scenarios
- Isolated test environments

### Risks ❌
- Duplicate data
- Dirty test data
- Test interference in parallel runs

---

## 2️⃣ UPDATE – Modifying Data (High Risk)

### Example
```sql
UPDATE users
SET status = 'BLOCKED'
WHERE user_id = 201;
```

### Tester Use Cases
- Simulating backend states
- Preparing negative scenarios

### Absolute Rules ⚠️
- **ALWAYS use WHERE**
- Target by **primary key**
- Validate affected row count

❌ Never run:
```sql
UPDATE users SET status = 'BLOCKED';
```

---

## 3️⃣ DELETE – Removing Data (VERY RISKY)

### Example
```sql
DELETE FROM users WHERE user_id = 201;
```

### Tester Guidance
- Avoid DELETE whenever possible
- Prefer soft-delete flags
- Use cleanup scripts cautiously

❌ Never run DELETE in PROD  
⚠️ Rarely allowed even in UAT

---

## Transactions & Rollback (Conceptual)

DML changes can be:
- Committed
- Rolled back

```sql
ROLLBACK;
```

Automation implication:
- Uncommitted data may not be visible
- Failed tests can leave dirty data

---

## Best Practices for Automation Testers ✅

- Prefer read-only DB users
- Isolate test data
- Use INSERT/UPDATE only in setup
- Clean up after tests
- Never mix DML with validation logic
- Log affected row counts

---

## Common Automation Mistakes ❌

- Running UPDATE/DELETE without WHERE
- Using DML in shared environments
- Not cleaning up test data
- Assuming auto-commit behavior

---

## Safer Alternatives to DML

- API-based setup
- Dedicated test data services
- Backend flags instead of deletes
- Reset environments periodically

---

## Real Project Strategy

**Recommended approach:**
- UI/API → Perform action
- DB → Validate using SELECT
- Avoid DB writes unless unavoidable

---

## Key Takeaways 🎯

- DML modifies real data
- SELECT is safe; others require caution
- Use DML only in controlled environments
- Safety > speed in automation
