---
sidebar_position: 5
title: Amazon Inspector Deep Dive
---

# Amazon Inspector – Deep Dive

Amazon Inspector is AWS’s **vulnerability management service**.
It helps you identify **security weaknesses before attackers exploit them**.

Inspector focuses on **what could be exploited**, not active attacks.

---

## What Is Amazon Inspector? (Clear Explanation)

Amazon Inspector:
- Continuously scans workloads
- Identifies vulnerabilities and exposures (CVEs)
- Provides remediation guidance

In simple terms:
> **Inspector = automated vulnerability scanning for AWS workloads**

---

## What Inspector Scans

Inspector supports scanning for:

- **EC2 instances** (OS & package vulnerabilities)
- **ECR container images** (image vulnerabilities)
- **Lambda functions** (package vulnerabilities)

This covers most modern AWS workloads.

---

## Types of Vulnerabilities Detected

Inspector detects:
- Missing security patches
- Known CVEs
- Software vulnerabilities
- Configuration weaknesses (limited)

Findings are mapped to:
- CVE IDs
- Severity levels

---

## Continuous vs On-Demand Scanning

Inspector works in:
- **Continuous mode** (recommended)
- On-demand scans (legacy approach)

Continuous scanning ensures:
- New vulnerabilities are detected automatically

---

## Inspector Findings

Each finding includes:
- Acknowledged CVE
- Affected resource
- Severity (Low → Critical)
- Remediation steps

This helps teams:
- Prioritize patching

---

## Severity Levels

Inspector uses:
- Low
- Medium
- High
- Critical

Best practice:
> **Patch Critical and High vulnerabilities first**

---

## Inspector and DevSecOps

Inspector integrates with:
- CI/CD pipelines
- ECR image scanning
- Security Hub

Use cases:
- Block vulnerable images from deployment
- Shift security left

---

## Inspector vs GuardDuty

| Aspect | Inspector | GuardDuty |
|----|-----------|-----------|
| Purpose | Vulnerability scanning | Threat detection |
| Timing | Pre-exploitation | Active threats |
| Data source | Packages & images | Logs & behavior |
| Response | Patch/fix | Investigate/respond |

They serve **different security layers**.

---

## Inspector and Security Hub

Inspector findings:
- Are sent to Security Hub
- Contribute to security posture

This enables:
- Centralized remediation tracking

---

## Cost Considerations

Inspector pricing is based on:
- Number of resources scanned
- Frequency of scanning

Best practice:
- Enable for production workloads
- Monitor scan scope

---

## Common Beginner Mistakes

- Ignoring vulnerability findings
- No patching process
- Treating Inspector as attack detection
- Not integrating with Security Hub

These lead to:
- Exploitable systems

---

## Interview Tip

If asked:
> “How do you identify vulnerabilities in AWS?”

Strong answer:
> By using Amazon Inspector to continuously scan EC2, container images, and Lambda functions for known vulnerabilities.

---

## Key Takeaways

- Inspector detects vulnerabilities, not attacks
- Supports EC2, ECR, and Lambda
- Continuous scanning is recommended
- Integrates with Security Hub
- Critical for DevSecOps

---

📌 **Next:** Amazon Detective Deep Dive
