---
sidebar_position: 5
---

## HTTP Methods – Deep Dive (PUT, PATCH & DELETE)
### Automation Tester Perspective

PUT, PATCH, and DELETE are used to **modify or remove data**.
Automation testers must understand these deeply because mistakes here often cause:
- Data corruption
- Flaky tests
- Environment pollution

---

# 3️⃣ PUT Method

## What is PUT?

`PUT` is used to **fully replace an existing resource**.

Example:
```http
PUT /users/101
```

Meaning:
> “Replace the entire user 101 with the provided data”

---

## Key Characteristics of PUT

| Aspect | Behavior |
|---|---|
| Purpose | Full update |
| Request Body | ✅ Required |
| Side Effects | ✅ Yes |
| Safe | ❌ No |
| Idempotent | ✅ Yes |
| Cacheable | ❌ No |

---

## PUT Request Example

```http
PUT /users/101
Content-Type: application/json

{
  "name": "John",
  "email": "john@gmail.com",
  "status": "ACTIVE"
}
```

⚠️ Missing fields may be **removed** after PUT.

---

## Automation Use Cases for PUT

- Update entire profile
- Replace configuration
- Reset resource state

Validation:
- Status code = 200 / 204
- All fields updated correctly
- DB reflects full replacement

---

## Common PUT Mistakes ❌

- Assuming partial update
- Sending incomplete payload
- Confusing PUT with PATCH

---

## PUT Interview Question

**Q: Is PUT idempotent?**  
A: Yes. Multiple PUT requests result in the same state.

---

# 4️⃣ PATCH Method

## What is PATCH?

`PATCH` is used to **partially update a resource**.

Example:
```http
PATCH /users/101
```

Meaning:
> “Update only specified fields of user 101”

---

## Key Characteristics of PATCH

| Aspect | Behavior |
|---|---|
| Purpose | Partial update |
| Request Body | ✅ Required |
| Side Effects | ✅ Yes |
| Safe | ❌ No |
| Idempotent | ⚠️ Depends |
| Cacheable | ❌ No |

---

## PATCH Request Example

```http
PATCH /users/101
Content-Type: application/json

{
  "status": "BLOCKED"
}
```

Only `status` is updated; other fields remain unchanged.

---

## PUT vs PATCH (CRITICAL COMPARISON)

| Aspect | PUT | PATCH |
|---|---|---|
| Update type | Full replace | Partial |
| Missing fields | Removed | Retained |
| Idempotent | ✅ | ⚠️ |
| Risk | High | Medium |

Tester rule:
> Use PATCH when available to avoid data loss.

---

## PATCH Interview Question

**Q: Why was PATCH introduced?**  
A: To allow partial updates without replacing the entire resource.

---

# 5️⃣ DELETE Method

## What is DELETE?

`DELETE` is used to **remove a resource**.

Example:
```http
DELETE /users/101
```

Meaning:
> “Remove user 101”

---

## Key Characteristics of DELETE

| Aspect | Behavior |
|---|---|
| Purpose | Remove resource |
| Request Body | ❌ Rare |
| Side Effects | ✅ Yes |
| Safe | ❌ No |
| Idempotent | ✅ Yes |
| Cacheable | ❌ No |

---

## DELETE – Hard vs Soft Delete (Awareness)

- **Hard delete** → Row removed from DB
- **Soft delete** → Status flag updated (most common)

Tester implication:
- DELETE may not remove DB row
- Validate status instead of existence

---

## Automation Use Cases for DELETE

- Cleanup test data
- Remove temporary resources
- Negative scenario testing

Validation:
- Status code = 200 / 204
- Resource inaccessible afterwards
- DB reflects expected delete behavior

---

## Common DELETE Mistakes ❌

- Assuming hard delete
- Reusing deleted IDs
- Running DELETE in shared envs

---

## DELETE Interview Question

**Q: Is DELETE idempotent?**  
A: Yes. Deleting the same resource multiple times has the same effect.

---

## Key Takeaways 🎯

- PUT replaces entire resource
- PATCH updates partial fields
- DELETE removes resource (often soft)
- PUT & DELETE are idempotent
- PATCH is safer for partial updates