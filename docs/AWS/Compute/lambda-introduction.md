---
sidebar_position: 9
title: AWS Lambda Introduction
---

# AWS Lambda – Introduction

AWS Lambda represents a **shift in how applications are built and run**.

With Lambda:
- You don’t manage servers
- You don’t worry about scaling
- You pay only when code runs

This is called **serverless computing** — not because servers don’t exist, but because **you don’t manage them**.

---

## What Is AWS Lambda? (Simple Explanation)

AWS Lambda lets you:
- Run code in response to events
- Without provisioning or managing servers
- With automatic scaling

In simple terms:
> **Lambda = run code on demand without managing EC2**

---

## Why Lambda Exists

Traditional compute problems:
- Servers must always be running
- You pay even when idle
- Scaling logic is complex

Lambda solves this by:
- Running code only when needed
- Scaling automatically
- Eliminating idle costs

👉 Lambda is **event-driven compute**.

---

## How Lambda Works (High-Level Flow)

1. An event occurs  
2. Lambda function is triggered  
3. Code executes  
4. Lambda shuts down  

Examples of events:
- HTTP request via API Gateway
- S3 file upload
- Scheduled cron job
- DynamoDB update

---

## Key Characteristics of Lambda

### 1. Fully Managed
AWS manages:
- Servers
- OS
- Scaling
- Patching

You manage:
- Code
- Logic
- Permissions

---

### 2. Automatic Scaling
- Scales from 0 to thousands instantly
- No capacity planning required

---

### 3. Pay Per Execution
You pay for:
- Number of executions
- Execution duration (milliseconds)

No execution = **no cost**.

---

## Common Lambda Use Cases

- REST APIs (with API Gateway)
- Event processing
- File processing (S3 triggers)
- Automation scripts
- Background jobs

Lambda is **ideal for short-lived tasks**.

---

## Lambda vs EC2 (Quick Comparison)

| Feature | Lambda | EC2 |
|------|-------|-----|
| Server management | None | Required |
| Scaling | Automatic | Manual/ASG |
| Billing | Per execution | Per hour |
| Execution time | Limited | Unlimited |
| Use case | Event-driven | Long-running apps |

---

## Important Limitations (Be Honest)

Lambda is powerful, but not perfect:

- Execution time limit
- Cold starts (latency on first run)
- Not ideal for long-running processes
- Debugging can be harder

👉 Knowing limits shows **real-world maturity**.

---

## Lambda in Real Architectures

Typical serverless setup:
- API Gateway → Lambda
- Lambda → DynamoDB / S3
- EventBridge for events

This architecture:
- Scales automatically
- Costs very little at low traffic
- Requires minimal operations

---

## Interview Tip

If asked:
> “When would you choose Lambda over EC2?”

Strong answer:
> For event-driven, short-lived workloads where automatic scaling and low operational overhead are important.

This shows **architect-level decision making**.

---

## Key Takeaways

- Lambda is serverless compute
- No server management required
- Scales automatically
- Pay only when code runs
- Best for event-driven workloads

---

📌 **Next:** Containers vs Serverless (ECS, EKS, Lambda comparison)
