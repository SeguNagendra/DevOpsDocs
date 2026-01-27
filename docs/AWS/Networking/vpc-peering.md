---
sidebar_position: 8
title: VPC Peering
---

# VPC Peering

VPC Peering allows **two VPCs to communicate privately** using the AWS network.

It is commonly used when:
- Applications are split across VPCs
- Teams manage separate VPCs
- You want private, low-latency connectivity

👉 No internet, no VPN, no gateways required.

---

## Why VPC Peering Exists

Without VPC Peering, VPC-to-VPC communication would require:
- Internet Gateway + public IPs
- VPN tunnels
- Complex routing

VPC Peering exists to:
- Keep traffic private
- Reduce latency
- Simplify architecture

---

## What Is VPC Peering? (Simple Explanation)

A VPC Peering connection:
- Connects two VPCs privately
- Allows traffic using private IPs
- Uses AWS backbone network

In simple terms:
> **VPC Peering = private network bridge between VPCs**

---

## Key Characteristics (Very Important)

- Traffic stays within AWS
- No single point of failure
- No bandwidth bottleneck
- No transitive routing

⚠️ **No transitive routing** is a critical limitation.

---

## How VPC Peering Works

High-level flow:
1. Create peering request
2. Accept peering request
3. Update route tables in both VPCs
4. Allow traffic via Security Groups / NACLs

👉 Missing route updates = no connectivity.

---

## CIDR Requirements

Peered VPCs:
- **Must not have overlapping CIDR blocks**

If CIDRs overlap:
- Peering will fail
- Requires re-architecture

👉 Plan CIDR carefully early.

---

## Intra-Region vs Inter-Region Peering

### Intra-Region
- VPCs in the same region
- Lower latency
- No data transfer cost

### Inter-Region
- VPCs in different regions
- Slightly higher latency
- Data transfer cost applies

---

## Common VPC Peering Use Cases

- Shared services VPC (logging, monitoring)
- Dev ↔ Prod communication
- Microservices across VPCs

Used heavily in **multi-team environments**.

---

## VPC Peering Limitations

Important limitations:
- No transitive routing
- No CIDR overlap
- Manual route table updates
- Not scalable for many VPCs

👉 For large-scale networking, use **Transit Gateway**.

---

## Security Considerations

- Peering does not bypass Security Groups
- Must explicitly allow traffic
- Least privilege networking applies

---

## Common Beginner Mistakes

- Forgetting route table updates
- Expecting transitive routing
- Overusing peering for many VPCs
- Ignoring CIDR overlap planning

These mistakes cause:
- Broken connectivity
- Complex troubleshooting

---

## Interview Tip

If asked:
> “How do two VPCs communicate privately?”

Strong answer:
> By using VPC Peering with non-overlapping CIDR blocks and proper route table configuration.

That answer shows **solid AWS networking understanding**.

---

## Key Takeaways

- VPC Peering enables private VPC-to-VPC communication
- Traffic stays on AWS backbone
- No transitive routing
- CIDR planning is critical
- Not suitable for large hub-and-spoke designs

---

📌 **Next:** Transit Gateway
