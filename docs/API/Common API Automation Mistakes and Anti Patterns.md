---
sidebar_position: 15
---

# Common API Automation Mistakes and Anti Patterns

Even well-written API tests can become **flaky, slow, or unreliable** if common mistakes are made.
This section highlights **real-world API automation anti-patterns** and how to avoid them.

---

## 1️⃣ Hardcoding Values ❌

### Problem
- Hardcoded URLs
- Hardcoded tokens
- Hardcoded IDs

Why it fails:
- Tests break across environments
- Security risk
- Not CI-friendly

### Correct Approach ✅
- Use environment variables
- Parameterize data
- Generate values dynamically

---

## 2️⃣ Ignoring Status Codes ❌

### Problem
- Validating response body without checking status code

Why it fails:
- False positives
- Misleading assertions

### Correct Approach ✅
Always assert:
```text
Status Code → Headers → Body
```

---

## 3️⃣ Blind Retries ❌

### Problem
- Retrying POST or PUT automatically

Why it fails:
- Duplicate data
- Data corruption

### Correct Approach ✅
- Retry only idempotent calls (GET, PUT)
- Investigate root cause first

---

## 4️⃣ Over Validating Responses ❌

### Problem
- Comparing full JSON response
- Validating every field

Why it fails:
- Fragile tests
- Breaks on non-functional changes

### Correct Approach ✅
- Validate only business-critical fields
- Ignore dynamic fields (timestamps, IDs)

---

## 5️⃣ Ignoring Async Behavior ❌

### Problem
- Validating DB immediately after API call

Why it fails:
- Flaky tests
- False failures

### Correct Approach ✅
- Use polling
- Implement retry with timeout
- Avoid fixed sleeps

---

## 6️⃣ Poor Test Data Strategy ❌

### Problem
- Shared test data
- No cleanup
- Environment pollution

Why it fails:
- Random failures
- Unreliable CI runs

### Correct Approach ✅
- Isolated test data
- Cleanup after tests
- Unique identifiers

---

## 7️⃣ Mixing Test Logic and Setup ❌

### Problem
- Auth logic inside every test
- Repeated setup code

Why it fails:
- Hard to maintain
- Duplicate code

### Correct Approach ✅
- Centralize setup
- Use base classes
- Reuse utilities

---

## 8️⃣ Treating API Tests Like UI Tests ❌

### Problem
- Sequential dependency
- Order-based tests

Why it fails:
- Parallel execution breaks tests

### Correct Approach ✅
- Independent tests
- Stateless design

---

## 9️⃣ Ignoring Security Scenarios ❌

### Problem
- Testing only happy paths

Why it fails:
- Security bugs slip through

### Correct Approach ✅
- Missing auth
- Invalid roles
- Expired tokens

---

## 🔟 Poor Logging ❌

### Problem
- No request/response logs

Why it fails:
- Hard debugging in CI

### Correct Approach ✅
- Log on failure
- Mask sensitive data
- Capture headers & body

---

## Interview Perspective 🎯

Most interviewers ask:
> “What mistakes have you seen in API automation?”

Strong answer:
- Hardcoding
- Blind retries
- Poor data handling
- Ignoring async behavior

---

## Key Takeaways 🎯

- Most API failures are design issues
- Small mistakes cause big flakiness
- Clean design > more tests
- Anti-pattern awareness = senior skill