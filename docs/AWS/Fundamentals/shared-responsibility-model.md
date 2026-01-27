---
sidebar_position: 6
title: AWS Shared Responsibility Model
---

# AWS Shared Responsibility Model

One of the **most misunderstood concepts in AWS** is the **Shared Responsibility Model**.

Many security incidents happen **not because AWS failed**, but because **customers misunderstood their responsibilities**.

This model clearly defines:
- What **AWS is responsible for**
- What **you (the customer) are responsible for**

---

## Simple One-Line Explanation (Interview Gold)

> AWS is responsible for **security of the cloud**, and customers are responsible for **security in the cloud**.

Let’s unpack this properly.

---

## Why the Shared Responsibility Model Exists

AWS runs:
- Data centers
- Physical servers
- Global infrastructure

You run:
- Applications
- Data
- Configurations

Both parties must play their role to keep systems **secure and reliable**.

---

## AWS Responsibility: Security *OF* the Cloud

AWS is responsible for protecting the **underlying infrastructure**.

### AWS takes care of:
- Physical data centers
- Physical servers and storage
- Networking hardware
- Power, cooling, and facilities
- Physical access controls

👉 You **never** worry about:
- Server theft
- Data center guards
- Hardware failures

That’s AWS’s job.

---

## Customer Responsibility: Security *IN* the Cloud

You are responsible for **everything you configure and deploy**.

### You take care of:
- Operating systems (patching, updates)
- Applications and code
- IAM users, roles, and permissions
- Network security (Security Groups, NACLs)
- Data encryption
- Backup and recovery

👉 Most security breaches happen **here**, not at AWS’s side.

---

## Responsibility Changes by Service Type

Your responsibility **depends on the AWS service you use**.

---

### IaaS Example – EC2

**AWS manages:**
- Physical servers
- Data center security

**You manage:**
- OS patching
- Firewall rules
- Applications
- Data protection

👉 EC2 gives you **maximum control**, but also **maximum responsibility**.

---

### PaaS Example – RDS

**AWS manages:**
- Infrastructure
- Operating system
- Database engine

**You manage:**
- Database configuration
- User access
- Backups (configuration)
- Data security

👉 Less operational work, but **still not zero responsibility**.

---

### SaaS Example – Amazon WorkSpaces / Office tools

**AWS manages:**
- Almost everything

**You manage:**
- User access
- Data usage

👉 Responsibility is minimal, but **not zero**.

---

## Real-World Scenario

❌ EC2 instance hacked because:
- SSH open to the internet
- Weak credentials
- No patching

Was AWS responsible?  
➡️ **No.** This was a customer responsibility.

This clarity saves companies from **blame and downtime**.

---

## Common Interview Traps

❌ “AWS is responsible for security”  
✅ AWS is responsible for **part** of security  

❌ “Managed services remove all responsibility”  
✅ They **reduce**, not eliminate responsibility  

Interviewers love candidates who explain this clearly.

---

## Visual Way to Remember

- AWS → Hardware, facilities, infrastructure
- You → Configuration, access, data, applications

If you can explain this in simple words, you **understand AWS security basics**.

---

## Key Takeaways

- Security is a shared responsibility
- AWS secures the cloud infrastructure
- Customers secure what they deploy
- Responsibility shifts with service type
- Misunderstanding this causes security incidents

---

📌 **Next:** AWS Pricing Models
