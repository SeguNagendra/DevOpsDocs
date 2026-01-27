---
sidebar_position: 4
title: CloudWatch Alarms
---

# CloudWatch Alarms

Metrics and logs tell you **what is happening**.
👉 **Alarms tell you when to act.**

CloudWatch Alarms convert monitoring data into **notifications and automated actions**.
They are critical for **availability, reliability, and auto-healing systems**.

---

## What Is a CloudWatch Alarm? (Simple Explanation)

A CloudWatch Alarm:
- Watches a metric
- Evaluates it against a threshold
- Changes state when conditions are met
- Triggers an action

In simple terms:
> **Alarm = rule that reacts to metric behavior**

---

## Why Alarms Matter

Without alarms:
- Issues are discovered manually
- Downtime lasts longer
- Scaling decisions are delayed

Alarms exist to:
- Detect problems early
- Notify teams
- Trigger automation

👉 Monitoring without alarms is **incomplete**.

---

## Alarm States (Must Know)

Every alarm has three states:

- **OK** → Metric is within threshold  
- **ALARM** → Threshold breached  
- **INSUFFICIENT_DATA** → Not enough data  

Understanding states helps debugging alarm behavior.

---

## Alarm Components

An alarm is defined by:

- Metric
- Statistic (Average, Sum, Max, etc.)
- Threshold
- Evaluation period
- Comparison operator

Example:
- CPUUtilization > 80% for 5 minutes

---

## Types of CloudWatch Alarms

### 1. Metric Alarms
- Most common
- Based on single or multiple metrics

### 2. Composite Alarms
- Combine multiple alarms
- Reduce alert noise

👉 Composite alarms are used in **large systems**.

---

## Alarm Actions

Alarms can trigger:

- SNS notifications (email, Slack, PagerDuty)
- Auto Scaling actions
- EC2 stop/start/recover
- Systems Manager actions

👉 Alarms turn monitoring into **automation**.

---

## Alarms and Auto Scaling

Common use case:
- Scale out when CPU > 70%
- Scale in when CPU < 30%

Alarms drive:
- Elastic scaling
- Cost optimization

---

## Treat Missing Data (Important)

Alarms can:
- Ignore missing data
- Treat missing as breaching
- Treat missing as not breaching

Choosing correctly prevents:
- False alarms
- Missed incidents

---

## Alarm Best Practices

- Alert on symptoms, not causes
- Avoid too many alarms
- Use composite alarms
- Test alarms regularly

👉 Good alarms are **actionable**.

---

## Common Beginner Mistakes

- Too many noisy alarms
- No alarms on critical metrics
- Wrong thresholds
- Ignoring INSUFFICIENT_DATA

These mistakes cause:
- Alert fatigue
- Missed outages

---

## Interview Tip

If asked:
> “How do you get notified when something goes wrong in AWS?”

Strong answer:
> By creating CloudWatch alarms on critical metrics and sending notifications using SNS or triggering automated actions.

---

## Key Takeaways

- Alarms react to metrics
- States indicate system health
- Trigger notifications and automation
- Essential for scaling and reliability
- Core part of monitoring strategy

---

📌 **Next:** CloudWatch Dashboards
