---
sidebar_position: 1
title: VPC Basics
---

# Amazon VPC – Basics

Amazon VPC (Virtual Private Cloud) is **the networking foundation of AWS**.

If:
- EC2 is where applications run
- S3 is where data lives

👉 **VPC is where everything connects securely**.

Almost every AWS service runs **inside or connected to a VPC**.

---

## What Is a VPC? (Simple Explanation)

A VPC is a **logically isolated virtual network** inside AWS where you can:
- Launch resources
- Control IP addressing
- Control network traffic
- Apply security rules

In simple terms:
> **VPC = your private network in AWS**

---

## Why VPC Exists

Without VPC:
- All AWS resources would live in a shared network
- No isolation between customers
- No control over traffic flow

VPC exists to provide:
- Network isolation
- Security boundaries
- Custom network design

👉 VPC gives you **full control over networking**.

---

## Default VPC vs Custom VPC

### Default VPC
- Automatically created by AWS
- Has public subnets
- Easy for beginners

### Custom VPC
- Manually created
- Full control over IP ranges
- Required for production

👉 **Real-world workloads always use custom VPCs**.

---

## Core VPC Components (High Level)

You must understand these building blocks:

- CIDR block
- Subnets
- Route tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs

We will cover each **in detail** next.

---

## CIDR Block (Very Important)

CIDR defines:
- IP address range of your VPC

Example:
```
10.0.0.0/16
```

This provides:
- 65,536 private IP addresses

👉 CIDR planning is **critical and hard to change later**.

---

## Subnets (Preview)

A subnet is:
- A smaller IP range inside a VPC
- Always created inside **one Availability Zone**

Common pattern:
- Public subnets (internet-facing)
- Private subnets (internal services)

---

## How Traffic Flows in a VPC (High Level)

Traffic flow depends on:
- Route tables
- Gateways
- Security rules

Nothing is reachable:
- Unless explicitly allowed

👉 AWS networking is **deny by default**.

---

## VPC and High Availability

VPC itself is:
- Region-scoped

High availability is achieved by:
- Creating subnets in multiple AZs
- Deploying resources across AZs

👉 VPC enables **multi-AZ architectures**.

---

## Common Beginner Mistakes

- Using default VPC in production
- Poor CIDR planning
- Putting everything in public subnets
- Ignoring route tables

These mistakes cause:
- Security risks
- Scaling problems
- Re-architecture later

---

## Interview Tip

If asked:
> “What is a VPC?”

Strong answer:
> A VPC is a logically isolated virtual network in AWS that allows customers to control IP addressing, routing, and security.

Simple, correct, professional.

---

## Key Takeaways

- VPC is the networking backbone of AWS
- Provides isolation and control
- Custom VPCs are standard for production
- CIDR planning is critical
- Foundation for all AWS architectures

---

📌 **Next:** CIDR and Subnetting
