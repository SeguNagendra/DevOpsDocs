---
sidebar_position: 2
---

# Freestyle Job

Freestyle jobs are the **oldest job type in Jenkins**.
They are still seen in legacy systems but are **not recommended for modern CI/CD**.

---

## What Is a Freestyle Job?

A Freestyle job is a UI-configured Jenkins job where:
- Build steps are configured via the Jenkins UI
- Logic is not stored as code
- Changes are hard to track and review

---

## How Freestyle Jobs Work

- Configuration is stored as XML on the controller
- Build steps are executed sequentially
- SCM, triggers, and steps are configured manually

---

## Typical Use Cases (Today)

Freestyle jobs are still used for:
- Very simple scripts
- Legacy Jenkins setups
- One-off administrative tasks

> They are **not suitable** for complex pipelines.

---

## Limitations of Freestyle Jobs

- No Pipeline-as-Code
- Poor version control
- Hard to review changes
- Difficult to scale
- Weak support for complex logic

---

## Freestyle vs Pipeline

| Feature | Freestyle | Pipeline |
|------|-----------|----------|
| Stored as code | ❌ | ✅ |
| Version control | ❌ | ✅ |
| Reusability | ❌ | ✅ |
| Scalability | ❌ | ✅ |
| Modern CI/CD | ❌ | ✅ |

---

## Why Freestyle Jobs Are Discouraged

Reasons:
- Configuration drift
- Manual errors
- UI-based logic
- Not team-friendly

Most organizations **migrate away from freestyle jobs**.

---

## Interview Perspective

- Know what freestyle jobs are
- Explain **why you avoid them**
- Mention migration to pipeline jobs

---

## When Can You Use Freestyle?

Acceptable scenarios:
- Learning Jenkins basics
- Simple cron-based scripts
- Legacy maintenance
