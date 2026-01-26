---
sidebar_position: 1
---

## Database – Introduction (Automation Tester Perspective)

## What is a Database?

A **database** is an organized place where an application **stores its data permanently**.

In simple words:

> **Database = the memory of an application**

Whenever a user:
- registers
- logs in
- places an order
- makes a payment

👉 that information is stored in a **database**.

---

## Why Applications Need a Database

Without a database:
- Data disappears after refresh ❌
- No login history ❌
- No transactions ❌
- No user profiles ❌

With a database:
- Data is permanent
- Multiple users are supported
- Business history is preserved

---

## Real Automation Examples

| Application Action | Database Effect |
|-------------------|----------------|
| User registration | New record created |
| Login | Status updated |
| Order placed | Transaction stored |
| Payment failed | Error flag saved |
| Account blocked | Status changed |

As an automation tester:
- UI/API = front-end
- Database = **source of truth**

---

## Database vs Excel / Files

### Excel / Files ❌
- Not secure
- No concurrent users
- Poor performance
- No relationships

### Database ✅
- Secure
- Multi-user
- Fast
- Structured
- Supports relationships

---

## High-Level Application Flow

```
User / Automation Script
        ↓
Application (UI / API)
        ↓
Business Logic
        ↓
Database
```

Automation validates **UI/API**, database confirms **actual behavior**.

---

## Why Database Knowledge Matters for Testers

- Detect backend issues early
- Validate business rules
- Debug failures faster
- Become senior-level automation tester

---

## Key Takeaways

- Database stores application data
- Every automation test relies on DB indirectly
- DB validation increases test reliability
