---
sidebar_position: 6
title: Amazon EventBridge (CloudWatch Events)
---

# Amazon EventBridge (CloudWatch Events)

Modern systems are **event-driven**.
Instead of polling or manual checks,
👉 systems react automatically when **something happens**.

Amazon EventBridge is AWS’s **central event bus** for building automated, loosely coupled architectures.

---

## What Is Amazon EventBridge? (Simple Explanation)

Amazon EventBridge:
- Receives events from AWS services, SaaS apps, and custom apps
- Routes events to targets based on rules
- Enables event-driven automation

In simple terms:
> **EventBridge = if this happens, do that**

---

## Why EventBridge Exists

Before EventBridge:
- Custom scripts polled for changes
- Cron jobs handled schedules
- Systems were tightly coupled

EventBridge exists to:
- React in real time
- Decouple services
- Automate workflows

👉 Event-driven design scales better.

---

## Event Sources

EventBridge supports events from:

- AWS services (EC2, S3, RDS, IAM, etc.)
- Custom applications
- SaaS partners (GitHub, PagerDuty, etc.)

Examples:
- EC2 instance state change
- S3 object uploaded
- IAM API call

---

## Event Buses

An event bus is:
- A channel where events flow

Types of event buses:
- Default event bus (AWS services)
- Custom event buses
- Partner event buses

👉 Most use cases start with the **default bus**.

---

## Rules

Rules define:
- Which events to match
- Where to send them

Rule components:
- Event pattern
- Target

Example:
- When EC2 stops → send notification

---

## Targets

EventBridge can trigger:
- Lambda functions
- SNS topics
- SQS queues
- Step Functions
- ECS tasks

This enables:
- Automation
- Remediation
- Integration

---

## Scheduled Rules (Cron)

EventBridge supports:
- Cron-based schedules
- Rate-based schedules

Examples:
- Run Lambda every 5 minutes
- Daily cleanup job at midnight

👉 EventBridge replaces traditional cron servers.

---

## Common EventBridge Use Cases

- Automated remediation
- Infrastructure changes reaction
- Scheduled jobs
- Audit and compliance automation

EventBridge is heavily used in **DevOps automation**.

---

## EventBridge vs CloudWatch Events

CloudWatch Events:
- Older name

EventBridge:
- Newer, extended service
- Same core functionality + more

👉 Think **EventBridge = CloudWatch Events (modern)**.

---

## Security and Permissions

EventBridge uses:
- IAM permissions
- Resource-based policies (targets)

Always:
- Restrict who can put events
- Restrict what targets can do

---

## Common Beginner Mistakes

- Overcomplicating event patterns
- Not handling failures
- Ignoring dead-letter queues
- Using polling instead of events

These mistakes reduce reliability.

---

## Interview Tip

If asked:
> “How do you automate actions based on AWS events?”

Strong answer:
> By using Amazon EventBridge to react to AWS service events and trigger automated workflows.

---

## Key Takeaways

- EventBridge enables event-driven automation
- Uses events, rules, and targets
- Supports schedules and real-time reactions
- Replaces cron and polling systems
- Core AWS automation service

---

📌 **Next:** AWS CloudTrail
