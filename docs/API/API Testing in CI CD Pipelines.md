---
sidebar_position: 14
---

# API Testing in CI CD Pipelines

Running API tests locally is not enough.
Modern automation requires **API tests to run reliably in CI/CD pipelines** with proper configuration, reporting, and failure analysis.

This section explains **how API automation fits into CI/CD**, from a practical tester perspective.

---

## Why Run API Tests in CI CD?

Benefits:
- Early bug detection
- Faster feedback than UI tests
- Stable execution (no browser dependency)
- Easy parallelization
- Backend confidence before UI tests

Best practice:
> **API tests should run before UI tests in CI pipelines**

---

## Typical CI Flow for API Testing

```
Code Commit
   ↓
Build (Maven)
   ↓
API Tests
   ↓
UI Tests
   ↓
Deployment
```

If API tests fail → pipeline should stop.

---

## Running API Tests with Maven

Common command:
```bash
mvn clean test
```

With TestNG suite:
```bash
mvn clean test -DsuiteXmlFile=testng-api.xml
```

Advantages:
- Consistent execution
- Easy CI integration
- Environment independent

---

## Environment Handling in CI

Never hardcode:
- Base URLs
- Tokens
- Credentials

Use:
- Maven profiles
- Environment variables
- CI secrets

Example:
```bash
mvn test -Denv=qa
```

---

## Authentication in CI

Best practices:
- Generate tokens dynamically
- Store secrets in CI vault
- Mask sensitive logs
- Avoid committing credentials

Common mistake ❌:
- Using locally generated tokens in CI

---

## Parallel Execution for API Tests

API tests are ideal for parallel execution.

Options:
- TestNG parallel methods
- Parallel classes
- CI-level parallel jobs

Caution:
- Ensure test data isolation
- Avoid shared state

---

## Reporting in CI

Common reporting options:
- TestNG reports
- Extent reports
- CI-native test reports

Good reports should show:
- Failed API
- Request & response
- Status codes
- Error messages

---

## Handling Failures in CI

When API tests fail:
1. Check status codes
2. Review request/response logs
3. Verify environment variables
4. Check DB or downstream services

Avoid:
- Blind retries
- Ignoring flaky failures

---

## Common CI Issues ❌

| Issue | Cause |
|---|---|
| 401 errors | Missing secrets |
| Random failures | Parallel collision |
| Timeouts | Slow backend |
| Works locally, fails in CI | Env mismatch |

---

## Best Practices ✅

- Run API tests early
- Keep API suite fast
- Fail pipeline on critical failures
- Separate API & UI jobs
- Keep logs readable

---

## Interview-Ready Explanation

**Q: Why run API tests in CI before UI tests?**  
A: API tests are faster, more stable, and catch backend issues early.

---

## Key Takeaways 🎯

- CI execution is mandatory for API automation
- Maven + TestNG integrate easily
- Proper env handling is critical
- Parallel execution boosts speed
- CI failures need structured debugging