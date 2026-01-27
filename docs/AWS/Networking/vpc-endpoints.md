---
sidebar_position: 7
title: VPC Endpoints
---

# VPC Endpoints

VPC Endpoints allow resources inside a VPC to **privately connect to AWS services** without using:
- The public internet
- Internet Gateways
- NAT Gateways

If security teams ask:
> “Can we access AWS services **without internet exposure**?”

👉 **VPC Endpoints are the answer.**

---

## Why VPC Endpoints Exist

Without VPC Endpoints:
- Private subnets need NAT Gateways
- Traffic goes over the public internet
- Security and compliance risks increase
- NAT Gateway costs add up

VPC Endpoints exist to:
- Keep traffic inside AWS network
- Improve security posture
- Reduce cost
- Simplify network architecture

---

## What Is a VPC Endpoint? (Simple Explanation)

A VPC Endpoint is:
- A private connection between your VPC and an AWS service
- Traffic never leaves the AWS backbone network

In simple terms:
> **VPC Endpoint = private access to AWS services**

---

## Types of VPC Endpoints

AWS provides **two types** of VPC Endpoints:

1. Gateway Endpoints  
2. Interface Endpoints  

Each is used for **different services**.

---

## 🚪 Gateway Endpoints

### Supported Services
- Amazon S3
- Amazon DynamoDB

### How They Work
- Added as a target in route tables
- No ENIs created
- No security groups involved

### Best For
- High-throughput S3/DynamoDB access
- Cost optimization
- Simple private access

👉 Gateway Endpoints are **free**.

---

## 🔌 Interface Endpoints

### Supported Services
- Most AWS services (EC2, CloudWatch, SNS, SQS, etc.)
- AWS PrivateLink

### How They Work
- Create elastic network interfaces (ENIs)
- Use private IPs in your subnets
- Controlled by security groups

### Best For
- Private access to AWS APIs
- Highly secure architectures

⚠️ Interface Endpoints have **hourly and data processing costs**.

---

## Gateway vs Interface Endpoints

| Feature | Gateway Endpoint | Interface Endpoint |
|------|-----------------|-------------------|
| Services | S3, DynamoDB | Most AWS services |
| Cost | Free | Paid |
| Network | Route table | ENI |
| Security Groups | No | Yes |
| Traffic | AWS backbone | AWS backbone |

---

## Common VPC Endpoint Use Cases

- Private S3 access from EC2
- Private Lambda access to AWS APIs
- Compliance environments (no internet)
- Reducing NAT Gateway costs

VPC Endpoints are **standard in secure AWS architectures**.

---

## Security Benefits

VPC Endpoints:
- Eliminate internet exposure
- Work with IAM policies
- Support endpoint policies

👉 Endpoint policies further restrict service access.

---

## Common Beginner Mistakes

- Using NAT Gateway instead of VPC Endpoint
- Forgetting to update route tables (Gateway endpoint)
- Ignoring endpoint policies
- Creating endpoints in wrong subnets

These mistakes cause:
- Higher costs
- Broken connectivity

---

## Interview Tip

If asked:
> “How do you access S3 privately from a VPC?”

Strong answer:
> By using a VPC Gateway Endpoint for S3 so traffic stays within the AWS network.

That answer shows **strong AWS networking knowledge**.

---

## Key Takeaways

- VPC Endpoints enable private AWS access
- Two types: Gateway and Interface
- Improve security and reduce cost
- Essential for private subnet architectures
- Common in enterprise environments

---

📌 **Next:** VPC Peering
