---
sidebar_position: 4
title: Internet Gateway and NAT Gateway
---

# Internet Gateway and NAT Gateway

One of the most important networking concepts in AWS is **how resources access the internet**.

AWS solves this using two different gateways:
- **Internet Gateway (IGW)** – inbound & outbound internet access
- **NAT Gateway** – outbound-only internet access

Understanding the difference is **mandatory for secure VPC design**.

---

## Why Gateways Exist

By default:
- Resources inside a VPC **cannot access the internet**
- The internet **cannot reach your VPC**

Gateways act as **controlled doors** between your VPC and the internet.

👉 Nothing is public unless you explicitly make it public.

---

## 🌍 Internet Gateway (IGW)

### What Is an Internet Gateway?
An Internet Gateway is a **VPC-level component** that allows:
- Resources to access the internet
- The internet to access resources (if allowed)

Think of IGW as:
> A two-way door between your VPC and the internet

---

## Requirements for Internet Access via IGW

For an EC2 instance to be publicly reachable:
1. VPC must have an Internet Gateway attached
2. Subnet route table must have:
```
0.0.0.0/0 → Internet Gateway
```
3. Instance must have a **public IP**
4. Security Group must allow traffic

👉 Missing any one of these = **no internet access**.

---

## When to Use Internet Gateway

Use IGW for:
- Load balancers
- Bastion hosts
- Public APIs
- Web frontends

⚠️ Never attach IGW routes to private subnets.

---

## 🔐 NAT Gateway

### What Is a NAT Gateway?
A NAT Gateway allows:
- Instances in **private subnets**
- To access the internet **outbound only**
- Without being reachable from the internet

Think of NAT as:
> A one-way door (outbound only)

---

## Why NAT Gateway Exists

Private instances often need:
- OS updates
- Package downloads
- External API access

But:
- They should NOT be exposed publicly

NAT Gateway solves this securely.

---

## How NAT Gateway Works

Typical flow:
1. Private EC2 sends request
2. Route table sends traffic to NAT Gateway
3. NAT Gateway sends traffic to the internet
4. Response flows back via NAT

Internet **never initiates** traffic to private EC2.

---

## NAT Gateway Requirements

To use a NAT Gateway:
- NAT Gateway must be in a **public subnet**
- Public subnet must have route to IGW
- Private subnet route table must have:
```
0.0.0.0/0 → NAT Gateway
```

---

## NAT Gateway vs NAT Instance

| Feature | NAT Gateway | NAT Instance |
|------|-------------|-------------|
| Managed by AWS | Yes | No |
| Availability | Highly available | Manual |
| Scaling | Automatic | Manual |
| Maintenance | None | Required |
| Recommendation | ✅ Use | ❌ Avoid |

👉 Always prefer **NAT Gateway**.

---

## Common Architecture Pattern

Typical secure VPC:
- Public subnets → ALB, NAT Gateway
- Private subnets → App servers, databases
- IGW attached to VPC
- NAT Gateway per AZ

This provides:
- Security
- High availability
- Controlled internet access

---

## Common Beginner Mistakes

- Placing NAT Gateway in private subnet
- Using IGW for private instances
- Forgetting public IP on NAT Gateway subnet
- Single NAT Gateway for all AZs (no HA)

These mistakes cause:
- No internet access
- Security risks
- Single points of failure

---

## Interview Tip

If asked:
> “How do private EC2 instances access the internet?”

Strong answer:
> Using a NAT Gateway placed in a public subnet with proper route table configuration.

This shows **solid AWS networking understanding**.

---

## Key Takeaways

- IGW enables public internet access
- NAT Gateway enables private outbound access
- Public vs private depends on routing
- Gateways are critical for VPC security
- Correct placement is essential

---

📌 **Next:** Security Groups
