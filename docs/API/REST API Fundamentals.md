---
sidebar_position: 3
---

## REST API Fundamentals (Automation Tester Perspective)

REST is the **most widely used API style** in modern applications.
Automation testers don’t need REST theory like backend developers — they need to know **how REST affects testing, validation, and debugging**.

---

## What is REST?

**REST** stands for **Representational State Transfer**.

In simple words:
> REST is a way of designing APIs so that clients can interact with resources using standard HTTP methods.

Key idea for testers:
- REST APIs are predictable
- Behavior is driven by HTTP methods + status codes

---

## REST Resources & Endpoints

### Resource
A **resource** represents a real-world entity.

Examples:
- User
- Order
- Payment

### Endpoint
An **endpoint** is the URL that represents a resource.

Examples:
```
/users
/users/101
/orders/5001
```

Tester mindset:
> Endpoints should represent **nouns**, not actions.

---

## REST Uses Standard HTTP Methods

REST relies on **HTTP methods** to define actions:

| Method | Meaning |
|---|---|
| GET | Fetch data |
| POST | Create resource |
| PUT | Replace resource |
| PATCH | Update part of resource |
| DELETE | Remove resource |

👉 We will deep-dive each method separately next.

---

## REST is Stateless (Why It Matters)

Stateless means:
- Server does not store client state
- Every request must contain all required information

Automation implications:
- Tokens must be sent with every request
- Tests should not depend on execution order
- Parallel execution is safer

---

## REST Constraints (Tester-Relevant Only)

REST has multiple constraints; testers only need these:

### 1️⃣ Client–Server
- UI/Test and API server are independent
- Easier to test API without UI

### 2️⃣ Statelessness
- No session memory on server
- Each request stands alone

### 3️⃣ Uniform Interface
- Consistent use of URLs, methods, status codes
- Makes automation predictable

You do NOT need to memorize all REST constraints.

---

## REST vs SOAP (Interview Favorite)

| REST | SOAP |
|---|---|
| Lightweight | Heavy |
| Uses HTTP | Uses XML + protocols |
| JSON common | XML only |
| Faster | Slower |
| Easy automation | Hard automation |

Tester takeaway:
> Most modern automation focuses on REST APIs.

---

## Idempotency (VERY IMPORTANT FOR TESTERS)

Idempotent means:
> Making the same request multiple times gives the same result.

| Method | Idempotent |
|---|---|
| GET | ✅ |
| PUT | ✅ |
| DELETE | ✅ |
| POST | ❌ |

Automation impact:
- Safe retries for idempotent methods
- Be careful retrying POST

---

## REST Error Handling (Conceptual)

REST APIs communicate errors using:
- HTTP status codes
- Error messages in response body

Tester focus:
- Validate correct status code
- Validate meaningful error message
- Do NOT rely on UI error alone

---

## Common Automation Mistakes ❌

- Treating REST like UI flows
- Ignoring HTTP method semantics
- Retrying POST blindly
- Assuming session state exists

---

## Best Practices for Automation Testers ✅

- Think in terms of resources
- Use correct HTTP methods
- Validate status codes strictly
- Design independent API tests
- Prefer API over UI for logic validation

---

## Key Takeaways 🎯

- REST is resource-based
- HTTP methods define actions
- Statelessness enables parallel tests
- Idempotency affects retry logic
- REST is automation-friendly