---
sidebar_position: 6
title: Veracode SCA Deep Dives
---

# Veracode SCA Deep Dive  
**Software Composition Analysis for DevOps Engineers**

This module focuses on **SCA**, the most DevOps-friendly and high-impact security scan.
You’ll learn **what SCA actually scans**, **why it matters more than ever**, and **how to use it correctly in CI/CD without slowing delivery**.

---

## 1. What SCA Really Is (Plain English)

**Software Composition Analysis (SCA)** identifies **known risks in third‑party and open‑source libraries** used by an application.

It answers a simple question:
> “Are we shipping code that depends on libraries with known vulnerabilities or risky licenses?”

SCA does **not** analyze your custom code logic — it analyzes **what your code depends on**.

---

## 2. Why Open Source Is the Biggest Risk Today

Modern applications are rarely written from scratch.

Typical reality:
- 70–90% of application code comes from open source
- Dependencies are pulled automatically by package managers
- Vulnerabilities are discovered **after** libraries are widely used

Many real-world breaches happened because:
- A known vulnerable library existed
- A patch was available
- Teams didn’t know they were affected

SCA exists to close this visibility gap.

---

## 3. What Veracode SCA Scans

Veracode SCA analyzes:
- Direct dependencies (you explicitly include)
- Transitive dependencies (pulled indirectly)
- Dependency versions
- Associated licenses
- Known vulnerabilities (CVEs)

### Common Ecosystems
- Java (Maven, Gradle)
- JavaScript (npm, yarn)
- Python (pip)
- .NET (NuGet)
- Go modules

👉 **DevOps takeaway:**  
Even if developers didn’t add a library directly, SCA will still find it.

---

## 4. How Veracode SCA Works (Step-by-Step)

1. Code is committed
2. CI pipeline runs
3. Dependency manifest is detected
4. Dependencies are analyzed
5. Vulnerabilities and licenses are identified
6. Results are returned quickly
7. Pipeline can pass or fail automatically

Most SCA scans complete in **seconds to a few minutes**.

---

## 5. Understanding CVEs and CVSS (Simple Explanation)

### CVE (Common Vulnerabilities and Exposures)
- A public identifier for a known vulnerability
- Example: CVE-2021-44228 (Log4Shell)

### CVSS (Common Vulnerability Scoring System)
- A numeric score (0–10)
- Indicates severity and exploitability

### DevOps Reality
- Not all CVEs are equally risky
- Context matters (reachable code, exploit maturity)

This is why **policies** matter more than raw numbers.

---

## 6. License Risk (Often Overlooked)

SCA also checks **open-source licenses**.

Some licenses:
- Are permissive (MIT, Apache)
- Are restrictive (GPL)
- May conflict with company policy

### DevOps Responsibility
- Ensure license checks are automated
- Prevent risky licenses from reaching production
- Avoid legal surprises late in release cycles

---

## 7. Where SCA Belongs in CI/CD (Best Practice)

### Ideal Placement
- Pull requests
- Feature branches
- Main branch builds

### Why SCA Fits Everywhere
- Fast
- Low noise
- Minimal configuration
- High value

SCA should run **more frequently than any other security scan**.

---

## 8. Failing Builds with SCA (Doing It Right)

### Bad Approach
- Fail on every CVE
- Block developers constantly
- Create alert fatigue

### Good Approach
- Fail on high/critical severity
- Consider CVE age
- Allow controlled exceptions
- Review transitive risks

DevOps engineers must design **risk-aware gates**, not blunt blocks.

---

## 9. Managing Transitive Dependency Risk

Transitive dependencies:
- Are often invisible to developers
- Can introduce serious vulnerabilities
- Are common attack paths

### Best Practices
- Keep dependency trees small
- Prefer well-maintained libraries
- Upgrade regularly
- Use SCA results to guide cleanup

---

## 10. Scaling SCA Across Teams

Challenges:
- Many repositories
- Different tech stacks
- Inconsistent rules

Solutions:
- Standardized CI templates
- Centralized policies
- Automated reporting
- Shared best practices

SCA scales easily when automation is consistent.

---

## 11. Common DevOps Mistakes with SCA

Avoid these:
- Ignoring transitive dependencies
- Treating license checks as optional
- Failing builds without context
- Running SCA too late
- Disabling SCA due to “noise”

---

## 12. Key Takeaways

- SCA identifies open-source risk
- Most modern breaches involve dependencies
- SCA is fast and CI-friendly
- Policies matter more than raw CVEs
- License compliance is part of security
- SCA should run everywhere

---

## What’s Next?

Next module covers:
- Veracode policies and security gates
- Risk-based decisions
- Exceptions and waivers
