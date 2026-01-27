---
sidebar_position: 8
title: AWS Free Tier
---

# AWS Free Tier

The AWS Free Tier allows you to **learn, experiment, and build small projects** on AWS **without paying (or paying very little)**.

However, many beginners misunderstand the Free Tier and end up with **unexpected bills**.
This page explains the Free Tier **clearly and honestly**.

---

## What Is AWS Free Tier?

AWS Free Tier is **not one single thing**.
It is a collection of **free usage limits** for different services.

These limits are meant for:
- Learning AWS
- Hands-on practice
- Small proof-of-concept projects

👉 It is **not meant for production workloads**.

---

## Types of AWS Free Tier

AWS Free Tier has **three categories**:

1. Always Free  
2. 12 Months Free  
3. Trials  

Understanding these categories avoids billing surprises.

---

## 🟢 Always Free

### What it means
These services are **free every month**, as long as you stay within limits.

### Common Always Free Services
- AWS Lambda (limited invocations)
- DynamoDB (limited read/write capacity)
- CloudWatch (basic metrics)
- SNS (limited notifications)

### Important
If you **cross the limit**, AWS will charge you.

---

## 🟡 12 Months Free

### What it means
Free usage is available for **12 months from account creation**.

After 12 months:
- Normal pricing applies automatically

### Common Examples
- EC2 (t2.micro / t3.micro – limited hours)
- EBS (limited storage)
- RDS (limited usage)
- S3 (limited storage)

👉 This is where **most beginners make mistakes**.

---

## 🔵 Trials

### What it means
Some services provide **short-term trials**:
- 7 days
- 30 days
- Limited credits

### Examples
- Amazon Redshift trials
- Advanced analytics services

These trials expire quickly and must be monitored.

---

## What AWS Free Tier Is NOT

❌ Unlimited free usage  
❌ Lifetime free EC2  
❌ Safe to ignore billing  

AWS assumes **you are responsible for monitoring usage**.

---

## Real-World Beginner Mistakes

These mistakes cause **unexpected bills**:

- Forgetting to stop EC2 instances
- Leaving EBS volumes after deleting EC2
- NAT Gateway usage (not free)
- Data transfer charges
- Creating resources in multiple regions

👉 AWS Free Tier **does not protect you automatically**.

---

## Best Practices to Stay Free (or Very Cheap)

- Always enable **billing alerts**
- Stop EC2 when not in use
- Delete unused resources
- Use one region consistently
- Monitor usage from Billing Dashboard

These habits make you **cloud-cost conscious early**.

---

## Free Tier for Learning AWS (Recommended Path)

Best use cases:
- Learn EC2 basics
- Practice IAM
- Test S3 and lifecycle rules
- Build small demo projects

Avoid:
- Long-running production systems
- Heavy data processing
- NAT Gateways and advanced networking

---

## Interview Tip

If asked:
> “Is AWS Free Tier really free?”

Best answer:
> AWS Free Tier provides limited free usage, but users must monitor and manage resources carefully to avoid charges.

This shows **real AWS experience**, not theory.

---

## Key Takeaways

- Free Tier has limits
- Always Free ≠ Unlimited
- Billing awareness is critical
- AWS does not auto-stop resources
- Free Tier is for learning, not production

---

📌 **Next:** AWS Service Categories
