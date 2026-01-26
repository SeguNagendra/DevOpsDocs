---
sidebar_position: 3
---

## Tables, Rows, and Columns

This concept explains **how data is actually stored inside a database**.
For automation testers, this is critical because **all validations ultimately read rows and columns from tables**.

---

## What is a Table?

A **table** is a structured container that stores related data in a grid-like format.

Example:
- `USERS` table → stores user information
- `ORDERS` table → stores order details
- `PAYMENTS` table → stores payment transactions

Think of a table as:

> **One Excel sheet, but much more powerful**

---

## Table Structure (Visual)

```
USERS
------------------------------------------------
| user_id | username | email | status | created |
------------------------------------------------
| 101     | john     | j@x.com| ACTIVE | 01-Jan |
| 102     | mary     | m@x.com| BLOCKED| 03-Jan |
------------------------------------------------
```

---

## What is a Column?

A **column** represents **one attribute** of the data.

Examples:
- `user_id` → unique identifier
- `username` → login name
- `status` → ACTIVE / BLOCKED
- `created` → account creation date

Column rules:
- Each column has a **data type** (number, text, date)
- All values in a column are of the same type

---

## What is a Row?

A **row** represents **one complete record**.

Example:
```
user_id = 101
username = john
email = j@x.com
status = ACTIVE
```

As an automation tester:
- One row = one user / one order / one transaction

---

## Why Rows & Columns Matter for Automation

When you validate backend data, you usually:
- Search for a specific row
- Validate values in certain columns

Example validations:
- User status is `ACTIVE`
- Payment amount is correct
- Order is created for the right user

---

## Primary Key (Basic Introduction)

A **primary key** uniquely identifies each row in a table.

Example:
```text
user_id
```

Rules:
- Cannot be NULL
- Must be unique

Why testers care:
- Helps fetch exact records
- Prevents duplicate data issues

---

## Foreign Key (Conceptual)

A **foreign key** links one table to another.

Example:
- `ORDERS.user_id` → refers to `USERS.user_id`

This creates a **relationship** between tables.

As a tester:
- You validate data across tables using this relationship

---

## Real Automation Scenario

### UI Action
User places an order

### Database Impact
- New row added in `ORDERS`
- Linked to `USERS` via `user_id`

Automation validation:
- Check order row exists
- Verify correct user_id
- Validate order status

---

## Common Beginner Mistakes ❌

- Confusing rows with columns
- Assuming table names are same across apps
- Expecting one table for everything
- Ignoring primary keys during validation

---

## Key Takeaways

- Table = data container
- Column = attribute
- Row = one record
- Primary key uniquely identifies a row
- Foreign key links tables
- Automation validations always read rows & columns
