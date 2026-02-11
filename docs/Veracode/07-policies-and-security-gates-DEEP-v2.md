---
sidebar_position: 7
title: Policies and Security Gates
---

# Policies and Security Gates
**SAST • SCA • DAST • IAST**

This is the **correct and complete version** of the Policies module.  
It explains **how Veracode policies behave across ALL scan types** and how a **DevOps engineer should enforce them without breaking delivery**.

This module is one of the **most interview‑critical** and **real‑world‑critical** chapters.

---

## 1. What a Security Policy Really Is (Revisited)

A **Veracode security policy** is a **decision engine**.

It answers one question:
> “Based on scan results, is this application allowed to move forward?”

Important clarifications:
- A policy is **not a scan**
- A policy is evaluated **after** a scan finishes
- A policy can **block or allow** progress automatically

Policies convert **technical findings → delivery decisions**.

---

## 2. Why Policies Exist in DevOps Pipelines

Without policies:
- Every vulnerability becomes a debate
- DevOps makes subjective decisions
- Pipelines behave inconsistently
- Security becomes manual

With policies:
- Decisions are predictable
- Risk tolerance is codified
- CI/CD becomes self‑governing
- DevOps enforces, not argues

---

## 3. Policy Enforcement by Scan Type (Core Section)

### High‑Level View

| Scan Type | Policy Evaluated | Can Block Pipeline | DevOps Ownership |
|---------|----------------|-------------------|-----------------|
| SAST | ✅ Yes | ✅ Yes | Primary |
| SCA | ✅ Yes | ✅ Yes | Primary |
| DAST | ✅ Yes | ⚠️ Rare | Secondary |
| IAST | ⚠️ Limited | ❌ No | Minimal |

Each scan type interacts with policies **differently**.

---

## 4. SAST Policies (Build‑Time Enforcement)

### How SAST Policies Work
- SAST runs on compiled code
- Policy evaluates severity, CWE, exploitability
- Result is **Pass / Fail**

### Typical SAST Policy Rules
- No Very High or High issues
- No exploitable injection flaws
- Aging limits on vulnerabilities

### DevOps Usage
- Enforce on **main / release branches**
- Fail builds automatically
- Never run strict policies on feature branches

👉 **SAST is the strongest policy gate in CI/CD**.

---

## 5. SCA Policies (Dependency Risk Enforcement)

### How SCA Policies Work
- Evaluated against dependency vulnerabilities
- Includes CVSS, CVE age, exploit maturity
- Includes **license risk**

### Typical SCA Policy Rules
- Block Critical / High CVEs
- Block known exploited vulnerabilities
- Block restricted licenses (GPL, AGPL)

### DevOps Usage
- Enforce on PRs and builds
- Prefer fast feedback
- Allow time‑bound exceptions

👉 **SCA policies should run most frequently**.

---

## 6. DAST Policies (Pre‑Release Enforcement)

### How DAST Policies Work
- Evaluated after runtime scans
- Applied to deployed environments
- Focused on exploitable runtime flaws

### Important Reality
DAST policies **rarely block CI pipelines directly** because:
- DAST runs late
- Environments are shared
- Results are slower

### Correct Usage
- Gate **release approvals**
- Block production promotion
- Trigger remediation workflows

👉 DAST policies protect **runtime behavior**, not developer velocity.

---

## 7. IAST Policies (Advisory, Not Blocking)

### How IAST Policies Work
- IAST findings supplement other scans
- Often treated as **informational**
- Rarely used for hard enforcement

### DevOps Reality
- IAST requires instrumentation
- Mostly driven by security teams
- DevOps rarely wires IAST into CI gates

👉 **IAST informs risk, it does not control pipelines**.

---

## 8. Progressive Enforcement Strategy (Best Practice)

### Bad Strategy
- One strict policy
- Applied everywhere
- Blocks developers constantly

### Good Strategy (Recommended)

| Stage | Enforcement |
|----|----|
| Feature Branch | Sandbox (No policy) |
| PR / Early CI | Soft SCA policies |
| Main Branch | SAST + SCA policies |
| Pre‑Prod | DAST policies |
| Production | Governance & reporting |

This balances **speed, security, and trust**.

---

## 9. Exceptions and Waivers (All Scan Types)

Valid reasons for exceptions:
- False positives
- Legacy constraints
- Accepted business risk

### Rules for Exceptions
- Must be time‑bound
- Must be documented
- Must be approved by security
- Must be enforced automatically

❌ Manual pipeline overrides are forbidden.

---

## 10. DevOps Responsibilities (Clear Boundary)

DevOps engineers:
- Integrate policy checks
- Ensure correct scan → policy mapping
- Automate enforcement
- Maintain pipeline reliability

DevOps engineers do **NOT**:
- Decide business risk alone
- Suppress findings arbitrarily
- Manually approve releases

---

## 11. Common DevOps Policy Mistakes

Avoid these:
- Blocking feature branches
- Treating all scans equally
- Using DAST to block CI
- Ignoring license policies
- No exception workflow

These mistakes destroy DevSecOps adoption.

---

## 12. Key Takeaways (Zero → Hero)

- Policies are decision engines
- SAST & SCA drive CI gates
- DAST protects releases, not builds
- IAST is advisory
- Progressive enforcement works best
- DevOps enforces objectively

---

## What’s Next?

Next module covers:
- CI/CD integration patterns
- Jenkins, GitHub Actions, GitLab
- Real pipeline designs
