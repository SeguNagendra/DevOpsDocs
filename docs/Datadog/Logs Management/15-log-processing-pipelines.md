---
sidebar_position: 2
---

# Log Processing & Pipelines

> *“Raw logs are noise. Processed logs are insight.”*

This module belongs to **PHASE 8: Logs Management**.  
Here we focus on **how logs are transformed after ingestion** so they become searchable, structured, and useful for alerts and analysis.

---

## What Is Log Processing?

Log processing is the step where Datadog:
- Parses raw log messages
- Extracts useful fields
- Enriches logs with metadata
- Routes logs to the right place

Without processing:
> Logs are just text — hard to search and harder to analyze.

---

## What Is a Log Pipeline?

A **log pipeline** is an ordered set of rules that process logs.

Each pipeline:
- Matches specific logs
- Applies processors in sequence
- Outputs structured logs

Think of pipelines as:
> *Assembly lines for logs.*

---

## How Pipelines Work (High Level)

Conceptually:

1. Log enters Datadog
2. Pipeline checks if it matches
3. Processors run in order
4. Fields are extracted or modified
5. Log is indexed or archived

Order matters:
> First match wins, processors run sequentially.

---

## Common Log Processors

### Parsing Processors
Used to extract fields.

Examples:
- Grok parser
- JSON parser

They turn:
```
"GET /checkout 500 123ms"
```
into structured fields:
- status_code
- path
- latency

---

### Enrichment Processors

Used to add context.

Examples:
- Add service name
- Add environment
- Add team ownership

Enrichment improves:
- Filtering
- Correlation
- Alert routing

---

### Transformation Processors

Used to:
- Rename fields
- Drop fields
- Mask sensitive data

Critical for:
- Security
- Compliance
- Cost control

---

## Structured Logs (Why They Matter)

Structured logs:
- Use key-value pairs
- Are machine-readable
- Enable powerful queries

Best practice:
> Emit JSON logs from applications whenever possible.

---

## Pipelines and Cost Control

Processing affects cost indirectly.

Good pipelines:
- Drop useless logs early
- Remove noisy fields
- Normalize data

Bad pipelines:
- Index everything
- Keep unused fields
- Increase storage cost

---

## Indexing vs Processing (Important Distinction)

- Processing → shapes logs
- Indexing → makes logs searchable

Not all logs need indexing.

Best practice:
> Process broadly, index selectively.

---

## Common Pipeline Mistakes

❌ One giant pipeline for everything  
❌ Parsing logs after indexing  
❌ No ownership or documentation  
❌ Ignoring sensitive data masking  

---

## Why This Module Matters

Well-designed pipelines:
- Improve search speed
- Reduce costs
- Enable better alerts

Poor pipelines:
- Waste money
- Hide important signals
- Create security risks

---

## Key Takeaways

- Pipelines transform raw logs into insight
- Processors must be ordered carefully
- Structured logs are essential
- Cost control starts in pipelines

---

➡️ **Next Module:** Log Indexes & Retention
