---
sidebar_position: 3
title: Route Tables
---

# Route Tables

Route Tables decide **where network traffic goes** inside a VPC.
You can think of them as the **traffic rules** of AWS networking.

Even if you design perfect subnets, **nothing works correctly without route tables**.

---

## Why Route Tables Matter

In AWS:
- Subnets don’t automatically know where to send traffic
- Internet access is **not enabled by default**
- Every packet follows routing rules

Route tables:
- Control inbound and outbound paths
- Decide internet access
- Enable private networking

👉 Route tables are **the heart of VPC traffic flow**.

---

## What Is a Route Table? (Simple Explanation)

A route table is a set of rules called **routes**.

Each route defines:
- **Destination CIDR**
- **Target** (where traffic should go)

Example route:
```
0.0.0.0/0 → Internet Gateway
```

Meaning:
- Send all internet-bound traffic to the Internet Gateway

---

## Default Route Table

Every VPC has a **default route table**.

Characteristics:
- Automatically created
- Associated with subnets unless changed
- Should NOT be used for production by default

👉 Best practice: **Create custom route tables**.

---

## Subnet Association (Very Important)

- Each subnet is associated with **one route table**
- One route table can be associated with **multiple subnets**

Traffic behavior of a subnet depends entirely on:
> The route table it is associated with

---

## Public Route Table

A subnet is considered **public** when its route table has:
```
0.0.0.0/0 → Internet Gateway (IGW)
```

Used for:
- Load balancers
- Bastion hosts
- NAT Gateways

---

## Private Route Table

A subnet is considered **private** when:
- It has NO route to Internet Gateway
- Or routes internet traffic via NAT Gateway

Example:
```
0.0.0.0/0 → NAT Gateway
```

Used for:
- Application servers
- Databases

👉 Private subnets can access the internet **without being exposed**.

---

## Route Table Targets (Common)

| Target | Purpose |
|-----|--------|
| Internet Gateway | Public internet access |
| NAT Gateway | Outbound internet for private subnets |
| VPC Peering | VPC-to-VPC traffic |
| Transit Gateway | Hub-and-spoke networking |
| VPC Endpoint | Private AWS service access |

---

## Local Route (Always Present)

Every route table has a default route:
```
VPC CIDR → local
```

This allows:
- Subnets to communicate within the VPC
- Private internal traffic

👉 You cannot delete this route.

---

## Common Beginner Mistakes

- Forgetting to associate route tables with subnets
- Adding IGW route to private subnets
- Using default route table everywhere
- Confusing security groups with routing

These mistakes cause:
- No internet access
- Security exposure
- Broken applications

---

## Real-World VPC Routing Pattern

Typical setup:
- Public route table → IGW
- Private route table → NAT Gateway
- Separate route tables per AZ

This ensures:
- Security
- High availability
- Clear traffic separation

---

## Interview Tip

If asked:
> “What makes a subnet public or private?”

Strong answer:
> A subnet is public if its route table has a route to an Internet Gateway; otherwise it is private.

That answer is **short and correct**.

---

## Key Takeaways

- Route tables control traffic flow
- Subnet behavior depends on route tables
- Public vs private is routing-based
- Local routes enable internal communication
- Critical for VPC design

---

📌 **Next:** Internet Gateway and NAT Gateway
