---
sidebar_position: 9
title: AWS WAF and Shield
---

# AWS WAF and Shield

Applications exposed to the internet are constantly under attack.
AWS WAF and AWS Shield protect applications from **common web attacks and DDoS threats**.

These services form the **front-line defense** of AWS security.

---

## What Is AWS WAF? (Simple Explanation)

AWS WAF (Web Application Firewall):
- Protects web applications
- Filters HTTP/HTTPS requests
- Blocks malicious traffic

In simple terms:
> **WAF = rules that decide which web requests are allowed or blocked**

---

## Why AWS WAF Exists

Without WAF:
- Applications are vulnerable to attacks
- Bots and scanners overload systems
- Security teams react too late

AWS WAF helps:
- Block common exploits
- Reduce attack surface
- Protect applications proactively

---

## Common Attacks Blocked by WAF

AWS WAF protects against:
- SQL injection
- Cross-site scripting (XSS)
- Bad bots
- Malicious IP addresses

These are **OWASP Top 10** threats.

---

## How AWS WAF Works

High-level flow:
1. Request reaches ALB / CloudFront / API Gateway
2. WAF evaluates request against rules
3. Request is allowed, blocked, or counted

👉 Decisions happen **before** reaching application.

---

## Web ACLs and Rules

### Web ACL
- A collection of rules
- Applied to a resource

### Rules
- Define match conditions
- Take actions (allow, block, count)

Rules are evaluated **in order**.

---

## Managed Rules vs Custom Rules

### Managed Rules
- Provided by AWS or vendors
- Cover common attack patterns
- Easy to enable

### Custom Rules
- Written by you
- Specific to application logic

Best practice:
- Start with managed rules
- Add custom rules gradually

---

## Rate-Based Rules

Rate-based rules:
- Limit requests from an IP
- Protect against brute force attacks

Example:
- Block IPs sending > 1000 requests in 5 minutes

---

## Where AWS WAF Can Be Used

AWS WAF integrates with:
- Application Load Balancer (ALB)
- CloudFront
- API Gateway

👉 Not used directly with EC2 instances.

---

## AWS Shield (DDoS Protection)

AWS Shield protects against:
- Distributed Denial of Service (DDoS) attacks

It is always:
- On
- Inline
- Transparent

---

## Shield Standard vs Shield Advanced

### Shield Standard
- Enabled by default
- Protects against common network attacks
- No additional cost

### Shield Advanced
- Enhanced DDoS protection
- 24/7 DDoS response team
- Cost protection

Used by:
- High-traffic
- Mission-critical applications

---

## When to Use WAF vs Shield

| Scenario | Service |
|-------|---------|
| Web exploits | WAF |
| Application-layer attacks | WAF |
| Network-layer DDoS | Shield |
| Large-scale DDoS | Shield Advanced |

👉 They work **together**, not separately.

---

## Monitoring and Logging

AWS WAF provides:
- Request logs
- Metrics in CloudWatch

Use logs to:
- Tune rules
- Investigate attacks

---

## Common Beginner Mistakes

- No WAF on public apps
- Overblocking legitimate traffic
- Ignoring logs
- Assuming Shield replaces WAF

These mistakes cause:
- Downtime
- False positives

---

## Interview Tip

If asked:
> “How do you protect web applications in AWS?”

Strong answer:
> By using AWS WAF to block malicious requests and AWS Shield to protect against DDoS attacks.

---

## Key Takeaways

- WAF protects against web attacks
- Shield protects against DDoS
- Managed rules simplify protection
- Logging is essential
- Both are critical for internet-facing apps

---

📌 **Next:** Security Summary
