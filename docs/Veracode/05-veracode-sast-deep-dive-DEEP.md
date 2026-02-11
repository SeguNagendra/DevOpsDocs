---
sidebar_position: 5
title: Veracode SAST Deep Dive
---

# Veracode SAST Deep Dive  
**Static Application Security Testing for DevOps Engineers**

This module goes deep into **SAST**, the scan type most commonly integrated into CI/CD.
You will learn **how SAST works**, **what DevOps must configure**, **how to avoid pipeline pain**, and **how to use SAST effectively at scale**.

---

## 1. What SAST Really Is (Plain English)

**Static Application Security Testing (SAST)** analyzes application code **without running the application**.

It answers a simple question:
> “Does the code contain insecure patterns that could be exploited?”

Unlike runtime scans, SAST:
- Looks at code paths
- Understands data flow
- Flags risky coding patterns early

---

## 2. What Veracode SAST Scans (Important Clarity)

Veracode SAST scans **compiled artifacts**, not raw source code.

### Common Artifacts
- Java: `.jar`, `.war`, `.ear`
- .NET: `.dll`, `.exe`
- C/C++: compiled binaries
- Python/Node: packaged files (ZIP, TAR)

👉 **DevOps takeaway:**  
If the build doesn’t succeed, **SAST cannot run**.

---

## 3. How Veracode SAST Works (Step-by-Step)

1. Developer commits code
2. CI pipeline builds the application
3. Build artifact is created
4. Artifact is uploaded to Veracode
5. Veracode analyzes code paths
6. Findings are generated
7. Policy is evaluated
8. CI pipeline receives pass/fail

There should be **no manual steps** after this.

---

## 4. Why SAST Can Be Slow (And That’s Normal)

SAST is slower because:
- It analyzes **entire codebases**
- It traces **data flows**
- It evaluates **multiple execution paths**

### Typical Scan Times
- Small apps: minutes
- Large monoliths: tens of minutes
- Huge legacy apps: longer

👉 This is why **placement in CI/CD matters**.

---

## 5. Where SAST Belongs in CI/CD (DevOps Rule)

### ❌ Bad Placement
- Every commit
- Every pull request
- Feature branches with policy enforcement

### ✅ Good Placement
- Main branch
- Nightly builds
- Release pipelines
- Sandbox scans for feature branches

**Golden rule:**  
> SAST should protect releases, not slow developers.

---

## 6. Sandbox vs Policy Scans (Revisited)

### Sandbox SAST
- Fast feedback
- No pipeline blocking
- Ideal for feature branches

### Policy SAST
- Enforces security rules
- Can block releases
- Used for compliance

DevOps engineers must **design pipelines using both**.

---

## 7. Understanding SAST Findings

SAST findings include:
- Severity (Very High → Low)
- Category (Injection, Auth, Crypto, etc.)
- CWE reference
- Code location
- Remediation guidance

### Important DevOps Insight
Not all findings are equal:
- Some are theoretical
- Some are exploitable
- Some are noise

This is why **policies and triage matter**.

---

## 8. False Positives (Why They Happen)

False positives occur due to:
- Framework abstractions
- Defensive coding patterns
- Incomplete context
- Legacy code structures

### DevOps Best Practice
- Don’t disable SAST
- Use **sandboxes**
- Tune policies
- Let security teams handle mitigation

---

## 9. Artifact Packaging Best Practices

### General Rules
- Include only required binaries
- Exclude test artifacts
- Keep packages small
- Be consistent

### Why This Matters
- Faster uploads
- Faster scans
- Fewer errors
- Better results

---

## 10. Scaling SAST in Large Organizations

Challenges:
- Many apps
- Long scan times
- Pipeline contention

Solutions:
- Nightly SAST
- Parallel pipelines
- Standardized build templates
- API-driven automation

SAST must scale **without blocking delivery**.

---

## 11. Common DevOps Mistakes with SAST

Avoid these:
- Running SAST on every commit
- Blocking feature branches
- Uploading wrong artifacts
- Treating all findings equally
- Using UI instead of CI automation

---

## 12. Key Takeaways

- SAST finds code-level vulnerabilities
- It scans compiled artifacts
- It is slower by design
- Placement matters more than frequency
- Sandboxes protect developer velocity
- DevOps enables SAST, security governs risk

---

## What’s Next?

Next module covers:
- Veracode SCA deep dive
- Open-source risk
- CVEs and license compliance
