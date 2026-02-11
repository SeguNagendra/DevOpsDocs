---
sidebar_position: 15
title: Networking Troubleshooting (Production Playbook)
description: A calm, step-by-step networking troubleshooting playbook used by real engineers during incidents.
---

# Networking Troubleshooting (Production Playbook)

## Mentor Truth

When systems are down, panic makes things worse.

Good engineers don’t rush.
They **follow a playbook**.

Networking problems are stressful only when you don’t know where to start.

---

## The Golden Rule

Never debug randomly.

Always debug in **order**.

Skipping steps creates confusion and false conclusions.

---

## The Universal Troubleshooting Flow

Whenever something is “not reachable”, follow this exact order:

1. Is the server running?
2. Does it have an IP?
3. Can it be reached?
4. Does DNS resolve?
5. Is the port listening?
6. Is traffic allowed?
7. Is the app responding?

This flow works everywhere:
- On‑prem
- Cloud
- Kubernetes

---

## Step 1: Confirm the Target Exists

First ask:
> “Am I debugging a real thing?”

Check:
- VM / Pod is running
- Correct environment
- Correct region / cluster

Many incidents start with **wrong target**.

---

## Step 2: Check Identity & Reachability

Questions:
- Does it have an IP?
- Is the network interface up?
- Can I ping it?

If there’s no identity, nothing else matters.

---

## Step 3: Validate DNS

Ask:
- Does the name resolve?
- Does it resolve to the correct IP?
- Is DNS different from another machine?

DNS issues often look like app issues.

---

## Step 4: Verify Port & Protocol

Questions:
- Is the app listening?
- On the expected port?
- Using the correct protocol?

Very common failure point.

---

## Step 5: Check Firewalls & Security

Never forget:
- Inbound rules
- Outbound rules
- Return traffic
- Ephemeral ports

Security blocks traffic **silently**.

---

## Step 6: Test the Path

Use:
- curl
- nc
- telnet
- traceroute

Look for:
- Timeouts
- Connection refused
- Partial responses

Each symptom tells a story.

---

## Step 7: Check Load Balancers

If LB is involved:
- Are backends healthy?
- Is health check correct?
- Is protocol consistent?

LB issues cause **random failures**, not total outages.

---

## Step 8: Kubernetes-Specific Checks

If Kubernetes is involved:
- Service selectors
- Pod readiness
- Ingress routing
- Network policies

Pods being “Running” means nothing by itself.

---

## Step 9: Observe, Don’t Guess

Check:
- Logs
- Metrics
- Latency
- Error patterns

Numbers reveal truth faster than assumptions.

---

## Common Incident Patterns

Seen many times:

- Works in one AZ, fails in another
- Works by IP, fails by name
- Works internally, fails externally
- Fails only under load

These patterns guide your next check.

---

## What Not To Do During Incidents

Avoid:
- Random restarts
- Blind redeploys
- Changing multiple things at once

You’ll lose the signal.

---

## Mentor Incident Rule

One change at a time.
One hypothesis at a time.

Stability comes from discipline.

---

## Key Takeaway

Troubleshooting is not heroics.
It’s **structured thinking under pressure**.

If you follow a playbook:
- Incidents feel manageable
- Root causes become clear
- Trust in you increases

---

### End of Module 15
