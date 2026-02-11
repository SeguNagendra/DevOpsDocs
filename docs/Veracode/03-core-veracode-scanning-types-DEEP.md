---
sidebar_position: 3
title: Core Veracode Scanning Types
---

# Core Veracode Scanning Types
(SAST • SCA • DAST • IAST)

This module explains **what each Veracode scan type really does**, **why it exists**, and **how a DevOps engineer should use it in CI/CD**.

If you ever wondered:
- “Why so many scan types?”
- “Why not run everything in CI?”
- “Which scan should fail my build?”

This chapter answers those questions from **zero → hero**.

---

## 1. Why Multiple Scan Types Exist

No single security scan can detect all vulnerabilities.

Applications have:
- Custom code written by developers
- Open-source libraries
- Runtime behavior
- Configuration issues

Each scan type focuses on a **different risk area**.  
DevOps engineers must **combine them intelligently**, not blindly.

---

## 2. Static Application Security Testing (SAST)

### What SAST Really Does
SAST analyzes **compiled application code** without running the application.

It looks for insecure patterns such as:
- SQL Injection
- Cross-Site Scripting (XSS)
- Insecure cryptography
- Authentication and authorization flaws
- Unsafe deserialization

SAST answers the question:
> “Is the code itself written securely?”

---

### How Veracode SAST Works (Simplified)
1. Developers write code
2. CI builds the application (JAR, WAR, DLL, EXE, etc.)
3. Compiled artifact is uploaded to Veracode
4. Veracode analyzes code paths
5. Vulnerabilities are reported

No source code is required — only compiled artifacts.

---

### DevOps Perspective on SAST
- High coverage
- Slower than other scans
- Can produce false positives
- Best suited for controlled pipeline stages

### Where SAST Belongs
- Main branch builds
- Nightly pipelines
- Pre-release validation

❌ Avoid running full SAST on every commit.

---

## 3. Software Composition Analysis (SCA)

### What SCA Really Does
SCA scans **third-party and open-source dependencies** used by the application.

It detects:
- Known vulnerabilities (CVEs)
- Vulnerable transitive dependencies
- License compliance issues
- End-of-life components

SCA answers:
> “Are we using any known vulnerable libraries?”

---

### Why SCA Is Critical in Modern DevOps
Most applications today are:
- 70–90% open-source
- Built using package managers (Maven, npm, pip, etc.)

Many high-profile breaches occurred due to **known vulnerable libraries**, not custom code.

---

### DevOps Perspective on SCA
- Extremely fast
- Very low noise
- Ideal for every build
- Easy to gate pipelines

### Where SCA Belongs
- Pull requests
- Feature branches
- Main branch builds

SCA is the **most DevOps-friendly security scan**.

---

## 4. Dynamic Application Security Testing (DAST)

### What DAST Really Does
DAST tests a **running application** by simulating attacker behavior.

It:
- Sends malicious inputs
- Observes responses
- Identifies runtime vulnerabilities

DAST answers:
> “How does the application behave when attacked?”

---

### DAST Requirements
- Deployed application
- Stable environment
- Network access
- Often authentication setup

### DevOps Reality
- Slower
- Environment-dependent
- Can be flaky if misconfigured

---

### Where DAST Belongs
- Staging environments
- Pre-production
- Scheduled scans

❌ DAST does **not** belong in fast CI builds.

---

## 5. Interactive Application Security Testing (IAST)

### What IAST Does
IAST runs inside the application runtime using agents.

It combines:
- Code visibility (like SAST)
- Runtime execution (like DAST)

### DevOps Reality Check
- Requires application instrumentation
- Adds runtime overhead
- Usually driven by security teams

### Recommendation
DevOps engineers should **understand IAST conceptually**, but rarely implement it themselves.

---

## 6. Comparing Scan Types (DevOps View)

| Scan | Speed | Coverage | CI Friendly | Typical Owner |
|---|---|---|---|---|
| SAST | Slow | High | Medium | DevOps |
| SCA | Fast | Medium | High | DevOps |
| DAST | Slow | Runtime | Low | Security |
| IAST | Medium | Runtime | Low | Security |

---

## 7. CI/CD Scan Placement Strategy

### Recommended Pipeline Flow

| Pipeline Stage | Scan Type |
|---|---|
| Pull Request | SCA |
| Feature Branch | SCA + Sandbox SAST |
| Main Branch | SAST + SCA |
| Pre-Production | DAST |
| Production | Monitoring & reporting |

This strategy balances **speed, coverage, and risk**.

---

## 8. Common DevOps Mistakes with Scans

Avoid these:
- Running all scans in CI
- Blocking feature branches
- Ignoring SCA results
- Treating all findings equally
- Using scans without policies

---

## 9. Key Takeaways

- Each scan serves a unique purpose
- SCA should run most frequently
- SAST must be placed carefully
- DAST requires stable environments
- IAST is optional for DevOps
- Smart placement = fast pipelines

---

## What’s Next?

Next module covers:
- Veracode SAST deep dive
- Packaging artifacts
- Scan tuning and noise reduction
