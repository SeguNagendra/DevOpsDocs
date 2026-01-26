---
sidebar_position: 7
---

## SQL Command Types – DDL, DML, DCL, TCL (Automation Tester Guide)

Before writing real SQL queries, it’s critical to understand **how SQL commands are classified**.
This helps automation testers:
- Avoid dangerous operations
- Know what they are allowed to run
- Debug permission & transaction issues confidently

---

## Why SQL Command Types Matter for Testers

In real projects:
- Testers mostly have **read-only DB access**
- Certain commands are **blocked in UAT/PROD**
- Knowing command types prevents accidental damage

---

## Overview of SQL Command Categories

SQL commands are grouped into **four main categories**:

| Category | Full Form | Purpose | Tester Usage |
|---|---|---|---|
| **DDL** | Data Definition Language | Define structure | Awareness |
| **DML** | Data Manipulation Language | Work with data | ⭐ Core |
| **DCL** | Data Control Language | Access control | Awareness |
| **TCL** | Transaction Control Language | Transactions | Conceptual |

---

## 1️⃣ DDL – Data Definition Language

DDL commands define or modify **database structure**.

### Common DDL Commands
- `CREATE`
- `ALTER`
- `DROP`
- `TRUNCATE`

### Examples
```sql
CREATE TABLE users (...);
ALTER TABLE users ADD email VARCHAR(50);
DROP TABLE users;
```

### Tester Perspective
- ❌ Do NOT run DDL in automation
- ❌ Never run in PROD
- ✅ Understand logs & scripts that contain DDL

Use case for testers:
- Reading migration scripts
- Understanding schema changes

---

## 2️⃣ DML – Data Manipulation Language ⭐ (MOST IMPORTANT)

DML commands work with **actual data inside tables**.

### Common DML Commands
- `SELECT` ⭐⭐⭐
- `INSERT`
- `UPDATE`
- `DELETE`

### Examples
```sql
SELECT * FROM users;
INSERT INTO users VALUES (...);
UPDATE users SET status='ACTIVE';
DELETE FROM users WHERE id=10;
```

### Tester Perspective
- ✅ `SELECT` is used daily
- ⚠️ `INSERT/UPDATE` only in test setup
- ❌ `DELETE` rarely allowed

➡️ **90% of automation DB validation uses SELECT**

---

## 3️⃣ DCL – Data Control Language

DCL commands manage **permissions and access**.

### Common DCL Commands
- `GRANT`
- `REVOKE`

### Example
```sql
GRANT SELECT ON users TO test_user;
```

### Tester Perspective
- ❌ You don’t use DCL in automation
- ✅ Helps debug errors like:
  - “Permission denied”
  - “Insufficient privileges”

---

## 4️⃣ TCL – Transaction Control Language

TCL commands control **transactions**.

### Common TCL Commands
- `COMMIT`
- `ROLLBACK`
- `SAVEPOINT`

### Example
```sql
ROLLBACK;
COMMIT;
```

### Tester Perspective
- Helps explain:
  - Dirty test data
  - Data not visible immediately
  - Flaky tests in parallel execution

---

## Quick Comparison (Important)

| Category | Structure | Data | Permissions | Transactions |
|---|---|---|---|---|
| DDL | ✅ | ❌ | ❌ | ❌ |
| DML | ❌ | ✅ | ❌ | ❌ |
| DCL | ❌ | ❌ | ✅ | ❌ |
| TCL | ❌ | ❌ | ❌ | ✅ |

---

## Common Tester Mistakes ❌

- Running UPDATE/DELETE without WHERE
- Confusing DDL with DML
- Assuming COMMIT happens automatically
- Blaming UI when transaction isn’t committed

---

## Best Practices for Automation Testers ✅

- Prefer read-only DB users
- Always double-check command type
- Use SELECT for validation
- Keep DML changes limited to test env
- Understand transaction behavior

---

## Key Takeaways 🎯

- SQL commands are classified for safety & control
- DML (SELECT) is core for testers
- DDL & DCL are awareness-level
- TCL explains many flaky behaviors
