---
sidebar_position: 5
---

# Architecture Overview – How SonarQube Works Internally

To use SonarQube confidently in real projects, especially in DevOps and production environments,
it is important to understand **how SonarQube works internally**.

This chapter explains the architecture in a **simple, practical way**, without unnecessary complexity.

---

## Why Architecture Understanding Matters

Many SonarQube issues happen because of misunderstandings like:
- Why scans succeed but results don’t appear
- Why the UI is slow
- Why Quality Gates don’t update in CI

All of these become easy to troubleshoot once you understand the architecture.

---

## High-Level Components of SonarQube

SonarQube is made up of four main components:

1. **Sonar Scanner**
2. **SonarQube Server**
3. **Database**
4. **Web User Interface**

Each component has a clear responsibility.

---

## Sonar Scanner – Close to the Code

The Sonar Scanner:
- Runs where your source code lives
- Reads files and applies rules
- Generates analysis results

Important points:
- The scanner does not store results
- The scanner does not enforce Quality Gates
- The scanner only sends data to the server

Think of the scanner as a **data collector**.

---

## SonarQube Server – The Brain

The SonarQube Server:
- Receives analysis data from scanners
- Processes rules and metrics
- Evaluates Quality Gates
- Coordinates storage and indexing

The server is responsible for **decision-making**, not scanning.

---

## Database – The Source of Truth

The database stores:
- Issues
- Metrics
- Quality Gate status
- Configuration
- User and permission data

PostgreSQL is recommended for production because of:
- Stability
- Performance
- Supportability

⚠️ Never modify the database manually.

---

## Elasticsearch – Fast Search & UI Performance

Elasticsearch is used to:
- Index analysis results
- Enable fast searching in the UI
- Power dashboards and filtering

Many performance problems are caused by:
- Insufficient memory for Elasticsearch
- Disk I/O limitations

These are infrastructure issues, not rule problems.

---

## Web UI – Visibility Layer

The Web UI:
- Displays project dashboards
- Shows issues and metrics
- Allows configuration and administration

The UI reads data from the server, not directly from scanners.

---

## Data Flow – End-to-End Picture

Understanding the data flow helps debugging:

```
Source Code
   ↓
Sonar Scanner
   ↓
SonarQube Server
   ↓
Database + Elasticsearch
   ↓
Web UI
```

If something breaks, this flow helps identify **where** the issue is.

---

## Common Architecture Misconceptions

Avoid these misunderstandings:

- “Scanner keeps history” → ❌
- “DB can be edited to fix issues” → ❌
- “UI calculates metrics” → ❌

All calculations happen on the **server side**.

---

## Key Takeaway

SonarQube is a **distributed system**, not a single tool.

Understanding the responsibilities of each component:
- Simplifies troubleshooting
- Improves production reliability
- Makes CI/CD integration clearer

---

➡️ **Next:** Sonar Scanner Deep Dive  
