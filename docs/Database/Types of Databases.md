---
sidebar_position: 5
---

## Types of Databases (RDBMS vs NoSQL) – Automation Tester Awareness

As an automation tester, you don’t need to master every database type.
You **must** understand **which type your application uses** and **how that affects validation**.

Most enterprise applications use **Relational Databases (RDBMS)**.
NoSQL knowledge is mainly **awareness-level** for testers.

---

## High-Level Database Classification

Databases are broadly classified into:

1. **Relational Databases (RDBMS)** ⭐ (MOST IMPORTANT)
2. **Non-Relational Databases (NoSQL)** (Awareness)

---

## 1️⃣ Relational Databases (RDBMS)

RDBMS store data in **tables with rows and columns** and enforce **relationships** using keys.

### Examples
- Oracle
- MySQL
- PostgreSQL
- SQL Server

---

## Key Characteristics of RDBMS

- Data stored in tables
- Fixed schema (structure)
- Uses **SQL**
- Supports joins
- Enforces data integrity (PK/FK)

This matches **most banking, e‑commerce, enterprise systems**.

---

## Why RDBMS is Critical for Automation Testers

As a tester, you will:
- Validate UI/API data against DB tables
- Write SELECT queries
- Use joins to verify relationships
- Check transactional data

👉 **90% of DB validations in automation are on RDBMS**

---

## 2️⃣ Non-Relational Databases (NoSQL) – Awareness Only

NoSQL databases store data in **non-tabular formats**.

### Common NoSQL Types

| Type | Example |
|---|---|
| Document | MongoDB |
| Key-Value | Redis |
| Column | Cassandra |
| Graph | Neo4j |

---

## How NoSQL Differs from RDBMS

| Aspect | RDBMS | NoSQL |
|---|---|---|
| Structure | Tables | Documents / Key-Value |
| Schema | Fixed | Flexible |
| Query Language | SQL | DB-specific |
| Joins | Yes | Limited / None |
| Transactions | Strong | Limited (varies) |

---

## Tester Perspective on NoSQL

- Rarely queried directly in UI automation
- Common in:
  - Microservices
  - Caching layers
  - Logs & analytics

Tester role:
- Validate API responses
- Validate business behavior
- DB-level checks usually done by backend tests

---

## How to Identify DB Type in a Project

You can identify DB type by:
- Asking developers
- Checking configuration files
- Observing SQL usage
- Error messages (Oracle / MySQL hints)

---

## Common Tester Mistakes ❌

- Expecting SQL joins in NoSQL
- Treating all databases the same
- Over-learning NoSQL without need
- Writing complex queries without understanding DB type

---

## Key Takeaways

- RDBMS is the primary DB type for automation testing
- SQL knowledge is essential
- NoSQL is awareness-level for most testers
- Always confirm DB type before validation