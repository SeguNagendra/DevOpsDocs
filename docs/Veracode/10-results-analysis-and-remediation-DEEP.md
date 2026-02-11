---
sidebar_position: 10
title: Results Analysis and Remediation
---

# Results Analysis & Remediation
**How DevOps Enables Developers to Fix Security Issues**

This module explains **what happens after a scan finishes**.
Finding vulnerabilities is useless unless teams can **understand, prioritize, and fix them efficiently**.

As a DevOps engineer, your role is **not to fix code**, but to **enable fast, low-noise remediation workflows**.

---

## 1. Why Results Analysis Matters

Security tools often fail because:
- Results are noisy
- Reports are overwhelming
- Developers don’t know where to start
- Everything looks critical

Good DevSecOps turns:
> “Huge vulnerability reports”  
into  
> “Clear, prioritized action items”

---

## 2. Understanding Veracode Findings (Core Concepts)

### What a Finding Typically Includes
- Severity (Very High, High, Medium, Low)
- Vulnerability category (Injection, Auth, Crypto, etc.)
- CWE reference
- Code or dependency location
- Remediation guidance

### DevOps Insight
Not every finding requires:
- Immediate fixing
- Build failure
- Release blocking

Context matters.

---

## 3. Severity vs Exploitability (Critical Distinction)

### Severity
- Potential impact if exploited

### Exploitability
- Likelihood of being exploited in your context

Examples:
- High severity in unreachable code → lower priority
- Medium severity in auth flow → higher priority

Policies and triage help teams **focus on what matters most**.

---

## 4. SAST Results – How to Interpret Them

### Common SAST Finding Types
- Injection flaws
- Authentication issues
- Cryptographic weaknesses
- Input validation problems

### Why SAST Feels Noisy
- Static analysis is conservative
- Framework abstractions confuse scanners
- Legacy code increases false positives

### DevOps Best Practice
- Use sandboxes for early feedback
- Let security teams mitigate false positives
- Avoid disabling rules globally

---

## 5. SCA Results – How to Interpret Them

### Typical SCA Findings
- Vulnerable direct dependencies
- Vulnerable transitive dependencies
- License violations

### Prioritization Strategy
1. Known exploited vulnerabilities
2. High CVSS + reachable code
3. Direct dependencies before transitive
4. Libraries with available patches

SCA results are usually **high confidence**.

---

## 6. DAST Results – How to Interpret Them

### What DAST Finds Well
- Runtime injection issues
- Authentication weaknesses
- Misconfigurations

### DAST Reality
- Results depend on environment stability
- Some findings are environment-specific

### DevOps Role
- Ensure scans target correct URLs
- Validate authentication setup
- Route findings to the right teams

---

## 7. IAST Results – How to Use Them

IAST findings:
- Provide runtime confirmation
- Reduce false positives
- Supplement SAST and DAST

### DevOps Perspective
- Treat IAST as **additional signal**
- Rarely gate pipelines on IAST alone

---

## 8. Prioritization Framework (Practical)

A simple prioritization model:
1. Exploitable?
2. Internet-facing?
3. Affects auth or data?
4. Patch available?
5. Compliance impact?

DevOps enables prioritization by:
- Enforcing policies
- Highlighting critical paths
- Avoiding alert fatigue

---

## 9. Developer Remediation Workflow

### Ideal Flow
1. Scan runs automatically
2. Results visible to developers
3. Clear fix guidance provided
4. Developer fixes issue
5. Pipeline re-runs
6. Policy passes

No emails. No meetings. No tickets unless needed.

---

## 10. Reducing Noise & Security Debt

### Noise Reduction Techniques
- Sandbox scans early
- Policy tuning
- Exception workflows
- Focused notifications

### Security Debt
- Accumulated unfixed vulnerabilities
- Often caused by rushed releases

DevOps helps manage debt by:
- Tracking trends
- Enforcing aging rules
- Encouraging regular cleanup

---

## 11. Metrics That Matter (DevOps View)

Useful metrics:
- Time to remediate (MTTR)
- Reopened vulnerabilities
- Policy pass rate
- Recurring dependency issues

Avoid vanity metrics like:
- Total vulnerability count

---

## 12. Common DevOps Mistakes

Avoid these:
- Treating all findings equally
- Failing builds without guidance
- Dumping reports on developers
- Ignoring remediation trends
- Manual tracking in spreadsheets

---

## 13. Key Takeaways

- Scans don’t fix problems — people do
- Prioritization beats volume
- DevOps enables fast feedback
- Policies reduce subjectivity
- Noise reduction is critical
- Remediation must fit developer workflows

---

## What’s Next?

Next module covers:
- Enterprise scale & governance
- Multi-application strategy
- Compliance and reporting
