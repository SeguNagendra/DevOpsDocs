---
sidebar_position: 1
title: EC2 Introduction
---

# Amazon EC2 – Introduction

Amazon EC2 (Elastic Compute Cloud) is the **most fundamental compute service in AWS**.

If AWS were a city:
- **EC2 is the land and buildings**
- Everything else is built on top of it

Almost every AWS engineer, DevOps engineer, or architect **starts with EC2**.

---

## What Is EC2? (Simple Explanation)

EC2 allows you to:
- Create virtual servers in the cloud
- Choose CPU, memory, storage, and OS
- Start, stop, resize, or delete servers anytime

In short:
> **EC2 = virtual machine in AWS**

But unlike traditional servers, EC2 is:
- On-demand
- Scalable
- Pay-as-you-go

---

## Why EC2 Exists

Before EC2:
- Companies bought physical servers
- Scaling took weeks or months
- Hardware was often underutilized

With EC2:
- Servers launch in minutes
- Scale up or down anytime
- No upfront hardware cost

👉 EC2 removed the biggest barrier to running applications.

---

## Core Concepts You Must Understand

Before using EC2 effectively, you must understand these terms:

- **Instance** – A running virtual server  
- **AMI** – Template used to launch an instance  
- **Instance Type** – CPU, memory, and network capacity  
- **Region & AZ** – Where the instance runs  
- **Key Pair** – Used for secure login  
- **Security Group** – Firewall for the instance  

We will cover each **in detail** in upcoming files.

---

## How EC2 Fits into Real Architectures

EC2 is rarely used alone.

Typical usage:
- EC2 behind a Load Balancer
- EC2 in Auto Scaling Groups
- EC2 inside private subnets
- EC2 accessing RDS, S3, and other services

👉 EC2 is a **building block**, not the full solution.

---

## Common EC2 Use Cases

- Hosting web applications
- Running backend APIs
- CI/CD build agents
- Batch processing
- Legacy application hosting

Despite newer services, **EC2 is still everywhere**.

---

## EC2 vs Traditional Servers

| Traditional Server | EC2 |
|-------------------|-----|
| Fixed capacity | Flexible capacity |
| Long procurement | Launch in minutes |
| High upfront cost | Pay-as-you-go |
| Manual scaling | Auto scaling |
| Physical maintenance | Fully managed hardware |

---

## Shared Responsibility Reminder

With EC2:
- AWS manages the **hardware**
- You manage the **OS, applications, and security configuration**

This is pure **IaaS responsibility**.

---

## Interview Tip

If asked:
> “What is EC2?”

A strong answer:
> EC2 is an AWS compute service that provides resizable virtual servers where customers control the operating system and applications.

That shows **clarity, not memorization**.

---

## Key Takeaways

- EC2 is the foundation of AWS compute
- Think of EC2 as a virtual server
- Highly flexible and scalable
- Requires proper security and management
- Used in almost every AWS architecture

---

📌 **Next:** EC2 Instance Types
