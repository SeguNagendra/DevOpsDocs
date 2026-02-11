---
sidebar_position: 10
title: Firewalls, NAT & Security (Why Traffic Gets Blocked)
description: Learn firewalls and NAT the calm, practical way — focused on why traffic is blocked in real systems.
---

# Firewalls, NAT & Security (Why Traffic Gets Blocked)

## Mentor Truth

When traffic fails, many people say:
> “Network is down.”

Most of the time, the network is **working perfectly**.
It is doing exactly what it was told to do:
**block traffic**.

Firewalls and NAT are usually the reason.

---

## What a Firewall Really Is

A firewall is simply:
> “A rule engine for network traffic.”

It looks at:
- Source
- Destination
- Port
- Protocol

Then decides:
- Allow
- Deny

Firewalls don’t care if your app is important.
Rules decide everything.

---

## Inbound vs Outbound Traffic

This distinction is critical.

### Inbound
- Traffic coming **into** a server
- Example: user accessing a website

### Outbound
- Traffic leaving a server
- Example: server calling an API or database

Many issues happen because:
- Inbound is allowed
- Outbound is forgotten

Traffic goes out — responses never come back.

---

## Stateful vs Stateless Firewalls

### Stateful Firewall
- Remembers previous traffic
- Allows response automatically
- Easier to manage

Example:
- Cloud Security Groups

### Stateless Firewall
- Checks every packet
- Needs explicit allow rules both ways
- More error-prone

Example:
- Network ACLs

Both are useful when used correctly.

---

## What Is NAT (Simple Explanation)

NAT stands for Network Address Translation.

It exists because:
> Private IPs cannot talk directly to the internet.

NAT translates:
- Private IP → Public IP

This allows:
- Outbound internet access
- Without exposing private machines

---

## SNAT vs DNAT (Only What You Need)

### SNAT (Source NAT)
- Used for outbound traffic
- Private subnet accessing internet
- Very common in cloud

### DNAT (Destination NAT)
- Used for inbound traffic
- Maps public IP to private server
- Used by load balancers

If NAT is missing or wrong, traffic silently fails.

---

## NAT Gateway vs Internet Gateway (Cloud View)

- **Internet Gateway**
  - Allows public subnets to access internet
  - Requires public IP

- **NAT Gateway**
  - Allows private subnets outbound access
  - Blocks inbound traffic

Confusing these two causes many outages.

---

## Bastion Host (Security Pattern)

A bastion host is:
> “A controlled entry point into private networks.”

Instead of:
- Exposing every server

You:
- Expose one hardened machine
- Access others through it

This reduces attack surface.

---

## Why Security Breaks Applications

Security is invisible when it works.

When it breaks, apps:
- Time out
- Hang
- Fail silently

Logs often show nothing.

That’s why security issues feel mysterious.

---

## Common Real-World Failures

Seen many times:

- Security group allows inbound, blocks outbound
- NACL blocks ephemeral ports
- NAT gateway missing route
- Firewall allows TCP but blocks UDP
- Health checks blocked by firewall

Everything looks green — users still fail.

---

## Mentor Debugging Checklist

When traffic is blocked, ask:

1. Is inbound allowed?
2. Is outbound allowed?
3. Is the correct protocol allowed?
4. Is NAT required?
5. Is return traffic allowed?

Never assume defaults.

---

## Zero Trust (Conceptual Only)

Modern systems follow:
> “Never trust, always verify.”

This means:
- Explicit rules
- Minimal access
- Identity-aware networking

You don’t configure Zero Trust here,
but you should understand the mindset.

---

## Key Takeaway

Firewalls and NAT do not break systems.
**Misconfigured rules do.**

If traffic fails:
- Check security before blaming code
- Think both directions
- Verify, don’t guess

Understanding security makes you calm during outages.

---

### End of Module 10
