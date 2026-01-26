---
sidebar_position: 8
---

## API Request Components – Headers, Path Params & Query Params
### Automation Tester Perspective

Every API request is built from **multiple components**.
Most API automation bugs happen because **one of these components is misunderstood or misused**.

This section explains each component clearly, with tester-focused rules.

---

## 1️⃣ URL & Endpoint (Quick Recap)

Example:
```http
GET /users/101/orders?status=SUCCESS
```

Breakdown:
- `/users/101/orders` → Path
- `?status=SUCCESS` → Query parameter

---

## 2️⃣ Path Parameters

### What are Path Params?

Path parameters identify a **specific resource**.

Example:
```http
GET /users/101
```

Here:
- `101` is a path parameter

---

### Characteristics of Path Params

| Aspect | Behavior |
|---|---|
| Purpose | Identify resource |
| Mandatory | ✅ Yes |
| Order matters | ✅ Yes |
| Part of URL | ✅ Yes |

---

### Automation Use Cases

- Fetch specific user
- Update specific order
- Delete a resource

Validation:
- Correct resource returned
- 404 for invalid IDs

---

### Common Path Param Mistakes ❌

- Passing invalid ID format
- Using query param instead of path param
- Hardcoding IDs across tests

---

## 3️⃣ Query Parameters

### What are Query Params?

Query parameters **filter or modify the response**.

Example:
```http
GET /orders?status=SUCCESS&limit=10
```

---

### Characteristics of Query Params

| Aspect | Behavior |
|---|---|
| Purpose | Filter, sort, paginate |
| Mandatory | ❌ Usually optional |
| Order matters | ❌ No |
| Part of URL | ✅ Yes |

---

### Common Automation Use Cases

- Pagination (`page`, `limit`)
- Filtering (`status`, `type`)
- Sorting (`sort=createdDate`)

---

### Common Query Param Mistakes ❌

- Forgetting encoding
- Assuming order matters
- Missing default values
- Hardcoding pagination

---

## 4️⃣ Headers (VERY IMPORTANT)

### What are Headers?

Headers carry **metadata** about the request.

Example:
```http
Headers:
Content-Type: application/json
Authorization: Bearer token
```

---

### Common Headers Testers Must Know

| Header | Purpose |
|---|---|
| Content-Type | Request body format |
| Accept | Expected response format |
| Authorization | Auth token |
| Cache-Control | Caching behavior |
| Custom headers | App-specific logic |

---

### Content-Type vs Accept (Interview Favorite)

| Header | Meaning |
|---|---|
| Content-Type | Format of request body |
| Accept | Expected response format |

---

### Header Automation Mistakes ❌

- Missing Content-Type
- Wrong token placement
- Hardcoding auth headers
- Ignoring custom headers

---

## 5️⃣ Request Body (Preview)

Body contains the **payload** sent to server.

Example:
```json
{
  "userId": 101,
  "amount": 500
}
```

We’ll cover body & JSON deeply in the **next section**.

---

## Parameter Comparison (Important)

| Aspect | Path Param | Query Param |
|---|---|---|
| Purpose | Identify resource | Filter data |
| Mandatory | Yes | Usually No |
| Order matters | Yes | No |
| Used for | CRUD | Search & pagination |

---

## Automation Best Practices ✅

- Always verify correct param usage
- Externalize IDs and params
- Log full request on failure
- Avoid hardcoding values
- Validate negative param scenarios

---

## Interview-Ready Questions

**Q: Difference between path and query parameters?**  
A: Path identifies resource; query filters data.

**Q: What happens if Content-Type is missing?**  
A: Server may reject or misinterpret request.

---

## Key Takeaways 🎯

- API requests have multiple components
- Path params identify resources
- Query params filter results
- Headers carry metadata & auth
- Small mistakes cause major failures