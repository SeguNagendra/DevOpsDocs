---
sidebar_position: 8
title: Networking Protocols
description: Learn networking protocols from a DevOps point of view — only what you really use, explained calmly.
---

# Networking Protocols (What Actually Matters)

## Mentor Reality Check

Protocols are just **rules of communication**.

Most people get overwhelmed because they try to learn *all* protocols.
You don’t need that.

As a DevOps engineer, you need to understand:
- Which protocol is being used
- Why it was chosen
- What breaks when it’s misused

That’s it.

---

## TCP vs UDP (This Matters a Lot)

This is one of the most important comparisons in networking.

### TCP (Transmission Control Protocol)

Think of TCP as:
> “I care about correctness.”

Characteristics:
- Connection-oriented
- Reliable delivery
- Retries and acknowledgements
- Slower but safe

Used by:
- HTTP / HTTPS
- Databases
- APIs
- SSH

If TCP traffic fails, apps usually hang or timeout.

---

### UDP (User Datagram Protocol)

Think of UDP as:
> “Speed over certainty.”

Characteristics:
- No connection
- No guarantee of delivery
- Very fast
- Lightweight

Used by:
- DNS
- Streaming
- Monitoring systems

UDP failures often look random.

---

## HTTP vs HTTPS

### HTTP
- Plain text
- No encryption
- Not safe for production

### HTTPS
- Encrypted using TLS
- Protects data
- Required everywhere today

**Mentor truth:**  
If HTTPS breaks, apps usually look “down” even if servers are fine.

---

## DNS (Protocol Perspective)

DNS is usually UDP.
Sometimes TCP is used when responses are large.

This explains why:
- DNS can be fast
- DNS can also fail silently

If you understand this, DNS debugging makes more sense.

---

## SSH (DevOps Lifeline)

SSH allows:
- Secure remote access
- Command execution
- Tunneling

If SSH fails:
- Networking or firewall is usually the cause
- Rarely the server itself

Knowing SSH behavior helps debug access issues quickly.

---

## ICMP (Ping)

Ping uses ICMP.

Important point:
- Ping working ≠ app working
- Ping failing ≠ network completely broken

Firewalls often block ICMP.

Don’t panic based on ping alone.

---

## FTP / SFTP (Practical Note)

- FTP is mostly legacy
- SFTP runs over SSH
- SFTP is preferred in production

If file transfers fail, protocol choice matters.

---

## Protocol + Port Relationship

Protocols don’t live alone.
They usually pair with ports.

Examples:
- HTTP → TCP 80
- HTTPS → TCP 443
- DNS → UDP 53
- SSH → TCP 22

Mismatch = silent failure.

---

## Common Protocol Misconfigurations

I’ve seen these many times:

- Using UDP where TCP is required
- Firewall allows port but blocks protocol
- Load balancer expects HTTP, app sends HTTPS
- Health checks using wrong protocol

Everything looks fine — traffic still fails.

---

## How DevOps Engineers Think About Protocols

Mentor mindset:
- What protocol is used?
- Why this protocol?
- Is the infrastructure expecting the same?

Never assume defaults.

---

## Debugging Tip

If traffic behaves:
- Randomly
- Inconsistently
- Differently across environments

Suspect protocol mismatch.

---

## Key Takeaway

Protocols define **how** data moves.

When you understand protocols:
- Failures make sense
- Debugging becomes logical
- Interviews become easy

You don’t need many protocols.
You just need to understand the right ones well.
