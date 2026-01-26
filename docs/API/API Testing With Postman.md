---
sidebar_position: 11
---

# API Testing with Postman
### Automation Tester Perspective

Postman is the **most widely used tool** for manual and exploratory API testing.
For automation testers, Postman is used to **understand APIs, debug issues, and design automation-ready tests**.

---

## Why Testers Use Postman

- Explore APIs quickly
- Validate request/response behavior
- Debug authentication issues
- Design test scenarios before automation
- Share collections with team

Postman is **not a replacement for automation**, but a **foundation**.

---

## Core Postman Concepts

### Workspace
Logical area to organize APIs.

### Collection
A group of related API requests.

Example:
- User APIs
- Order APIs
- Payment APIs

---

## Creating a Request

Each request has:
- Method (GET, POST, etc.)
- URL
- Headers
- Params
- Body

Tester tip:
> Always start with **GET** to understand the response.

---

## Environments (VERY IMPORTANT)

Environments store **variables**.

Example:
```
baseUrl = https://qa.api.com
token = {{authToken}}
```

Benefits:
- Environment switching (DEV / QA / PROD)
- No hardcoding
- Cleaner requests

---

## Variables in Postman

Types:
- Global
- Environment
- Collection
- Local

Automation rule:
> Use **environment or collection variables**, not globals.

---

## Authorization in Postman

- Basic Auth
- API Key
- Bearer Token

Best practice:
- Generate token using login API
- Save token to variable
- Reuse in all requests

---

## Pre-request Scripts

Used to:
- Generate dynamic data
- Fetch tokens
- Set variables

Example use cases:
- Timestamp-based values
- Random emails
- Token refresh

---

## Tests Tab (Assertions)

Postman allows basic assertions using JavaScript.

Common checks:
- Status code
- Response time
- Field existence
- Value validation

Automation mindset:
> Design assertions similar to how you’ll assert in code.

---

## Chaining APIs (Critical Skill)

Flow:
```
API 1 → Extract value → API 2
```

Example:
- Create user → Get userId → Fetch user

This mirrors **real automation flows**.

---

## Collection Runner

Used to:
- Run multiple requests
- Data-driven testing (CSV/JSON)
- Basic regression checks

Limitations:
- Not ideal for large suites
- Limited control vs automation frameworks

---

## Common Postman Mistakes ❌

- Hardcoding URLs/tokens
- Using globals excessively
- Ignoring environments
- Over-relying on Postman for regression

---

## Best Practices for Automation Testers ✅

- Use Postman for exploration
- Finalize API behavior
- Move stable tests to automation
- Keep Postman collections clean
- Version control collections (export)

---

## Interview-Ready Questions

**Q: Why use Postman if you automate APIs?**  
A: To explore, debug, and design automation-ready tests.

**Q: Difference between Postman and RestAssured?**  
A: Postman is a tool; RestAssured is a code-based automation library.

---

## Key Takeaways 🎯

- Postman is for exploration & debugging
- Environments prevent hardcoding
- Chaining builds real flows
- Automation mindset starts in Postman
- Stable APIs move to code automation