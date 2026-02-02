---
sidebar_position: 2
title: AWS Security Monitoring Services Overview
---

# AWS Security Monitoring Services – Overview

AWS provides multiple **managed security services** to help you detect threats,
identify vulnerabilities, and maintain a strong security posture.

Understanding **what each service does and when to use it** is critical for effective security operations.

---

## Why AWS Security Monitoring Services Matter

Modern cloud environments:
- Change frequently
- Are highly distributed
- Generate massive security signals

Manual monitoring is not scalable.
AWS security services provide:
- Continuous threat detection
- Centralized visibility
- Automated findings

---

## Core AWS Security Monitoring Services

The main AWS security monitoring services are:

1. Amazon GuardDuty
2. AWS Security Hub
3. Amazon Inspector
4. Amazon Detective

Each service has a **specific role**.

---

## Amazon GuardDuty (Threat Detection)

GuardDuty:
- Continuously monitors AWS accounts
- Uses machine learning and threat intelligence
- Detects suspicious activity

Monitors:
- CloudTrail events
- VPC Flow Logs
- DNS logs

Examples of findings:
- Compromised IAM credentials
- Crypto-mining activity
- Port scanning

---

## AWS Security Hub (Central Visibility)

Security Hub:
- Aggregates security findings
- From AWS and third-party tools
- Provides a single security dashboard

Key features:
- Security standards (CIS, AWS Foundational)
- Compliance scores
- Centralized reporting

---

## Amazon Inspector (Vulnerability Management)

Inspector:
- Scans workloads for vulnerabilities
- Identifies missing patches and CVEs

Supports:
- EC2 instances
- ECR container images
- Lambda functions

Used for:
- Proactive vulnerability detection

---

## Amazon Detective (Investigation)

Detective:
- Helps investigate security incidents
- Visualizes relationships and timelines

Used after:
- GuardDuty or Security Hub findings

Detective answers:
> **How did this incident happen?**

---

## How These Services Work Together

Typical flow:
1. GuardDuty detects threat
2. Security Hub aggregates finding
3. Inspector identifies vulnerabilities
4. Detective helps investigate

This creates a **complete SecOps workflow**.

---

## Security Service Comparison

| Service | Purpose | When Used |
|------|--------|----------|
| GuardDuty | Threat detection | Continuous |
| Security Hub | Central view | Always |
| Inspector | Vulnerability scan | Pre/Post deploy |
| Detective | Investigation | During incident |

---

## Enable by Default?

Recommended:
- Enable GuardDuty and Security Hub organization-wide
- Enable Inspector for production workloads
- Use Detective for investigation teams

---

## Common Beginner Mistakes

- Enabling services but ignoring findings
- No alert routing
- Treating findings as noise
- No ownership defined

These reduce security effectiveness.

---

## Interview Tip

If asked:
> “How do you monitor security in AWS?”

Strong answer:
> By using GuardDuty for threat detection, Security Hub for centralized visibility, Inspector for vulnerability scanning, and Detective for investigations.

---

## Key Takeaways

- AWS provides specialized security monitoring tools
- Each service has a distinct role
- Services work best together
- Central visibility is critical
- Monitoring enables fast response

---

📌 **Next:** Amazon GuardDuty Deep Dive
