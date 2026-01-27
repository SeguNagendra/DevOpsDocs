---
sidebar_position: 6
title: Network ACLs (NACLs)
---

# Network ACLs (NACLs)

Network ACLs (NACLs) are an **optional but powerful layer of network security** in AWS.
They operate at the **subnet level** and provide **stateless traffic control**.

If Security Groups are your **first line of defense**,
👉 NACLs are your **coarse-grained perimeter rules**.

---

## What Is a Network ACL? (Simple Explanation)

A Network ACL:
- Is attached to a **subnet**
- Controls inbound and outbound traffic
- Uses numbered rules with allow **and deny**
- Is **stateless**

In simple terms:
> **NACL = stateless firewall for subnets**

---

## Why NACLs Exist

Security Groups are:
- Resource-level
- Allow-only
- Stateful

NACLs exist to:
- Provide an extra security layer
- Block traffic explicitly
- Apply rules across an entire subnet

👉 Used mainly in **high-security environments**.

---

## Key Characteristics (Very Important)

### 1. Stateless
- Inbound and outbound rules are evaluated separately
- You must allow **return traffic explicitly**

👉 This is the biggest difference from Security Groups.

---

### 2. Allow and Deny Rules
- NACLs support explicit **DENY**
- Useful for blocking known bad IPs

---

### 3. Rule Order Matters
- Rules are evaluated in ascending order
- First match wins

Example:
- Rule 100: DENY 1.2.3.4
- Rule 200: ALLOW 0.0.0.0/0

---

## Default NACL

Every VPC has a **default NACL**:
- Allows all inbound traffic
- Allows all outbound traffic

👉 Default NACL is permissive.

---

## Custom NACL

Best practice:
- Create custom NACLs for control
- Explicitly allow required traffic
- Deny everything else

But:
- Be careful — misconfiguration causes outages

---

## NACL vs Security Group (Very Important)

| Feature | Security Group | NACL |
|------|---------------|------|
| Scope | Resource | Subnet |
| Stateful | Yes | No |
| Rules | Allow only | Allow & Deny |
| Rule Order | No | Yes |
| Complexity | Low | Medium |

👉 Use **Security Groups first**, NACLs only if needed.

---

## Common Use Cases for NACLs

- Blocking malicious IP ranges
- Compliance-driven network controls
- Extra protection for public subnets

NACLs are **not required for most workloads**.

---

## Common Beginner Mistakes

- Forgetting outbound return rules
- Blocking ephemeral ports
- Overusing NACLs unnecessarily
- Assuming NACLs replace Security Groups

These mistakes cause:
- Broken connectivity
- Hard-to-debug issues

---

## Interview Tip

If asked:
> “Difference between Security Groups and NACLs?”

Strong answer:
> Security Groups are stateful and resource-level, while NACLs are stateless, subnet-level, and support explicit deny rules.

That answer is **short, clear, and correct**.

---

## Key Takeaways

- NACLs are stateless subnet firewalls
- Rule order matters
- Support allow and deny
- Used as an extra security layer
- Not required for most architectures

---

📌 **Next:** VPC Endpoints
