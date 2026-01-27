---
sidebar_position: 5
title: AWS Global Infrastructure
---

# AWS Global Infrastructure

AWS Global Infrastructure explains **where AWS runs its services** and **how AWS designs for high availability, low latency, and fault tolerance**.

This is one of the **most important fundamentals** because:
- It affects **availability**
- It affects **latency**
- It affects **cost**
- It affects **architecture decisions**

---

## Why Global Infrastructure Matters

Imagine running an application for users across the world.

If everything runs from **one data center**:
- Users far away experience high latency
- A single failure can take everything down

AWS solves this using a **global, distributed infrastructure**.

---

## Core Building Blocks of AWS Infrastructure

AWS global infrastructure is built using **three main components**:

1. Regions  
2. Availability Zones (AZs)  
3. Edge Locations  

Let’s understand each clearly.

---

## 🌍 AWS Regions

### What is a Region?
An AWS Region is a **geographical area** where AWS has **multiple data centers**.

Each region is:
- Physically separate
- Isolated from other regions
- Designed for fault tolerance

### Examples
- us-east-1 (North Virginia)
- eu-west-1 (Ireland)
- ap-south-1 (Mumbai)

### Why Regions Exist
- Serve users closer to their location
- Meet data residency and compliance requirements
- Enable disaster recovery across regions

👉 **Choosing the right region is an architectural decision.**

---

## 🏢 Availability Zones (AZs)

### What is an Availability Zone?
An Availability Zone is:
- One or more data centers
- Located within a region
- Isolated from failures in other AZs

Each region has **multiple AZs**.

### Why AZs Matter
AZs allow you to:
- Design highly available applications
- Protect against data center failures
- Run services across independent power and networking

### Real-World Example
If one AZ fails:
- Traffic automatically shifts to another AZ
- Application remains available

👉 This is **how AWS designs for failure**.

---

## 🌐 Edge Locations

### What is an Edge Location?
Edge Locations are:
- Data centers located close to end users
- Used mainly for content delivery and DNS

### AWS Services Using Edge Locations
- CloudFront
- Route 53
- AWS Shield

### Why Edge Locations Matter
- Reduce latency
- Improve user experience
- Protect against DDoS attacks

Example:
- Static website content loads faster globally
- DNS queries resolve quickly

---

## How These Pieces Work Together

| Component | Purpose |
|--------|--------|
| Region | Geographic isolation & compliance |
| Availability Zone | High availability & fault tolerance |
| Edge Location | Low latency & fast content delivery |

Together, they form the **backbone of AWS reliability**.

---

## Common Architecture Pattern

A typical production architecture:
- Application deployed across **multiple AZs**
- Data replicated across AZs
- Content delivered via **Edge Locations**
- Disaster recovery in another **Region**

This is **standard AWS design**, not optional.

---

## Common Interview Mistakes

❌ “AZs are just different rooms in the same building”  
✅ AZs are **physically separate data centers**  

❌ “Regions are only for pricing”  
✅ Regions affect **latency, compliance, and DR**

Interviewers love candidates who get this right.

---

## Key Takeaways

- AWS infrastructure is global and distributed
- Regions = geographic isolation
- AZs = high availability
- Edge Locations = performance and protection
- Architecture decisions depend heavily on this

---

📌 **Next:** AWS Shared Responsibility Model
