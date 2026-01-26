---
sidebar_position: 1
---

# Logs Architecture & Ingestion

> *“Metrics tell you something is wrong. Logs tell you exactly what went wrong.”*

This module belongs to **PHASE 8: Logs Management**.  
Here we focus on **how logs enter Datadog**, how they are structured, and why ingestion design matters for **cost and usability**.

---

## What Is a Log?

A **log** is a timestamped record of an event.

Logs typically contain:
- Timestamp
- Log level (INFO, WARN, ERROR)
- Message
- Context (service, host, request)

Logs answer:
> *What exactly happened at this moment?*

---

## Why Logs Matter in Production

When something breaks:
- Metrics show symptoms
- Logs show causes

Logs are essential for:
- Debugging errors
- Investigating incidents
- Auditing actions

Without logs:
> You are guessing under pressure.

---

## Logs in Datadog (Big Picture)

Datadog log management includes:
- Log collection
- Processing & enrichment
- Indexing
- Search & analytics
- Archiving

Each stage affects:
- Cost
- Performance
- Troubleshooting speed

---

## Log Ingestion Flow (High Level)

A typical log flow:

1. Application or system generates logs
2. Datadog Agent or integration collects logs
3. Logs are enriched with tags
4. Logs are processed and indexed
5. Logs become searchable in the UI

Understanding this flow helps:
> Avoid missing logs and surprise bills.

---

## Log Collection Methods

Datadog supports multiple log sources.

### Agent-Based Collection
- Most common method
- Works on hosts and containers
- Supports file and stream logs

### Container & Kubernetes Logs
- Automatically collected
- Metadata added automatically
- Scales with workloads

### Cloud Provider Logs
- Pulled from cloud services
- Useful for managed services

---

## Structured vs Unstructured Logs

### Unstructured Logs
- Plain text
- Harder to search

### Structured Logs
- Key-value format (JSON)
- Easy to filter and analyze

Best practice:
> Always prefer structured logs.

---

## Tags on Logs

Tags are critical for logs.

Tags allow:
- Filtering by service
- Separating environments
- Correlating with metrics and traces

Examples:
- `env:prod`
- `service:checkout`
- `team:payments`

Good tagging turns logs into data.

---

## Log Volume Awareness

Logs can grow fast.

High log volume causes:
- Increased cost
- Slower searches
- Noise

Best practices:
- Log what matters
- Avoid excessive debug logs in prod
- Sample noisy logs when possible

---

## Common Log Ingestion Mistakes

❌ Collecting all logs blindly  
❌ No tagging strategy  
❌ Using only unstructured logs  
❌ Ignoring log volume growth  

---

## Why This Module Matters

Good log ingestion design:
- Reduces cost
- Improves debugging
- Keeps systems observable

Bad log ingestion design:
- Creates noise
- Hides real issues
- Increases spend

---

## Key Takeaways

- Logs provide detailed context
- Ingestion design matters
- Structured logs are powerful
- Tags enable correlation
- Volume must be controlled

---

➡️ **Next Module:** Log Processing & Pipelines
