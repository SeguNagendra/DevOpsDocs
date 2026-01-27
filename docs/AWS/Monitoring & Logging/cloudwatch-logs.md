---
sidebar_position: 3
title: CloudWatch Logs
---

# CloudWatch Logs

If metrics tell you **something is wrong**,
👉 **logs tell you why it is wrong**.

CloudWatch Logs is used for **troubleshooting, debugging, and audits**.
In real production incidents, engineers spend more time in logs than anywhere else.

---

## What Are CloudWatch Logs?

CloudWatch Logs allows you to:
- Collect logs from AWS services and applications
- Store logs centrally
- Search and analyze logs
- Retain logs for auditing and troubleshooting

In simple terms:
> **CloudWatch Logs = centralized logging service in AWS**

---

## Why Logs Matter

Without logs:
- Root cause analysis is impossible
- Debugging becomes guesswork
- Audits fail

Logs help answer:
> “What exactly happened, and when?”

---

## Core CloudWatch Logs Concepts (Must Know)

### Log Group
- A logical container for logs
- Usually represents an application or service

Examples:
- `/aws/lambda/my-function`
- `/aws/ec2/web-server`

---

### Log Stream
- A sequence of log events
- Represents a single source

Examples:
- One EC2 instance
- One Lambda execution environment

---

## How Logs Get Into CloudWatch

Logs can be sent using:
- AWS services (Lambda, API Gateway, ECS)
- CloudWatch Agent
- Application SDKs

👉 Logs are **not automatic** for EC2 — you must configure them.

---

## CloudWatch Log Retention

By default:
- Logs are kept forever

Best practice:
- Set retention policies
- Delete old logs automatically

Common retention:
- 7 days (dev)
- 30–90 days (prod)
- Longer for compliance

---

## Searching Logs

CloudWatch Logs supports:
- Filter patterns
- Keyword search
- Structured JSON logs

Example:
- Search for ERROR messages
- Filter by request ID

This is critical during incidents.

---

## Log Insights (Very Important)

CloudWatch Logs Insights allows you to:
- Query logs using SQL-like syntax
- Analyze large volumes quickly

Use cases:
- Find error spikes
- Trace slow requests
- Analyze traffic patterns

👉 This is a **powerful troubleshooting tool**.

---

## Real-World Troubleshooting Flow

Typical incident flow:
1. Alarm triggers (metrics)
2. Check CloudWatch Logs
3. Use Logs Insights
4. Identify root cause
5. Fix and monitor

Logs complete the monitoring loop.

---

## Security and Auditing

Logs are used for:
- Security audits
- Compliance
- Incident investigation

Best practices:
- Restrict log access via IAM
- Encrypt logs
- Retain logs as required

---

## Common Beginner Mistakes

- Not enabling log collection
- Infinite log retention (high cost)
- Poor log structure
- Logging too much or too little

These mistakes cause:
- Blind incidents
- High bills

---

## Interview Tip

If asked:
> “How do you debug issues in AWS?”

Strong answer:
> By using CloudWatch metrics to detect issues and CloudWatch Logs to analyze and identify root causes.

That shows **real production experience**.

---

## Key Takeaways

- Logs explain failures
- Log groups and streams are core concepts
- Retention policies control cost
- Logs Insights enables fast analysis
- Essential for debugging and audits

---

📌 **Next:** CloudWatch Alarms
