---
sidebar_position: 8
title: Launch Templates and Launch Configurations
---

# Launch Templates and Launch Configurations

When Auto Scaling Groups need to launch EC2 instances, AWS needs a **definition** of:
- Which AMI to use
- Which instance type to launch
- What security settings apply
- What startup actions to run

This definition is provided by **Launch Templates** (and earlier, Launch Configurations).

---

## Why Launch Templates Exist

Without a standard launch definition:
- Auto Scaling cannot work reliably
- Instance configurations become inconsistent
- Updates become risky

Launch Templates solve this by acting as a **single source of truth** for EC2 launches.

---

## What Is a Launch Template?

A Launch Template is a **reusable configuration** that defines how EC2 instances are launched.

It can include:
- AMI ID
- Instance type
- Key pair
- Security groups
- User Data scripts
- IAM role
- Storage configuration

Think of it as:
> A **blueprint** used by Auto Scaling Groups to create instances.

---

## Launch Template vs Launch Configuration

AWS originally introduced **Launch Configurations**, but they are now **legacy**.

### Key Differences

| Feature | Launch Template | Launch Configuration |
|------|----------------|---------------------|
| Versioning | Supported | Not supported |
| Flexibility | High | Limited |
| New features | Yes | No |
| AWS recommendation | ✅ Use | ❌ Avoid |

👉 **Always use Launch Templates for new workloads.**

---

## Why Versioning Matters (Very Important)

Launch Templates support **versions**.

This means you can:
- Create version 1 (baseline)
- Create version 2 (new AMI)
- Roll back safely if something breaks

This is **critical for safe deployments**.

---

## Launch Templates in Real Architectures

Typical production flow:
1. Create Launch Template
2. Attach it to Auto Scaling Group
3. Update template version for new releases
4. ASG launches new instances automatically

This enables:
- Blue/Green deployments
- Rolling updates
- Zero-downtime changes

---

## What Should Go Into a Launch Template?

Best practices:
- Use a **custom AMI**
- Keep User Data minimal
- Use IAM roles, not credentials
- Avoid hardcoding values

The goal is **consistency and repeatability**.

---

## Common Mistakes

- Using Launch Configurations for new systems
- Hardcoding secrets in User Data
- Editing templates without version control
- Not testing new template versions

These mistakes cause **failed launches and downtime**.

---

## Interview Tip

If asked:
> “How do Auto Scaling Groups know how to launch instances?”

Strong answer:
> By using Launch Templates, which define the AMI, instance type, security settings, and startup configuration.

That answer signals **production-level AWS knowledge**.

---

## Key Takeaways

- Launch Templates define EC2 launch behavior
- Required for Auto Scaling Groups
- Support versioning and safe updates
- Replace Launch Configurations
- Core building block for scalable systems

---

📌 **Next:** AWS Lambda Introduction
