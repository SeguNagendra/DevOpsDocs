---
sidebar_position: 6
---

## HTTP Methods – HEAD & OPTIONS (Awareness + Debugging)
### Automation Tester Perspective

HEAD and OPTIONS are **not used daily** by automation testers, but they are **extremely important for debugging, security checks, and interviews**.

---

# 6️⃣ HEAD Method

## What is HEAD?

`HEAD` is similar to `GET`, but it **returns only headers, not the response body**.

Example:
```http
HEAD /users/101
```

Meaning:
> “Check if the resource exists and return metadata, without fetching the body.”

---

## Key Characteristics of HEAD

| Aspect | Behavior |
|---|---|
| Purpose | Metadata check |
| Request Body | ❌ Not allowed |
| Response Body | ❌ Not returned |
| Safe | ✅ Yes |
| Idempotent | ✅ Yes |
| Cacheable | ✅ Yes |

---

## When Testers Use HEAD

- Check resource existence
- Validate authentication/authorization
- Measure response time without payload
- Debug caching issues

Example use case:
- Verify file exists before download
- Validate API availability

---

## HEAD vs GET (Important Difference)

| Aspect | HEAD | GET |
|---|---|---|
| Response body | ❌ No | ✅ Yes |
| Performance | Faster | Slower |
| Use case | Check availability | Fetch data |

Tester rule:
> Use HEAD when you don’t need the data, only the status.

---

## Common HEAD Mistakes ❌

- Expecting response body
- Using HEAD for data validation
- Ignoring HEAD in API debugging

---

# 7️⃣ OPTIONS Method

## What is OPTIONS?

`OPTIONS` returns the **allowed HTTP methods** for a resource.

Example:
```http
OPTIONS /users
```

Meaning:
> “What operations are allowed on this endpoint?”

---

## Key Characteristics of OPTIONS

| Aspect | Behavior |
|---|---|
| Purpose | Discover allowed methods |
| Request Body | ❌ |
| Safe | ✅ |
| Idempotent | ✅ |

---

## OPTIONS & CORS (Very Important)

OPTIONS is heavily used in **CORS preflight requests**.

Browser flow:
```
Browser
 ↓
OPTIONS (preflight)
 ↓
API Server
 ↓
Allowed methods & headers
```

If OPTIONS fails:
- UI/API calls may fail
- Automation may see unexpected 403/405 errors

---

## Automation Use Cases for OPTIONS

- Debug CORS issues
- Validate allowed methods
- Security testing (method exposure)
- Environment comparison

---

## Common OPTIONS Mistakes ❌

- Ignoring OPTIONS failures
- Not understanding CORS preflight
- Assuming all methods are allowed

---

## Interview Questions

**Q: Why is OPTIONS used?**  
A: To identify allowed HTTP methods and support CORS preflight checks.

**Q: Difference between GET and HEAD?**  
A: HEAD returns headers only, GET returns headers + body.

---

## Key Takeaways 🎯

- HEAD checks metadata without body
- OPTIONS lists allowed methods
- Both are safe & idempotent
- Critical for debugging & interviews
- Often involved in CORS issues