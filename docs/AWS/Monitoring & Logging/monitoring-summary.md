---
sidebar_position: 9
title: Monitoring and Logging Summary
---

# Monitoring and Logging – Summary

This page is a **mental-model recap** of AWS Monitoring and Logging.
It connects **CloudWatch, EventBridge, CloudTrail, and AWS Config** into a single, clear picture.

If you understand this page, you understand **how AWS observability really works**.

---

## Monitoring vs Logging vs Auditing vs Compliance

First, clear the confusion:

- **Monitoring** → How is the system behaving?
- **Logging** → Why did something happen?
- **Auditing** → Who did what?
- **Compliance** → Is the system following rules?

AWS provides **different services** for each concern.

---

## CloudWatch (Monitoring Core)

CloudWatch is used for:
- Metrics (health & performance)
- Logs (application & system logs)
- Alarms (notifications & automation)
- Dashboards (visualization)

Key idea:
> **CloudWatch answers: Is the system healthy right now?**

---

## CloudWatch Metrics (Quick Recall)

- Time-series numerical data
- Namespaces organize metrics
- Dimensions identify resources
- Used by alarms and dashboards

Examples:
- EC2 CPUUtilization
- ALB RequestCount
- Lambda Duration

---

## CloudWatch Logs (Quick Recall)

- Centralized log storage
- Log groups and log streams
- Retention policies control cost
- Logs Insights enables fast queries

Key use:
> Debugging and root cause analysis

---

## CloudWatch Alarms (Quick Recall)

- Watch metrics
- Trigger notifications or actions
- Drive Auto Scaling
- Use composite alarms to reduce noise

Key idea:
> **Alarms convert metrics into action**

---

## CloudWatch Dashboards (Quick Recall)

- Single-pane-of-glass monitoring
- Combine metrics across services
- Used during incidents and operations

Dashboards answer:
> “What is the current system state?”

---

## Amazon EventBridge (Automation Layer)

EventBridge is used for:
- Reacting to AWS events
- Event-driven automation
- Scheduled jobs (cron replacement)

Examples:
- EC2 state change → trigger Lambda
- Scheduled cleanup job

Key idea:
> **EventBridge connects events to actions**

---

## AWS CloudTrail (Audit Layer)

CloudTrail records:
- AWS API calls
- Console logins
- Service-to-service actions

Used for:
- Security investigations
- Compliance audits
- Accountability

Key question answered:
> **Who did what, when, and from where?**

---

## AWS Config (Compliance Layer)

AWS Config tracks:
- Resource configuration changes
- Historical configuration states
- Compliance against rules

Used for:
- Drift detection
- Governance
- Regulatory compliance

Key question answered:
> **Is the resource configured correctly?**

---

## CloudTrail vs AWS Config (Must Remember)

| Aspect | CloudTrail | AWS Config |
|-----|-----------|-----------|
| Focus | API activity | Resource configuration |
| Answers | Who did what | What changed |
| Time | Event-based | State-based |
| Use | Auditing | Compliance & drift |

👉 They complement each other.

---

## Real-World Monitoring Flow

Typical production flow:
1. CloudWatch metric detects issue
2. Alarm triggers notification
3. Logs used for root cause analysis
4. EventBridge automates remediation
5. CloudTrail audits the action
6. AWS Config verifies compliance

This is **full observability**.

---

## Common Anti-Patterns (Avoid)

- No alarms on critical metrics
- Logs without retention policies
- CloudTrail not enabled in all regions
- AWS Config enabled but ignored
- Manual remediation instead of automation

---

## Interview Rapid-Fire Answers

**Q: How do you monitor AWS resources?**  
A: Using CloudWatch metrics, logs, alarms, and dashboards.

**Q: How do you audit AWS API activity?**  
A: Using AWS CloudTrail.

**Q: How do you track configuration drift?**  
A: Using AWS Config rules.

**Q: How do you automate reactions to events?**  
A: Using Amazon EventBridge.

---

## Final Takeaway

Monitoring and logging are not tools — they are **operational discipline**.

When done right:
- Failures are detected early
- Root causes are clear
- Automation reduces downtime
- Compliance becomes manageable

---

📌 **Next:** Phase 06 – Databases
