---
sidebar_position: 1
---

## API Testing – Introduction (Automation Tester Perspective)

API testing is a **core skill** for modern automation testers.
It validates the **backend behavior** of applications without relying on the UI, making tests **faster, more stable, and more reliable**.

This section starts from **absolute basics** and gradually moves to **real-world automation patterns**.

---

## What is an API?

**API** stands for **Application Programming Interface**.

In simple terms:
> An API allows one software system to communicate with another.

Example:
- UI sends request → API
- API processes logic → Database
- API sends response → UI

Automation testers validate this **middle layer**.

---

## Why API Testing is Important

UI testing alone is not enough.

| UI Testing | API Testing |
|---|---|
| Slow | Fast |
| Fragile (UI changes break tests) | Stable |
| Hard to debug | Easy to debug |
| Depends on frontend | Independent of frontend |

API testing helps:
- Catch bugs earlier
- Reduce flaky UI tests
- Validate business logic directly
- Improve CI stability

---

## Where API Fits in Test Pyramid

```
        UI Tests
       ----------
      API Tests
     ------------
   Unit Tests
```

Key idea:
> **More API tests, fewer UI tests = stable automation suite**

---

## API Testing vs UI Testing

| Aspect | UI | API |
|---|---|---|
| Speed | Slow | Fast |
| Execution | Browser needed | No browser |
| Validation | Visual + functional | Functional + data |
| Flakiness | High | Low |

Senior testers always prefer:
> **Validate logic at API level, UI only for critical flows**

---

## Real Application Flow (Important)

```
UI
 ↓
API
 ↓
Business Logic
 ↓
Database
```

Automation testers can validate at:
- API layer
- Database layer
- API + DB together (best practice)

---

## What Automation Testers Validate Using APIs

- Status codes
- Response body
- Business rules
- Error handling
- Security behavior
- Data correctness (API → DB)

---

## What API Testing is NOT

- ❌ Not UI automation
- ❌ Not backend development
- ❌ Not performance testing (unless specified)
- ❌ Not replacing unit tests

API testing focuses on **functional correctness**.

---

## Tools Commonly Used for API Testing

- Postman (manual + exploration)
- RestAssured (Java automation)
- Curl (debugging)
- CI tools (Jenkins, GitLab)

We will cover:
> **Postman first → then RestAssured automation**

---

## Common Beginner Myths ❌

- “API testing is only for backend developers” → ❌
- “UI testing is enough” → ❌
- “API tests are hard” → ❌

Reality:
> API testing is one of the **most valuable skills for automation testers**.

---

## Key Takeaways 🎯

- API testing validates backend behavior
- Faster and more stable than UI tests
- Essential for modern automation roles
- Strongly complements DB knowledge