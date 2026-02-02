---
sidebar_position: 8
title: AWS Certificate Manager (ACM)
---

# AWS Certificate Manager (ACM)

Encryption in transit is **mandatory** for modern applications.
AWS Certificate Manager (ACM) makes it easy to **provision, manage, and renew SSL/TLS certificates**.

If your application uses HTTPS,
👉 ACM should be your default choice.

---

## What Is AWS Certificate Manager? (Simple Explanation)

AWS Certificate Manager:
- Provisions SSL/TLS certificates
- Manages renewal automatically
- Integrates with AWS services

In simple terms:
> **ACM = managed SSL/TLS certificates for AWS**

---

## Why ACM Exists

Without ACM:
- Certificates must be purchased manually
- Renewals are error-prone
- Expired certs cause outages

ACM provides:
- Free public certificates
- Automatic renewal
- Deep AWS integration

---

## Public vs Private Certificates

### Public Certificates
- Trusted by browsers
- Used for internet-facing apps
- Free when used with AWS services

### Private Certificates
- Used for internal apps
- Require ACM Private CA
- Used inside organizations

---

## Supported AWS Integrations

ACM integrates with:
- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- CloudFront
- API Gateway

👉 Certificates cannot be exported for external use.

---

## Certificate Validation Methods

ACM supports:
- DNS validation (recommended)
- Email validation

DNS validation:
- Automatic
- No renewal issues

👉 Always prefer DNS validation.

---

## TLS Termination

ACM is commonly used for:
- TLS termination at load balancer
- Offloading encryption from instances

Benefits:
- Simplified application code
- Centralized certificate management

---

## Regional vs Global Certificates

- ACM certificates are **regional**
- CloudFront requires certificates in **us-east-1**

This is a common interview and real-world gotcha.

---

## Certificate Lifecycle

ACM handles:
- Issuance
- Validation
- Renewal
- Replacement

You don’t:
- Track expiry dates
- Manually rotate certificates

---

## Security Best Practices

- Use HTTPS everywhere
- Redirect HTTP to HTTPS
- Use modern TLS versions
- Monitor certificate usage

---

## Common Beginner Mistakes

- Using email validation
- Forgetting us-east-1 for CloudFront
- Trying to export ACM certificates
- Using self-signed certs publicly

These mistakes cause:
- Downtime
- Browser warnings

---

## Interview Tip

If asked:
> “How do you manage SSL certificates in AWS?”

Strong answer:
> By using AWS Certificate Manager to provision and automatically renew SSL/TLS certificates for AWS services.

---

## Key Takeaways

- ACM manages SSL/TLS certificates
- Free public certs for AWS services
- Automatic renewal
- Deep AWS integration
- Essential for HTTPS

---

📌 **Next:** AWS WAF (Web Application Firewall)
