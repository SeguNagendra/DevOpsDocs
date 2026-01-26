---
sidebar_position: 8
---

## SQL SELECT Queries – Basics (Automation Tester Guide)

`SELECT` is the **most important SQL command** for automation testers.
Almost every backend validation in automation relies on **reading data using SELECT**.

> If you master SELECT, you master database validation.

---

## What is SELECT?

`SELECT` is used to **fetch data from one or more columns of a table**.

Basic syntax:
```sql
SELECT column_name FROM table_name;
```

Example:
```sql
SELECT username FROM users;
```

---

## Selecting All Columns

```sql
SELECT * FROM users;
```

- `*` means **all columns**
- Useful for exploration
- ❌ Avoid in automation assertions (fetches unnecessary data)

---

## Selecting Specific Columns (BEST PRACTICE)

```sql
SELECT user_id, username, status FROM users;
```

Why this is better:
- Faster
- Cleaner results
- Clear intent in tests

---

## Using WHERE Clause (MOST USED)

`WHERE` filters rows.

```sql
SELECT * FROM users WHERE user_id = 101;
```

Automation examples:
- Fetch a user by ID
- Check order by order_id
- Validate payment by transaction_id

---

## Using AND / OR Conditions

```sql
SELECT * FROM users
WHERE status = 'ACTIVE' AND role = 'ADMIN';
```

```sql
SELECT * FROM users
WHERE status = 'BLOCKED' OR status = 'INACTIVE';
```

Tester tip:
- Use **AND** for strict checks
- Use **OR** carefully (can return multiple rows)

---

## Using IN (Cleaner Multiple Conditions)

```sql
SELECT * FROM users
WHERE status IN ('ACTIVE', 'PENDING');
```

Better than:
```sql
status='ACTIVE' OR status='PENDING'
```

---

## Using LIKE (Pattern Matching)

```sql
SELECT * FROM users
WHERE email LIKE '%@gmail.com';
```

Common patterns:
- `%text` → ends with
- `text%` → starts with
- `%text%` → contains

Use carefully — LIKE is slower on large tables.

---

## ORDER BY (Sorting Results)

```sql
SELECT * FROM users
ORDER BY created_date DESC;
```

Use cases:
- Get latest record
- Validate most recent transaction

---

## LIMIT / ROWNUM (DB Dependent)

### MySQL / PostgreSQL
```sql
SELECT * FROM users LIMIT 1;
```

### Oracle
```sql
SELECT * FROM users WHERE ROWNUM = 1;
```

Tester use:
- Fetch latest record
- Reduce result size

---

## Common Automation Validations Using SELECT

- Verify record exists
- Validate status flag
- Check timestamps
- Validate amount/value
- Ensure one and only one record exists

---

## Common Mistakes ❌

- Using SELECT * in assertions
- Missing WHERE clause
- Expecting single row but getting many
- Ignoring case sensitivity
- Forgetting ORDER BY for latest data

---

## Best Practices for Automation Testers ✅

- Always use WHERE with primary key
- Fetch only required columns
- Expect exact number of rows
- Log queries during failures
- Keep queries simple and readable

---

## Key Takeaways 🎯

- SELECT is core to DB validation
- WHERE clause is mandatory for accuracy
- ORDER BY helps deterministic results
- LIMIT/ROWNUM avoids unnecessary data
- Clean SELECT = reliable automation
