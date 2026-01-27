---
sidebar_position: 5
title: Security Groups
---

# Security Groups

Security Groups are the **first and most important layer of network security** in AWS.

They act as a **virtual firewall** that controls:
- What traffic is allowed **into** a resource
- What traffic is allowed **out of** a resource

If you understand Security Groups well, you avoid **most AWS security mistakes**.

---

## What Is a Security Group? (Simple Explanation)

A Security Group:
- Is attached to AWS resources (EC2, ALB, RDS, etc.)
- Contains inbound and outbound rules
- Allows traffic explicitly

In simple terms:
> **Security Group = stateful firewall for AWS resources**

---

## Why Security Groups Exist

Without Security Groups:
- All resources would be exposed
- Fine-grained access control would be impossible

Security Groups exist to:
- Restrict access
- Reduce attack surface
- Enforce least privilege networking

👉 Nothing is allowed unless you allow it.

---

## Key Characteristics (Very Important)

### 1. Stateful
- If inbound traffic is allowed, response traffic is automatically allowed
- You don’t need to add outbound rules for responses

👉 This is a **huge difference** from NACLs.

---

### 2. Allow Rules Only
- Security Groups do **not support deny rules**
- Anything not explicitly allowed is denied

---

### 3. Resource-Level
- Applied to instances or services
- Not applied at subnet level

---

## Inbound and Outbound Rules

### Inbound Rules
Control:
- Who can access the resource
- From where
- On which port/protocol

Example:
- Allow HTTP (80) from Load Balancer SG
- Allow SSH (22) from admin IP

---

### Outbound Rules
Control:
- Where the resource can send traffic

Default:
- Allow all outbound traffic

Best practice:
- Restrict outbound traffic when possible

---

## Referencing Other Security Groups (Best Practice)

Instead of allowing IP ranges, you can:
- Reference another Security Group

Example:
- Allow traffic from ALB Security Group to EC2 Security Group

Benefits:
- Dynamic scaling support
- More secure than IP-based rules

👉 This is **standard production practice**.

---

## Common Security Group Examples

### Web Server SG
- Inbound: 80/443 from ALB SG
- Inbound: 22 from admin IP
- Outbound: limited

### Database SG
- Inbound: DB port from App SG only
- No public access

---

## Security Groups vs NACLs (Preview)

| Feature | Security Group | NACL |
|------|---------------|------|
| Scope | Resource | Subnet |
| Rules | Allow only | Allow & Deny |
| Stateful | Yes | No |
| Complexity | Simple | Advanced |

👉 Use Security Groups for **most security needs**.

---

## Common Beginner Mistakes

- Opening ports to 0.0.0.0/0
- Using one SG for everything
- Allowing SSH from anywhere
- Ignoring outbound rules

These mistakes cause:
- Security breaches
- Compliance failures

---

## Interview Tip

If asked:
> “How do Security Groups work?”

Strong answer:
> Security Groups are stateful virtual firewalls that control inbound and outbound traffic at the resource level using allow rules only.

This shows **clear AWS networking understanding**.

---

## Key Takeaways

- Security Groups are stateful firewalls
- Default deny, explicit allow
- Applied to resources, not subnets
- SG-to-SG referencing is best practice
- Core AWS security concept

---

📌 **Next:** Network ACLs (NACLs)
