---
sidebar_position: 4
---

<!-- ## Primary Key & Foreign Key -->

Keys define **how data is uniquely identified and related** inside a database.
For automation testers, understanding keys is critical to:
- Fetch the right records
- Validate relationships
- Avoid false test failures

---

## What is a Primary Key?

A **Primary Key (PK)** uniquely identifies **each row** in a table.

### Example
```
USERS
--------------------------------
| user_id (PK) | username | ... |
--------------------------------
| 101          | john     |     |
| 102          | mary     |     |
```

### Rules of Primary Key
- Must be **unique**
- Cannot be **NULL**
- One primary key per table (can be composite)

---

## Why Primary Key Matters for Testers

- Fetch exact records reliably
- Avoid validating duplicate rows
- Ensure assertions target the correct data

**Bad validation ❌**
> “Check first row in USERS table”

**Good validation ✅**
> “Fetch row where user_id = 101”

---

## What is a Foreign Key?

A **Foreign Key (FK)** creates a **relationship** between two tables.

### Example
```
ORDERS
------------------------------------
| order_id (PK) | user_id (FK) | ...|
------------------------------------
| 5001          | 101          |     |
```

Here:
- `ORDERS.user_id` → refers to `USERS.user_id`

This enforces **referential integrity**.

---

## Why Foreign Key Matters for Automation

- Validates data across tables
- Ensures business rules are followed
- Enables joins for backend verification

### Real Scenario
- User places an order
- Order must reference an existing user

Automation check:
- Order exists
- Linked user exists
- Relationship is valid

---

## Primary Key vs Foreign Key (Quick Comparison)

| Aspect | Primary Key | Foreign Key |
|---|---|---|
| Purpose | Identify a row | Link tables |
| Uniqueness | Must be unique | Can repeat |
| NULL allowed | ❌ No | ✅ Yes (sometimes) |
| Used by testers | Always | Very often |

---

## Composite Keys (Awareness)

A **composite key** uses **multiple columns** as a primary key.

Example:
```
(order_id, product_id)
```

Tester note:
- Rarely validated directly
- Be aware when querying

---

## Common Automation Mistakes ❌

- Ignoring primary keys in validations
- Using non-unique columns (like username)
- Assuming FK always exists
- Hardcoding IDs without context

---

## Best Practices (Tester-Level)

- Always identify the primary key first
- Use PKs in WHERE clauses
- Understand FK relationships before joins
- Validate relationships, not just data

---

## Key Takeaways

- Primary key uniquely identifies a record
- Foreign key links related tables
- Keys make validations accurate
- Essential before learning joins & SQL
