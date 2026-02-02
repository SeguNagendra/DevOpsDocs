---
sidebar_position: 3
title: Amazon GuardDuty Deep Dive
---

# Amazon GuardDuty – Deep Dive

Amazon GuardDuty is AWS’s **primary threat detection service**.
It continuously analyzes activity across your AWS accounts to detect **malicious behavior and compromised resources**.

GuardDuty is a **must-have** for real-world AWS security operations.

---

## What Is Amazon GuardDuty? (Clear Definition)

Amazon GuardDuty:
- Continuously monitors AWS environments
- Uses machine learning, anomaly detection, and threat intelligence
- Generates actionable security findings

In simple terms:
> **GuardDuty = continuous threat detection for AWS accounts**

---

## Data Sources Used by GuardDuty

GuardDuty analyzes signals from:

- **CloudTrail** – API activity and IAM behavior
- **VPC Flow Logs** – Network traffic patterns
- **DNS Logs** – Domain name queries

You do **not** need to enable or manage these logs manually for GuardDuty.

---

## Types of Threats Detected

GuardDuty detects:

- Compromised IAM credentials
- Unusual API calls
- Crypto-mining activity
- Port scanning and brute force attacks
- Data exfiltration attempts
- Communication with known malicious IPs/domains

Findings are based on **behavior**, not signatures alone.

---

## GuardDuty Findings

A finding includes:
- Severity (Low, Medium, High)
- Affected resource
- Description of suspicious activity
- Recommended remediation

Severity helps prioritize response.

---

## Common GuardDuty Finding Categories

Examples:
- **UnauthorizedAccess:IAMUser**
- **CryptoCurrency:EC2/BitcoinTool.B**
- **Recon:EC2/Portscan**
- **Trojan:EC2/BlackholeTraffic**

Understanding categories helps faster triage.

---

## GuardDuty Severity Levels

- **Low** – Unusual but low risk
- **Medium** – Suspicious activity
- **High** – Confirmed or very likely threat

Best practice:
> **Treat High severity findings as incidents**

---

## Enabling GuardDuty (Best Practice)

Recommended setup:
- Enable GuardDuty in all regions
- Enable organization-wide via AWS Organizations
- Designate a delegated admin account

This provides:
- Centralized visibility
- Consistent detection

---

## GuardDuty and Automation

GuardDuty findings can trigger:
- EventBridge rules
- Lambda functions
- Automated remediation

Examples:
- Disable compromised IAM credentials
- Isolate EC2 instances
- Notify SOC team

Automation reduces MTTR.

---

## GuardDuty vs CloudTrail

| Aspect | GuardDuty | CloudTrail |
|----|----------|-----------|
| Purpose | Threat detection | Audit logging |
| Analysis | ML-based | Raw logs |
| Alerts | Yes | No |
| Automation | Yes | Manual |

They **complement**, not replace, each other.

---

## Cost Considerations

GuardDuty pricing is based on:
- Log volume analyzed

Best practices:
- Enable organization-wide
- Review findings regularly
- Cost is usually low compared to risk reduction

---

## Common Beginner Mistakes

- Enabling GuardDuty but ignoring findings
- No alert routing
- No automation for high severity alerts
- Not enabling in all regions

These reduce GuardDuty’s effectiveness.

---

## Interview Tip

If asked:
> “How do you detect compromised credentials in AWS?”

Strong answer:
> By using Amazon GuardDuty to detect anomalous IAM and API activity.

---

## Key Takeaways

- GuardDuty is AWS’s primary threat detection service
- Uses ML and threat intelligence
- Detects IAM, network, and DNS threats
- Works best with automation
- Essential for AWS SecOps

---

📌 **Next:** AWS Security Hub Deep Dive
