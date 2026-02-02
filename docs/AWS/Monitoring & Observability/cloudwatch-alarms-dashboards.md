---
sidebar_position: 5
title: CloudWatch Alarms and Dashboards
---

# CloudWatch Alarms and Dashboards

Metrics and logs are only useful if they **drive action**.
CloudWatch Alarms and Dashboards help you **detect problems early and visualize system health**.

This guide focuses on **designing useful alerts and dashboards**, not noisy ones.

---

## CloudWatch Alarms (Core Concept)

CloudWatch alarms:
- Watch a metric or expression
- Compare against a threshold
- Trigger actions when breached

Actions include:
- SNS notifications
- Auto Scaling
- Lambda invocation

---

## Alarm States Explained

An alarm can be in one of three states:

- **OK** – Metric is within threshold
- **ALARM** – Threshold breached
- **INSUFFICIENT_DATA** – Not enough data

Understanding states prevents:
- False alerts
- Missed incidents

---

## Types of Alarms

### Static Threshold Alarms
- Fixed threshold (CPU > 80%)

Simple but:
- Not adaptive

---

### Anomaly Detection Alarms
- Use machine learning
- Detect abnormal behavior

Best for:
- Unknown traffic patterns
- Seasonal workloads

---

## What to Alert On (Very Important)

Alert on:
- High error rate
- High latency
- Failed requests
- Capacity exhaustion

Avoid alerting on:
- CPU alone
- Non-actionable metrics

Rule:
> **Alert on customer impact, not infrastructure noise**

---

## Alarm Evaluation Periods

Alarm evaluation:
- Period × datapoints

Example:
- CPU > 80% for 3 out of 5 minutes

This helps:
- Reduce false positives

---

## Composite Alarms

Composite alarms:
- Combine multiple alarms
- Reduce alert noise

Example:
- Alert only if CPU high AND error rate high

Used for:
- Complex systems

---

## Notifications with SNS

SNS is commonly used to:
- Send email alerts
- Trigger PagerDuty / Slack

Best practice:
- Separate topics for severity levels

---

## CloudWatch Dashboards

Dashboards:
- Visualize metrics and logs
- Provide real-time visibility

Used for:
- Operations teams
- Management views
- Incident response

---

## Dashboard Best Practices

Good dashboards:
- Show high-level health first
- Use few, meaningful metrics
- Include error and latency metrics

Avoid:
- Overcrowded dashboards
- Too many graphs

---

## Service vs Application Dashboards

### Service Dashboards
- EC2, RDS, ALB metrics

### Application Dashboards
- Business KPIs
- Error rates
- Latency percentiles

Both are needed.

---

## Cost Considerations

Alarms cost:
- Per alarm

Dashboards:
- Limited free widgets
- Paid for custom dashboards

Control cost by:
- Removing unused alarms
- Consolidating dashboards

---

## Common Beginner Mistakes

- Alerting on everything
- No dashboards
- Dashboards with too much data
- Ignoring alarm tuning

These lead to:
- Alert fatigue
- Missed real issues

---

## Interview Tip

If asked:
> “How do you design monitoring alerts?”

Strong answer:
> By alerting on customer-impacting metrics, tuning thresholds, and reducing noise using composite alarms.

---

## Key Takeaways

- Alarms turn metrics into action
- Alert design matters more than quantity
- Dashboards provide situational awareness
- Composite alarms reduce noise
- Good observability reduces MTTR

---

📌 **Next:** AWS X-Ray and Distributed Tracing
