---
sidebar_position: 10
title: AWS Security Summary
---

# AWS Security – Summary

This page is a **complete mental-model recap** of AWS Security.
It connects **IAM, KMS, Secrets, ACM, WAF, Shield, CloudTrail, and Config** into one clear picture.

If you understand this page, you understand **how AWS security works in real production environments**.

---

## Security Is a Mindset, Not a Service

AWS security is about:
- Preventing unauthorized access
- Limiting blast radius
- Detecting issues early
- Responding quickly

Security is **designed**, not added later.

---

## Shared Responsibility Model (Recall)

- AWS secures **the cloud**
- You secure **what’s in the cloud**

You are responsible for:
- IAM
- Network rules
- Encryption
- Application security
- Monitoring and audits

---

## Identity and Access Management (IAM)

IAM answers:
> **Who can do what on which resource?**

Key principles:
- Least privilege
- Roles over users
- No long-term credentials
- Strong root account protection

IAM is the **first line of defense**.

---

## Encryption and Secrets

### AWS KMS
- Manages encryption keys
- Uses envelope encryption
- Integrated with AWS services

### Secrets Manager
- Stores sensitive credentials
- Encrypts secrets with KMS
- Supports automatic rotation

Rule:
> **Never hardcode secrets**

---

## Encryption in Transit (ACM)

AWS Certificate Manager:
- Provides SSL/TLS certificates
- Enables HTTPS everywhere
- Auto-renews certificates

Best practice:
- TLS termination at load balancers
- Enforce HTTPS only

---

## Network and Application Protection

### AWS WAF
- Protects against web attacks
- Blocks OWASP Top 10 threats
- Filters requests before reaching apps

### AWS Shield
- Protects against DDoS attacks
- Always on by default
- Advanced for mission-critical apps

They work **together**, not separately.

---

## Monitoring and Auditing

### CloudTrail
- Records all API calls
- Answers “who did what?”
- Essential for audits and investigations

### AWS Config
- Tracks configuration changes
- Detects drift
- Enforces compliance rules

Visibility is mandatory for security.

---

## Defense-in-Depth (Big Picture)

A secure AWS architecture uses **multiple layers**:

1. IAM (identity)
2. Network isolation
3. Encryption (at rest & transit)
4. Application protection
5. Monitoring and auditing

No single service is enough.

---

## Common Security Anti-Patterns

- Using root account daily
- Wildcard IAM policies
- Hardcoded credentials
- No logging or monitoring
- Public resources without protection

These mistakes cause **real breaches**.

---

## Interview Rapid Answers

**Q: How do you secure AWS accounts?**  
A: Using IAM with least privilege, encryption with KMS, secure secrets management, network protections, and continuous monitoring.

**Q: How do you protect web applications?**  
A: Using ACM for HTTPS, WAF for web attacks, and Shield for DDoS protection.

**Q: How do you audit AWS activity?**  
A: Using CloudTrail and AWS Config.

---

## Final Takeaway

AWS provides **excellent security tools**.
Security failures happen due to **misconfiguration**, not weak technology.

Strong security comes from:
- Correct design
- Least privilege
- Continuous monitoring
- Automation

---

📌 **Next:** Phase 08 – CI/CD and Automation
