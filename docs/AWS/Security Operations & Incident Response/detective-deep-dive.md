---
sidebar_position: 6
title: Amazon Detective Deep Dive
---

# Amazon Detective – Deep Dive

Detection tells you **something is wrong**.
Investigation tells you **what actually happened**.

Amazon Detective helps security teams **analyze, investigate, and understand security incidents** using timelines and relationship graphs.

---

## What Is Amazon Detective? (Clear Explanation)

Amazon Detective:
- Helps investigate security findings
- Automatically builds security data graphs
- Provides visual timelines and context

In simple terms:
> **Detective = investigation and root-cause analysis for AWS security incidents**

---

## When Do You Use Detective?

Detective is used **after detection**, not before.

Typical triggers:
- GuardDuty high-severity finding
- Security Hub alert
- Suspicious IAM activity

Detective answers:
> **How did this incident happen?**

---

## Data Sources Used by Detective

Detective automatically ingests:
- CloudTrail logs
- VPC Flow Logs
- GuardDuty findings

No manual log correlation required.

---

## Detective Investigation Graphs

Detective builds:
- Relationship graphs between resources
- Historical timelines of activity

You can visualize:
- IAM user behavior
- EC2 network activity
- API call sequences

---

## Investigation Workflow (Real-World)

Typical workflow:
1. Alert received from GuardDuty/Security Hub
2. Open finding in Detective
3. Review timeline and related entities
4. Identify root cause
5. Take remediation action

This reduces investigation time significantly.

---

## Detective vs CloudWatch Logs

| Aspect | Detective | CloudWatch Logs |
|----|-----------|-----------------|
| Purpose | Investigation | Raw logging |
| Visualization | Yes | No |
| Correlation | Automatic | Manual |
| Use case | Security incidents | Debugging |

Detective complements logs — it doesn’t replace them.

---

## Use Cases

Common Detective use cases:
- Investigating compromised credentials
- Analyzing lateral movement
- Understanding data exfiltration paths

---

## Integration with Other Services

Detective integrates with:
- GuardDuty
- Security Hub

This creates:
- Detection → Investigation → Response pipeline

---

## Cost Considerations

Detective pricing is based on:
- Data volume analyzed

Best practice:
- Enable for production accounts
- Limit scope if necessary

---

## Common Beginner Mistakes

- Expecting Detective to prevent attacks
- Not using it during incidents
- Ignoring historical timelines
- No defined investigation process

These reduce its effectiveness.

---

## Interview Tip

If asked:
> “How do you investigate security incidents in AWS?”

Strong answer:
> By using Amazon Detective to analyze timelines and relationships after GuardDuty or Security Hub findings.

---

## Key Takeaways

- Detective is for investigation, not detection
- Uses timelines and graphs
- Reduces MTTR
- Complements GuardDuty and Security Hub
- Essential for SOC teams

---

📌 **Next:** Incident Response Workflow in AWS
