---
sidebar_position: 1
---

# Jenkins Jobs – Overview

This section explains **how work is defined and executed in Jenkins** using different job types.
Choosing the right job type is critical for **maintainability, scalability, and CI/CD maturity**.

---

## What Is a Jenkins Job?

A Jenkins job defines:
- What code to run
- When to run it
- Where to run it
- How to report results

Jobs are created and managed by the **Jenkins Controller** and executed on **Agents**.

---

## Why Job Type Selection Matters

Wrong job type leads to:
- Hard-to-maintain configurations
- Duplicate logic
- Poor scalability
- Fragile CI/CD pipelines

Correct job type ensures:
- Pipeline as Code
- Version control
- Reusability
- Team collaboration

---

## Jenkins Job Types (High Level)

Jenkins supports multiple job types, but **only three matter in real projects**:

1. Freestyle Job  
2. Pipeline Job  
3. Multibranch Pipeline  

Each job type has a **dedicated document** in this section.

---

## Recommended Usage (Industry Standard)

| Job Type | Recommendation |
|--------|----------------|
| Freestyle | ❌ Avoid for new projects |
| Pipeline | ✅ Default choice |
| Multibranch Pipeline | ✅ Mandatory for teams |

> Modern Jenkins = Pipeline + Multibranch + SCM

---

## Pipeline as Code (Key Concept)

Pipeline jobs use a `Jenkinsfile` stored in source control.
This provides:
- Versioning
- Code review
- History tracking
- Easy rollback

---

## Configuration Scope

Jobs can be configured at:
- Global level
- Folder level
- Job level

Understanding configuration scope prevents **unexpected overrides**.

---

## Common Beginner Mistakes

- Using freestyle jobs for complex workflows
- Hardcoding logic in UI
- Not using source control for pipelines

