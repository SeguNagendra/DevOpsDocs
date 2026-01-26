---
sidebar_position: 7
---

## HTTP Status Codes – Deep Dive (Automation Tester Perspective)

HTTP status codes tell you **what happened to your API request**.
For automation testers, status codes are the **first and most important assertion**.

This section covers **what to validate, why it matters, and common traps**.

---

## Why Status Codes Matter

- Fast validation without parsing body
- Clear success vs failure signal
- Standardized across APIs
- Primary indicator in CI failures

Golden rule:
> **Always assert status code before validating response body**

---

## Status Code Categories

| Category | Meaning |
|---|---|
| 1xx | Informational (rare) |
| 2xx | Success |
| 3xx | Redirection |
| 4xx | Client errors |
| 5xx | Server errors |

Automation focus is mainly on **2xx, 4xx, and 5xx**.

---

# ✅ 2xx – Success Codes

### 200 OK
- Request processed successfully
- Common for GET, PUT, PATCH

Automation check:
- Body present
- Data correctness

---

### 201 Created
- Resource successfully created
- Common for POST

Automation check:
- New ID present
- DB row created

---

### 204 No Content
- Success with no response body
- Common for DELETE

Automation check:
- No body expected
- Validate side effects (DB/state)

---

# ❌ 4xx – Client Error Codes

Client sent an invalid request.

### 400 Bad Request
- Invalid input
- Missing fields
- Invalid format

Tester use:
- Negative testing
- Input validation checks

---

### 401 Unauthorized
- Missing or invalid authentication

Tester check:
- Token missing/expired
- Correct auth mechanism used

---

### 403 Forbidden
- Authenticated but no permission

Tester insight:
- Role-based access issue

---

### 404 Not Found
- Resource does not exist

Tester use:
- Invalid ID scenarios
- Delete validation

---

### 409 Conflict
- Duplicate data
- Resource state conflict

Common in:
- Duplicate POST
- Idempotency issues

---

### 422 Unprocessable Entity
- Valid format but business rule violation

Tester insight:
- Business validation failures

---

# 💥 5xx – Server Error Codes

Server failed to process valid request.

### 500 Internal Server Error
- Unhandled exception
- Backend bug

Tester action:
- Capture request/response
- Report as backend defect

---

### 502 Bad Gateway
- Upstream service failure

Common in:
- Microservices
- Downstream dependency issues

---

### 503 Service Unavailable
- Server overloaded or down

Tester insight:
- Infra issue, not functional bug

---

## Status Codes vs Automation Decisions

| Code | Test Result |
|---|---|
| Expected 2xx | PASS |
| Expected 4xx | PASS (negative case) |
| Unexpected 4xx | FAIL |
| Any 5xx | FAIL |

---

## Common Automation Mistakes ❌

- Ignoring status code
- Validating body before status
- Treating 4xx as failures always
- Retrying on 5xx without investigation

---

## Interview-Ready Questions

**Q: Difference between 401 and 403?**  
A: 401 = not authenticated, 403 = authenticated but not authorized.

**Q: When do you expect 422?**  
A: When business validation fails.

**Q: Should automation retry on 500?**  
A: No, it indicates server-side issue.

---

## Key Takeaways 🎯

- Status codes are primary assertions
- 2xx = success, 4xx = client issue, 5xx = server issue
- Negative tests expect 4xx
- 5xx always indicates a problem
- Strong status code validation improves test reliability