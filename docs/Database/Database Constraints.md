---
sidebar_position: 22
---

## Database Constraints (UNIQUE, NOT NULL, CHECK) – Automation Tester Awareness

Database constraints enforce **data integrity rules** at the database level.
Automation testers don’t define constraints, but understanding them is essential to:
- Explain DB errors
- Debug failed inserts/updates
- Identify real backend bugs vs test issues

---

## What is a Database Constraint?

A **constraint** is a rule applied to a column or table that restricts the data allowed.

Think of it as:
> **A safety guard that prevents invalid data from entering the database**

---

## Why Constraints Matter for Automation Testers

When a constraint is violated:
- UI/API may show a generic error
- DB throws a specific constraint error
- Automation test may fail without clarity

Knowing constraints helps testers:
- Pinpoint root cause
- Report accurate defects
- Avoid false failures

---

## 1️⃣ NOT NULL Constraint

### What it Does
Prevents NULL values in a column.

```sql
email VARCHAR NOT NULL
```

### Automation Scenario
- UI submits form without email
- Backend tries to insert NULL
- DB rejects the insert

### Tester Takeaway
- Validate mandatory fields
- Expect failure if NULL is passed
- Use IS NULL / IS NOT NULL in DB checks

---

## 2️⃣ UNIQUE Constraint

### What it Does
Ensures all values in a column are unique.

```sql
email VARCHAR UNIQUE
```

### Automation Scenario
- Create user with existing email
- DB rejects insert due to duplication

### Tester Takeaway
- Duplicate data bugs are caught at DB level
- COUNT(*) checks help detect duplicates
- Useful for validating idempotency

---

## 3️⃣ CHECK Constraint

### What it Does
Restricts values based on a condition.

```sql
status CHECK (status IN ('ACTIVE','INACTIVE','BLOCKED'))
```

### Automation Scenario
- Backend tries to store invalid status
- DB rejects the operation

### Tester Takeaway
- Explains “invalid value” errors
- Helps validate business rules enforcement

---

## Constraint Violations – What Testers See

Typical error patterns:
- “Unique constraint violated”
- “Cannot insert NULL”
- “Check constraint failed”

UI/API may hide these details, but DB logs reveal them.

---

## Constraints vs Application Validation

| Validation | Application | Database |
|---|---|---|
| User-friendly error | ✅ | ❌ |
| Final data safety | ❌ | ✅ |
| Can be bypassed | ❌ | ❌ |

Tester insight:
> Application validation can be bypassed, DB constraints cannot.

---

## Common Automation Mistakes ❌

- Ignoring DB constraint errors
- Treating constraint failures as UI bugs
- Using shared test data that violates UNIQUE
- Not cleaning up data between runs

---

## Best Practices for Automation Testers ✅

- Know which fields are constrained
- Use unique test data
- Validate error scenarios intentionally
- Correlate UI/API errors with DB constraints
- Include DB evidence in defect reports

---

## Interview-Ready Explanations

**Q: What is a UNIQUE constraint?**  
A: It prevents duplicate values in a column.

**Q: Why are constraints important?**  
A: They enforce data integrity at the database level.

**Q: Do testers create constraints?**  
A: No, testers validate behavior when constraints are violated.

---

## Key Takeaways 🎯

- Constraints protect data integrity
- NOT NULL, UNIQUE, CHECK are most common
- Constraint errors explain many failures
- DB constraints are final authority
- Awareness improves debugging & interviews