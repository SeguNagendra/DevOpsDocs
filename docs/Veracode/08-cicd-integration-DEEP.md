---
sidebar_position: 8
title: CI/CD Integration with Veracode
---

# CI/CD Integration with Veracode
**Jenkins • GitHub Actions • GitLab CI**

This module is the **hands-on core** of Veracode for DevOps engineers.

Up to now, you learned:
- What Veracode is
- How scans work
- How policies decide pass/fail

Now we answer the most important question:
> **How do I integrate Veracode into real CI/CD pipelines without breaking delivery?**

---

## 1. Core CI/CD Integration Principles (Read First)

Before touching any tool, understand these rules.

### Rule 1: CI/CD Owns Automation, Not Security Decisions
- CI/CD triggers scans
- CI/CD enforces results
- Security teams define policies

DevOps never manually approves security results.

---

### Rule 2: Not All Scans Belong in CI
- Fast scans → CI
- Slow scans → scheduled or pre-prod
- Runtime scans → staging

Blind integration causes slow, fragile pipelines.

---

### Rule 3: Pipelines Must Be Predictable
- Same behavior every run
- No UI clicks
- No manual overrides
- Same rules across repos

Predictability builds developer trust.

---

## 2. High-Level Veracode CI/CD Flow

Typical pipeline flow:

1. Code pushed
2. CI triggered
3. Build artifact created
4. Veracode scan triggered
5. Scan status checked
6. Policy evaluated
7. Pipeline passes or fails

Everything must be **fully automated**.

---

## 3. Authentication & Secrets Management (Critical)

### How CI Authenticates to Veracode
- API credentials
- Service accounts
- Never personal accounts

### Best Practices
- Store credentials in CI secret stores
- Rotate credentials regularly
- Limit permissions
- Never echo secrets in logs

Security failures often start with leaked CI secrets.

---

## 4. Jenkins + Veracode Integration (Conceptual)

### Typical Jenkins Usage
- Jenkins builds the application
- Veracode scan triggered post-build
- Jenkins polls scan status
- Jenkins enforces policy result

### Best Practices
- Use shared libraries
- Separate build and scan stages
- Avoid long-running synchronous jobs
- Prefer polling over blocking

Jenkins works well for **large enterprises**.

---

## 5. GitHub Actions + Veracode Integration

### Why GitHub Actions Is Popular
- Native to GitHub
- Easy secrets management
- YAML-based pipelines

### Recommended Flow
- Trigger SCA on PRs
- Trigger sandbox SAST on feature branches
- Trigger policy scans on main branch

### Key Advice
- Keep workflows small
- Reuse actions
- Avoid complex logic in YAML

---

## 6. GitLab CI + Veracode Integration

### GitLab CI Strengths
- Strong branch rules
- Built-in security concepts
- Good mono-repo support

### Recommended Flow
- Use stages (build → scan → gate)
- Use rules for branch-based behavior
- Separate sandbox and policy jobs

Consistency across projects is key.

---

## 7. Branching Strategy & Scan Mapping

### Recommended Strategy

| Branch Type | Scan Type | Enforcement |
|-----------|-----------|------------|
| feature/* | SCA + Sandbox SAST | Informational |
| pull request | SCA | Soft gate |
| main | SAST + SCA | Hard gate |
| release | SAST + SCA | Hard gate |
| staging | DAST | Release gate |

This keeps pipelines fast and secure.

---

## 8. Synchronous vs Asynchronous Scans

### Synchronous (Blocking)
- Pipeline waits
- Simple logic
- Risk of long waits

### Asynchronous (Preferred)
- Pipeline triggers scan
- Polls or checks later
- Better pipeline performance

Asynchronous scans scale better.

---

## 9. Handling Scan Failures Gracefully

Failures can happen due to:
- Build issues
- Network problems
- Scan timeouts

### DevOps Best Practices
- Distinguish infra failure vs policy failure
- Retry transient errors
- Fail fast on policy violations
- Log clearly

Never hide failures.

---

## 10. CI/CD Anti-Patterns (Avoid These)

Avoid:
- Running full SAST on every commit
- Blocking feature branches
- Manual approvals
- Hardcoding credentials
- One pipeline for all apps

These destroy DevSecOps adoption.

---

## 11. Example End-to-End CI/CD Flow (Narrative)

1. Developer opens PR
2. SCA runs automatically
3. PR shows dependency risk
4. Developer fixes issue
5. Code merged to main
6. SAST + SCA policy scan runs
7. Policy passes
8. Release promoted
9. DAST validates runtime behavior

No emails. No meetings. No panic.

---

## 12. Key Takeaways

- CI/CD integration is the DevOps core responsibility
- Use fast scans early, deep scans later
- Enforce policies automatically
- Protect developer experience
- Consistency beats complexity

---

## What’s Next?

Next module covers:
- Veracode CLI and APIs
- Automation at scale
- Script-driven workflows
