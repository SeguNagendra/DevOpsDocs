---
sidebar_position: 5
title: DNS
description: Understand DNS like a mentor would explain it — simple, practical, and focused on real outages.
---

# DNS (Why It Breaks So Often)

## Mentor Truth Up Front

If an application is down, slow, or behaving strangely,
**DNS is guilty more often than people expect**.

DNS problems don’t always look like DNS problems.
They look like:
- Timeouts
- Random failures
- “Works from my laptop but not from server”

That’s why DNS deserves its own module.

---

## What DNS Really Does

DNS is just:
> “A phonebook for the internet.”

Humans remember names.  
Machines talk using IP addresses.

DNS connects the two.

```
google.com  →  142.250.xxx.xxx
```

Without DNS, you’d be typing IP addresses everywhere.
Nobody wants that.

---

## Why DNS Is a Critical Dependency

Almost everything depends on DNS:
- Websites
- APIs
- Databases
- Microservices
- Kubernetes services
- Cloud resources

If DNS is slow or wrong, **everything above it suffers**.

---

## DNS Resolution Flow (Simple and Calm)

When a client asks for a domain:

1. Client checks local cache
2. Asks configured DNS server
3. Resolver finds the correct IP
4. IP is returned to client
5. Client connects to that IP

If this flow breaks at any point, name resolution fails.

---

## Common DNS Record Types (You Actually Use)

### A Record
- Maps name → IPv4 address
- Most common record

### AAAA Record
- Maps name → IPv6 address

### CNAME
- Alias to another domain
- Common with cloud services

### MX Record
- Used for email routing

You don’t need more than this for DevOps work.

---

## Internal DNS vs External DNS

### External DNS
- Public internet names
- Used by users and browsers

### Internal DNS
- Used inside VPCs, clusters, networks
- Critical for microservices

Many outages happen because **internal DNS is misconfigured**.

---

## DNS in Cloud (Important Reality)

Cloud providers give managed DNS:
- Private hosted zones
- Public hosted zones
- Internal resolution

But the logic is the same:
> Name → IP

Cloud just hides the servers.

---

## DNS in Kubernetes (Why People Get Confused)

In Kubernetes:
- Services get DNS names
- Pods change IPs frequently
- DNS provides stability

If DNS breaks in Kubernetes:
- Pods look healthy
- Traffic fails silently

This confuses beginners a lot.

---

## Common DNS Failure Patterns

Here are real-world issues I’ve seen many times:

- DNS points to old IP
- Cached wrong record
- TTL too high
- Wrong resolver configured
- Split-horizon DNS confusion

DNS failures are often **slow and subtle**, not loud.

---

## How to Debug DNS (Mentor Checklist)

When DNS is suspected, ask:

1. Does name resolve?
2. Does it resolve to the correct IP?
3. Is resolution slow?
4. Is DNS different from another machine?
5. Is cache involved?

Never guess — always verify.

---

## Tools You’ll Actually Use

- `nslookup`
- `dig`
- `host`
- `resolv.conf`

These tools tell you:
- What DNS server is used
- What IP is returned
- How long resolution takes

---

## Mentor Rule About DNS

If something:
- Works by IP
- Fails by name

Then:
> It is almost always DNS.

Remember this rule. It saves hours.

---

## Key Takeaway

DNS is simple in concept but powerful in impact.

When DNS breaks:
- Everything above it looks broken
- Logs lie
- Metrics mislead

Understanding DNS makes you calm during chaos.
