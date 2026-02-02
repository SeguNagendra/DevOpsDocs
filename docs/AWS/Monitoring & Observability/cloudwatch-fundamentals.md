---
sidebar_position: 2
title: Amazon CloudWatch Fundamentals
---

# Amazon CloudWatch – Fundamentals

Amazon CloudWatch is the **core monitoring service** in AWS.
It collects metrics, logs, and events to help you **observe, alert, and act** on what’s happening in your environment.

If you operate AWS workloads,
👉 you **must** understand CloudWatch properly.

---

## What Is Amazon CloudWatch? (Simple Explanation)

Amazon CloudWatch:
- Collects metrics from AWS services
- Stores and queries logs
- Triggers alarms and automated actions

In simple terms:
> **CloudWatch = visibility and alerting for AWS resources**

---

## Why CloudWatch Is Critical

Without CloudWatch:
- You don’t know when systems fail
- Issues are detected too late
- Debugging is guesswork

CloudWatch enables:
- Proactive monitoring
- Faster incident response
- Operational confidence

---

## Core Components of CloudWatch

CloudWatch consists of four main parts:

1. Metrics
2. Alarms
3. Logs
4. Events (EventBridge)

Each solves a **different observability problem**.

---

## CloudWatch Metrics

Metrics are:
- Time-series numerical data
- Collected at regular intervals

Examples:
- CPUUtilization
- NetworkIn / NetworkOut
- RequestCount

Metrics answer:
> **What is happening right now?**

---

## Namespaces

A namespace:
- Groups related metrics
- Prevents metric name conflicts

Examples:
- AWS/EC2
- AWS/RDS
- AWS/Lambda

Custom metrics:
- Use custom namespaces

---

## Dimensions

Dimensions:
- Are key-value pairs
- Add context to metrics

Example:
- InstanceId=i-123456

Dimensions allow:
- Filtering
- Aggregation
- Granular monitoring

---

## Metric Resolution

CloudWatch supports:
- Standard resolution (1 minute)
- High resolution (1 second)

Use high resolution:
- For latency-sensitive workloads
- When fast alerting is required

---

## CloudWatch Alarms

Alarms:
- Watch metrics
- Trigger actions when thresholds are crossed

Actions:
- Send SNS notification
- Trigger Auto Scaling
- Invoke Lambda

---

## Alarm States

Alarm states:
- OK
- ALARM
- INSUFFICIENT_DATA

Understanding states helps:
- Avoid false alerts
- Debug issues

---

## CloudWatch Logs

Logs:
- Store application and system logs
- Are searchable and filterable

Sources:
- EC2
- Lambda
- ECS
- Custom applications

Logs answer:
> **Why did something happen?**

---

## Log Groups and Log Streams

- Log Group → Collection of logs
- Log Stream → Single source of logs

Example:
- One log group per application
- One log stream per instance

---

## Retention Policies

Logs retention:
- Configurable per log group
- Default is “never expire”

Best practice:
- Set retention to control costs

---

## CloudWatch Events (EventBridge)

Events:
- Respond to state changes
- Trigger automation

Examples:
- EC2 instance stopped
- CodePipeline state change

---

## Security in CloudWatch

Security features:
- IAM-based access control
- Encryption at rest
- Audit logs via CloudTrail

Best practice:
- Least privilege for monitoring roles

---

## Common Beginner Mistakes

- No alarms configured
- Alerting on wrong metrics
- No log retention policy
- Ignoring dimensions

These mistakes lead to:
- Missed incidents
- High costs

---

## Interview Tip

If asked:
> “What does CloudWatch do?”

Strong answer:
> CloudWatch collects metrics and logs, triggers alarms, and provides visibility into AWS resources.

---

## Key Takeaways

- CloudWatch is AWS’s core monitoring service
- Metrics, logs, alarms, and events work together
- Namespaces and dimensions add structure
- Alerts enable proactive operations
- Essential for reliable cloud systems

---

📌 **Next:** CloudWatch Metrics Deep Dive
