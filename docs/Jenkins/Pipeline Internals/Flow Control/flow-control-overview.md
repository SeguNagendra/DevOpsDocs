---
sidebar_position: 1
---

# Pipeline Flow Control – Overview

This section covers **how Jenkins pipelines make decisions and control execution flow**.
Flow control is essential for **real-world CI/CD pipelines**, not toy examples.

---

## What Is Pipeline Flow Control?

Flow control allows pipelines to:
- Run stages conditionally
- Accept runtime input
- Change behavior based on parameters
- Handle failures gracefully
- Control time, retries, and concurrency

Without flow control, pipelines are:
- Rigid
- Hard to reuse
- Unsafe for production

---

## Why Flow Control Matters in Production

Real pipelines must handle:
- Multiple environments (DEV / QA / PROD)
- Branch-based logic
- Feature toggles
- Manual approvals
- Failures and retries

Flow control makes pipelines **safe and flexible**.

---

## Core Flow Control Features

This section is split into focused documents covering:

- `when` conditions (conditional stages)
- Build parameters
- `input` step (manual approvals)
- `options` directive
- Timeouts and retries

Each concept is documented **independently**.

---

## Typical Real-World Examples

- Deploy only from `main` branch
- Run regression tests only when flag is enabled
- Pause pipeline for production approval
- Automatically retry flaky tests
- Fail fast on long-running stages

---

## Common Beginner Mistakes

- Hardcoding branch logic
- Skipping approvals in PROD
- No timeouts (pipelines hang forever)
- No retries for flaky tests

---

## Interview Perspective

- Flow control questions are very common
- Expect scenarios, not definitions
- Ability to explain `when` vs parameters is key
