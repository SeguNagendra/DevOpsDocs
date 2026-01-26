---
sidebar_position: 10
---

## API Authentication & Authorization
### Automation Tester Perspective

Authentication and authorization control **who can access an API and what they are allowed to do**.
Most API test failures in real projects are related to **auth issues**, not business logic.

This section focuses on **how testers use auth**, not how it’s implemented internally.

---

## Authentication vs Authorization

| Concept | Meaning |
|---|---|
| Authentication | Who you are |
| Authorization | What you can do |

Tester rule:
> Authentication happens first, authorization happens next.

---

## Common Authentication Types in APIs

### 1️⃣ No Authentication (Public APIs)

- No token or credentials required
- Rare in enterprise systems

Automation note:
- Easy to test
- High security risk in real apps

---

### 2️⃣ Basic Authentication

```http
Authorization: Basic base64(username:password)
```

Characteristics:
- Simple
- Less secure
- Often used in internal tools

Tester considerations:
- Avoid logging credentials
- Use environment variables

---

### 3️⃣ API Key Authentication

```http
x-api-key: abc123
```

Characteristics:
- Key identifies client
- Often used for rate limiting

Automation pitfalls ❌:
- Hardcoding API keys
- Sharing keys across environments

---

### 4️⃣ Bearer Token Authentication (Most Common)

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...
```

Characteristics:
- Token-based
- Stateless
- Used in most REST APIs

Automation flow:
```
Login API → Token
          ↓
All subsequent API calls
```

---

## Token Handling – Tester Best Practices

- Never hardcode tokens
- Fetch token dynamically
- Store token in variable
- Refresh token when expired
- Mask token in logs

---

## Token Expiry & Refresh (Awareness)

Common issues:
- Token expires mid-test
- Parallel tests reuse expired token

Tester strategies:
- Short-lived tests
- Refresh token logic
- Retry only auth call, not business call

---

## OAuth 2.0 (Awareness Only)

OAuth is commonly used in:
- Enterprise apps
- Third-party integrations

Tester-level understanding:
- Client ID
- Client secret
- Access token

You do NOT need:
- OAuth grant flow internals
- Token signing logic

---

## Authorization (Role-Based Access)

Examples:
- Admin vs User
- Read-only vs Write access

Automation validation:
- Correct status codes (403)
- Access denied messages
- Role-specific behavior

---

## Common Auth-Related Failures ❌

- Missing Authorization header
- Expired token
- Wrong role access
- Token from wrong environment
- Hardcoded credentials

---

## Interview-Ready Questions

**Q: Difference between 401 and 403?**  
A: 401 = authentication failure, 403 = authorization failure.

**Q: How do you handle tokens in automation?**  
A: Generate dynamically and store securely.

---

## Key Takeaways 🎯

- Auth issues are very common
- Bearer tokens are most widely used
- Token handling must be dynamic
- Authorization must be validated separately
- Good auth handling reduces flaky tests