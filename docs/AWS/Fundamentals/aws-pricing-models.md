---
sidebar_position: 7
title: AWS Pricing Models
---

# AWS Pricing Models

One of the **biggest fears** people have about AWS is:
> “AWS is expensive.”

In reality, AWS is **flexible**, not automatically expensive.
You pay **based on how you use services**, not a fixed amount.

Understanding AWS pricing models helps you:
- Control costs
- Design efficient architectures
- Answer cost-related interview questions confidently

---

## Core Idea Behind AWS Pricing

AWS follows a simple principle:

> **Pay only for what you use.**

There is:
- No upfront hardware purchase
- No long-term commitment (unless you choose one)
- Ability to scale costs up or down

---

## Main AWS Pricing Models

AWS offers four primary pricing options:

1. On-Demand  
2. Reserved Instances  
3. Spot Instances  
4. Savings Plans  

Each serves a **different business need**.

---

## 💳 On-Demand Pricing

### What it is
You pay:
- Per second or per hour
- Only while the resource is running

No commitment, no contracts.

### When to use
- Development & testing
- Short-term workloads
- Unpredictable traffic

### Example
You launch an EC2 instance for 5 hours:
- You pay only for those 5 hours
- Stop the instance → billing stops

👉 Most people **start with On-Demand**.

### Downsides
- Most expensive option long-term

---

## 🏷️ Reserved Instances (RI)

### What it is
You commit to using a service for:
- 1 year or 3 years

In return, AWS gives **significant discounts**.

### Types of Reserved Instances
- Standard RI (highest discount)
- Convertible RI (more flexibility)

### When to use
- Steady, predictable workloads
- Production servers running 24/7

### Example
Your production EC2 runs all year:
- Use Reserved Instance
- Save up to 70%

👉 Best for **stable workloads**.

---

## ⚡ Spot Instances

### What it is
You use **unused AWS capacity** at very low prices.

AWS can reclaim Spot instances:
- With short notice
- When capacity is needed

### When to use
- Batch jobs
- CI/CD runners
- Big data processing
- Fault-tolerant workloads

### Example
Video rendering or log processing:
- Job restarts if interrupted
- Massive cost savings

👉 Spot can save **up to 90%**.

### Risk
- Instances can be terminated anytime

---

## 📉 Savings Plans

### What it is
You commit to:
- A consistent amount of usage (per hour)
- Over 1 or 3 years

Applies automatically across services.

### Types
- Compute Savings Plans
- EC2 Instance Savings Plans

### When to use
- Flexible workloads
- Modern architectures
- Mixed instance types

👉 Preferred replacement for many RI use cases.

---

## Quick Comparison

| Pricing Model | Commitment | Flexibility | Cost |
|-------------|------------|------------|------|
| On-Demand | None | High | High |
| Reserved | 1–3 years | Low–Medium | Low |
| Spot | None | Low | Very Low |
| Savings Plans | 1–3 years | High | Low |

---

## Common Cost Mistakes (Real-World)

- Leaving EC2 running 24/7 unnecessarily
- Forgetting unused EBS volumes
- No cost alerts or budgets
- No tagging strategy

👉 Cost problems are usually **operational**, not AWS issues.

---

## Interview Tip (Important)

If asked:
> “How do you reduce AWS cost?”

Mention:
- Right pricing model
- Auto scaling
- Spot usage
- Savings Plans
- Monitoring & alerts

This shows **practical AWS experience**.

---

## Key Takeaways

- AWS pricing is usage-based
- Different models for different workloads
- On-Demand for flexibility
- Reserved/Savings Plans for steady usage
- Spot for massive savings

---

📌 **Next:** AWS Free Tier
