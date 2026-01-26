---
sidebar_position: 2
---

## API Architecture Basics (Automation Tester Perspective)

Before testing APIs, automation testers must understand **how APIs work internally**.
This section explains **API architecture in simple terms**, focused on **how testers observe, validate, and debug issues**.

---

## Client–Server Architecture

APIs follow a **client–server model**.

- **Client**: UI, mobile app, another service, or automation test
- **Server**: API service that processes requests

```
Client (UI / Test / Postman)
            ↓
        API Server
            ↓
        Database
```

Automation tests usually act as the **client**.

---

## Request–Response Cycle (Core Concept)

Every API interaction follows this cycle:

```
Request  →  Processing  →  Response
```

### Request Contains:
- HTTP method (GET, POST, etc.)
- URL (endpoint)
- Headers
- Body (optional)

### Response Contains:
- Status code
- Headers
- Body (JSON/XML)

Tester focus:
> Validate both **response correctness** and **side effects** (DB changes).

---

## Stateless Nature of APIs

Most REST APIs are **stateless**.

Meaning:
- Each request is independent
- Server does not remember previous requests
- All required data must be sent in the request

Automation implication:
- Tokens must be sent every time
- Tests should not rely on execution order
- Parallel execution becomes easier

---

## Synchronous vs Asynchronous APIs

### Synchronous APIs
- Client waits for response
- Immediate result

Example:
```text
Create user → Response returned immediately
```

### Asynchronous APIs
- Client gets acknowledgment
- Actual processing happens later

Example:
```text
Trigger payment → Response OK → DB update later
```

Tester implication:
- DB validation may require wait/retry
- Immediate assertions may fail

---

## API Layer in Real Applications

```
UI
 ↓
API Layer
 ↓
Business Logic
 ↓
Database
```

Automation testers commonly validate:
- API response
- Business rules
- Database state

Best practice:
> Validate **API + DB together** for critical flows.

---

## Monolithic vs Microservices APIs (Awareness)

### Monolithic
- Single API service
- Shared database

### Microservices
- Multiple APIs
- Each service owns its data

Tester awareness:
- One UI action may trigger multiple APIs
- DB changes may span multiple services

---

## Common Automation Issues Explained by Architecture

| Issue | Architectural Reason |
|---|---|
| Data not visible immediately | Async processing |
| Random failures | Stateless + timing |
| Duplicate data | Non-idempotent APIs |
| Flaky tests | Parallel requests |

---

## Tester Best Practices Based on Architecture

- Treat every request independently
- Do not assume execution order
- Handle async behavior properly
- Validate backend state, not just response
- Log full request & response

---

## Key Takeaways 🎯

- APIs follow client–server model
- Request–response cycle is fundamental
- APIs are stateless
- Async APIs cause timing issues
- Architecture understanding reduces flaky tests