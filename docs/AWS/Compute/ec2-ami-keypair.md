---
sidebar_position: 3
title: EC2 AMI and Key Pairs
---

# EC2 AMI and Key Pairs

When you launch an EC2 instance, AWS asks two very important questions:
1. **What software should be installed?**
2. **How will you securely log in?**

AMI answers the first question.  
Key Pairs answer the second.

If you understand these two concepts well, EC2 becomes **much clearer**.

---

## What Is an AMI? (Amazon Machine Image)

An AMI is a **template** used to create an EC2 instance.

It contains:
- Operating system (Linux, Windows)
- Pre-installed software (optional)
- Configuration settings

Think of an AMI as:
> A **golden image** used to create servers consistently.

---

## Why AMIs Are Important

Without AMIs:
- Every server setup would be manual
- Configurations would drift
- Scaling would be slow

With AMIs:
- Instances launch quickly
- Servers are consistent
- Scaling becomes reliable

👉 AMIs are the foundation of **automation and scalability**.

---

## Types of AMIs

### 1. AWS-Provided AMIs
- Amazon Linux
- Ubuntu
- Windows Server

Best for:
- Beginners
- Standard workloads

---

### 2. Marketplace AMIs
- Pre-configured software (NGINX, Docker, etc.)
- Third-party images

⚠️ Some marketplace AMIs are **paid**.

---

### 3. Custom AMIs
- Created by you
- Based on existing EC2 instances

Best for:
- Production environments
- Auto Scaling Groups
- Standardized deployments

---

## Real-World AMI Usage

Typical production flow:
1. Launch EC2
2. Install and configure application
3. Create a custom AMI
4. Use AMI in Auto Scaling

This ensures **every server is identical**.

---

## What Is a Key Pair?

A key pair is used for **secure authentication** to an EC2 instance.

It consists of:
- **Public key** (stored by AWS)
- **Private key** (downloaded by you)

AWS uses **SSH key-based authentication**, not passwords.

---

## Why Key Pairs Matter

Key pairs:
- Are more secure than passwords
- Prevent brute-force attacks
- Are required for Linux EC2 access

👉 Lose the private key = lose access (unless recovery steps are taken).

---

## How Key Pairs Work (Simple Flow)

1. You create a key pair
2. AWS stores the public key
3. Private key is downloaded once
4. You use the private key to connect via SSH

AWS **never stores your private key**.

---

## Common Beginner Mistakes

- Losing the private key
- Sharing private keys
- Using the same key everywhere
- Not restricting SSH access

👉 Treat private keys like **passwords**.

---

## AMI vs Snapshot (Common Confusion)

| AMI | Snapshot |
|----|---------|
| Full instance template | Disk backup |
| Used to launch EC2 | Used to restore data |
| Includes OS & config | Storage-only |

Both are related but **not the same**.

---

## Interview Tip

If asked:
> “How do you ensure EC2 instances are identical?”

Strong answer:
> By creating custom AMIs and using them in Auto Scaling Groups.

That shows **real-world AWS experience**.

---

## Key Takeaways

- AMI = blueprint for EC2
- Key pairs enable secure access
- Custom AMIs improve consistency
- Never lose private keys
- Critical for automation

---

📌 **Next:** EC2 User Data and Metadata
