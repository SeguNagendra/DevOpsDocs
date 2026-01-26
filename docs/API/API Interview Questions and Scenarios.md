---
sidebar_position: 16
---

# API Interview Questions and Scenarios

This section consolidates **concepts, decisions, and real-world scenarios** commonly discussed in automation and SDET interviews.
Answers are **concise, practical, and experience-oriented**.

---

## Core Concept Questions

### Q1. What is API testing?
**Answer:**  
API testing validates backend functionality by sending requests directly to APIs and asserting responses, without using the UI.

---

### Q2. Why API testing is preferred over UI testing?
**Answer:**  
API tests are faster, more stable, easier to debug, and can validate business logic directly.

---

### Q3. Where does API testing fit in the test pyramid?
**Answer:**  
Between unit tests and UI tests; more API tests and fewer UI tests lead to a stable automation suite.

---

### Q4. REST vs SOAP?
**Answer:**  
REST is lightweight, uses HTTP methods, commonly JSON-based, and is easier to automate than SOAP.

---

## HTTP Methods & Status Codes

### Q5. Difference between GET and POST?
**Answer:**  
GET retrieves data and is idempotent; POST creates data and is not idempotent.

---

### Q6. PUT vs PATCH?
**Answer:**  
PUT replaces the entire resource; PATCH updates only specific fields.

---

### Q7. Difference between 401 and 403?
**Answer:**  
401 means authentication failure; 403 means authorization failure.

---

### Q8. When do you expect 201 vs 200?
**Answer:**  
201 for successful creation (POST), 200 for successful fetch or update.

---

## Authentication & Security

### Q9. How do you handle authentication in API automation?
**Answer:**  
Generate tokens dynamically using auth APIs, store securely, and reuse across tests.

---

### Q10. What are common auth-related failures?
**Answer:**  
Expired tokens, missing headers, wrong roles, environment mismatch.

---

## JSON & Validation

### Q11. How do you validate JSON responses?
**Answer:**  
Assert status code first, then validate key fields, data types, and business rules using flexible paths.

---

### Q12. Why avoid full JSON comparison?
**Answer:**  
It makes tests fragile due to dynamic fields like timestamps and IDs.

---

## API + Database Scenarios

### Q13. Why validate database after API call?
**Answer:**  
API response confirms processing; DB validation confirms persistence.

---

### Q14. How do you handle async API behavior?
**Answer:**  
Use polling with timeout, avoid hard sleeps, and validate final committed state.

---

## CI CD & Stability

### Q15. Why API tests fail in CI but pass locally?
**Answer:**  
Environment differences, missing secrets, parallel data collision, timing issues.

---

### Q16. Should API tests run before UI tests in CI?
**Answer:**  
Yes, because API tests are faster and catch backend issues early.

---

## Scenario-Based Questions

### Scenario 1: POST API returns 200 but DB has no data
**Possible reasons:**
- Async processing
- Transaction rollback
- Wrong schema queried

---

### Scenario 2: Random failures in parallel execution
**Root causes:**
- Shared test data
- Non-idempotent APIs
- Missing data isolation

---

### Scenario 3: DELETE API returns success but data still exists
**Explanation:**
- Soft delete implementation
- Validate status flag instead of row deletion

---

## Design & Best Practices

### Q17. What makes a good API automation test?
**Answer:**  
Independent, deterministic, environment-agnostic, and focused on business validation.

---

### Q18. What should not be automated at API level?
**Answer:**  
Pure UI validations, third-party APIs (unless mocked), non-critical endpoints.

---

## Strong Closing Statement (Interview Gold)

> “I use API testing to validate business logic early, reduce UI flakiness, and ensure backend correctness with DB validation where required.”

---

## Key Takeaways

- Interviews focus on reasoning, not syntax
- Status codes drive decisions
- API + DB validation shows seniority
- CI awareness is critical
- Clean design prevents flakiness