---
sidebar_position: 4
---

## HTTP Methods – Deep Dive (GET & POST)
### Automation Tester Perspective

HTTP methods define **what action an API performs**.
Using the wrong method or misunderstanding its behavior is a **very common automation mistake**.

This section deep-dives into **GET and POST**, the two most frequently used methods.

---

# 1️⃣ GET Method

## What is GET?

`GET` is used to **retrieve data** from the server.

Example:
```http
GET /users/101
```

Meaning:
> “Give me the details of user 101”

---

## Key Characteristics of GET

| Aspect | Behavior |
|---|---|
| Purpose | Fetch data |
| Request Body | ❌ Not allowed |
| Side Effects | ❌ None |
| Safe | ✅ Yes |
| Idempotent | ✅ Yes |
| Cacheable | ✅ Yes |

---

## GET Request Structure

```http
GET /orders?status=SUCCESS
Headers:
Authorization: Bearer token
```

Components:
- URL
- Query parameters
- Headers

---

## Automation Use Cases for GET

- Fetch user details
- Get order status
- Validate payment history
- Verify data created by POST/PUT

Example validation:
- Status code = 200
- Response body contains expected fields
- DB data matches API response

---

## Common GET Status Codes

| Code | Meaning |
|---|---|
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not found |
| 500 | Server error |

---

## Common GET Mistakes ❌

- Sending request body
- Using GET to create/update data
- Hardcoding query params
- Ignoring pagination

---

## GET Interview Question

**Q: Is GET idempotent?**  
A: Yes. Multiple GET requests return the same result without side effects.

---

# 2️⃣ POST Method

## What is POST?

`POST` is used to **create a new resource**.

Example:
```http
POST /users
```

Meaning:
> “Create a new user”

---

## Key Characteristics of POST

| Aspect | Behavior |
|---|---|
| Purpose | Create resource |
| Request Body | ✅ Required |
| Side Effects | ✅ Yes |
| Safe | ❌ No |
| Idempotent | ❌ No |
| Cacheable | ❌ No |

---

## POST Request Structure

```http
POST /orders
Headers:
Content-Type: application/json
Authorization: Bearer token

Body:
{
  "userId": 101,
  "amount": 500
}
```

---

## Automation Use Cases for POST

- Create user
- Place order
- Trigger payment
- Submit form data

Validation includes:
- Status code (201)
- Response body
- DB record creation

---

## Common POST Status Codes

| Code | Meaning |
|---|---|
| 201 | Created |
| 400 | Invalid input |
| 401 | Unauthorized |
| 409 | Conflict (duplicate) |
| 500 | Server error |

---

## POST Idempotency Trap ⚠️

Retrying POST may:
- Create duplicate data
- Break test environment

Automation rule:
> Never blindly retry POST requests.

---

## Common POST Mistakes ❌

- Missing Content-Type header
- Sending invalid JSON
- Retrying POST automatically
- Not validating DB side effects

---

## POST Interview Question

**Q: Why is POST not idempotent?**  
A: Because multiple POST requests can create multiple resources.

---

## GET vs POST (Quick Comparison)

| Aspect | GET | POST |
|---|---|---|
| Purpose | Read | Create |
| Request Body | ❌ | ✅ |
| Idempotent | ✅ | ❌ |
| Safe | ✅ | ❌ |

---

## Key Takeaways 🎯

- GET = read-only
- POST = create resource
- GET is safe & idempotent
- POST causes side effects
- Automation must treat POST carefully