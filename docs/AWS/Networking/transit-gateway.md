---
sidebar_position: 9
title: Transit Gateway
---

# AWS Transit Gateway

As AWS environments grow, **VPC Peering stops scaling**.

AWS Transit Gateway (TGW) is designed to solve **large-scale networking** problems by acting as a **central hub** for connectivity.

If VPC Peering is a point-to-point bridge,
👉 **Transit Gateway is a hub-and-spoke network router**.

---

## Why Transit Gateway Exists

Problems with VPC Peering at scale:
- Too many peering connections
- Complex route tables
- No transitive routing
- Hard to manage

Transit Gateway exists to:
- Simplify network topology
- Enable transitive routing
- Centralize connectivity

👉 TGW is built for **enterprise AWS environments**.

---

## What Is a Transit Gateway? (Simple Explanation)

A Transit Gateway:
- Is a **regional network hub**
- Connects multiple VPCs, VPNs, and Direct Connect
- Supports transitive routing

In simple terms:
> **Transit Gateway = central router for AWS networks**

---

## How Transit Gateway Works

High-level flow:
1. Create a Transit Gateway
2. Attach VPCs, VPNs, or Direct Connect
3. Configure route tables
4. Traffic flows through the hub

All connected networks can communicate:
- According to routing rules
- Without direct peering

---

## Transit Gateway Attachments

TGW supports multiple attachment types:

- VPC attachments
- Site-to-Site VPN attachments
- Direct Connect Gateway attachments
- Peering attachments (TGW-to-TGW)

This allows **hybrid and multi-region networking**.

---

## Transit Gateway Route Tables

TGW uses its own route tables:
- Separate from VPC route tables
- Control traffic between attachments

This enables:
- Network segmentation
- Shared services
- Fine-grained traffic control

---

## Common Architecture Pattern (Hub-and-Spoke)

Typical enterprise setup:
- Hub VPC (shared services, firewalls)
- Spoke VPCs (applications)
- Transit Gateway in the middle

Benefits:
- Simplified routing
- Centralized security
- Easy scaling

---

## Transit Gateway vs VPC Peering

| Feature | Transit Gateway | VPC Peering |
|------|----------------|-------------|
| Scale | High | Low |
| Transitive routing | Yes | No |
| Management | Centralized | Distributed |
| Use case | Enterprise | Small setups |

👉 Use TGW when networking grows beyond a few VPCs.

---

## Security Considerations

- Security Groups still apply
- NACLs still apply
- TGW controls **routing**, not firewall rules

For inspection:
- Use firewall appliances in hub VPC

---

## Cost Considerations

Transit Gateway:
- Has hourly attachment cost
- Charges for data processing

👉 More expensive than peering, but far more scalable.

---

## Common Beginner Mistakes

- Using TGW for small setups unnecessarily
- Forgetting TGW route tables
- Ignoring cost implications
- Expecting TGW to replace security controls

These mistakes lead to:
- Higher cost
- Broken routing

---

## Interview Tip

If asked:
> “How do you connect many VPCs together?”

Strong answer:
> By using AWS Transit Gateway to create a hub-and-spoke network with centralized routing.

That answer signals **enterprise-level AWS networking knowledge**.

---

## Key Takeaways

- Transit Gateway is a central network hub
- Enables transitive routing
- Scales to large environments
- Core service for enterprise networking
- Complements VPC Peering

---

📌 **Next:** AWS VPN and Direct Connect
