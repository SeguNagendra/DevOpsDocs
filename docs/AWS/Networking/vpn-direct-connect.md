---
sidebar_position: 10
title: VPN and Direct Connect
---

# AWS VPN and Direct Connect

Many organizations need to connect their **on-premises data centers** to AWS.

AWS provides two main services for this:
- **Site-to-Site VPN** – quick, encrypted internet-based connection
- **AWS Direct Connect** – dedicated private network connection

Choosing the right option depends on **security, performance, and cost**.

---

## Why Hybrid Connectivity Exists

Not everything moves to the cloud at once:
- Legacy systems stay on-prem
- Compliance requires local systems
- Gradual cloud migration is common

AWS VPN and Direct Connect exist to:
- Enable hybrid architectures
- Extend on-prem networks to AWS
- Provide secure connectivity

---

## 🔐 Site-to-Site VPN

### What Is Site-to-Site VPN?
Site-to-Site VPN creates an **encrypted tunnel over the internet** between:
- Your on-premises network
- Your AWS VPC

In simple terms:
> **VPN = secure tunnel over the public internet**

---

## How Site-to-Site VPN Works

High-level flow:
1. Customer Gateway (on-prem router)
2. Virtual Private Gateway or Transit Gateway (AWS)
3. IPSec encrypted tunnels
4. Traffic flows securely

AWS creates **two tunnels** for high availability.

---

## When to Use Site-to-Site VPN

Best for:
- Quick setup
- Small to medium traffic
- Dev/Test environments
- Backup connectivity

Advantages:
- Fast to deploy
- Lower cost
- Secure (encrypted)

Limitations:
- Internet-dependent
- Variable latency
- Limited bandwidth

---

## 🏢 AWS Direct Connect

### What Is Direct Connect?
AWS Direct Connect is a **dedicated private network connection** between:
- Your data center
- AWS

In simple terms:
> **Direct Connect = private highway to AWS**

---

## How Direct Connect Works

- Physical connection to AWS location
- Dedicated bandwidth (1 Gbps, 10 Gbps, etc.)
- Traffic bypasses public internet

Provides:
- Consistent latency
- Higher throughput
- Reliable performance

---

## When to Use Direct Connect

Best for:
- Large data transfers
- Low-latency requirements
- Enterprise workloads
- Hybrid production environments

Advantages:
- Predictable performance
- Reduced network jitter
- More stable than VPN

Limitations:
- Higher cost
- Longer setup time
- Physical dependency

---

## VPN vs Direct Connect (Comparison)

| Feature | Site-to-Site VPN | Direct Connect |
|------|-----------------|----------------|
| Connection | Internet | Private |
| Setup time | Fast | Slow |
| Bandwidth | Limited | High |
| Latency | Variable | Predictable |
| Cost | Low | High |
| Encryption | Yes | Optional |

👉 Many enterprises use **both together**.

---

## Common Hybrid Architecture Pattern

Best practice:
- Direct Connect for primary traffic
- VPN as backup (failover)

This provides:
- Reliability
- Security
- High availability

---

## Security Considerations

- VPN traffic is always encrypted
- Direct Connect can use MACsec or VPN overlay
- IAM and VPC security still apply

Networking does NOT replace security controls.

---

## Common Beginner Mistakes

- Using VPN for high-throughput production workloads
- Expecting Direct Connect to be instant
- Ignoring redundancy
- Not planning failover

These mistakes cause:
- Performance issues
- Downtime

---

## Interview Tip

If asked:
> “How do you connect on-premises to AWS?”

Strong answer:
> Using Site-to-Site VPN for quick encrypted connectivity and AWS Direct Connect for high-performance, dedicated network access.

This shows **hybrid-cloud understanding**.

---

## Key Takeaways

- VPN uses the public internet securely
- Direct Connect is private and high-performance
- Choose based on workload needs
- Hybrid architectures are common
- Often used together for reliability

---

📌 **Next:** Phase 04 – IAM (Identity and Access Management)
