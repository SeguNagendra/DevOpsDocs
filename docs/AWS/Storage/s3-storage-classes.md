---
sidebar_position: 2
title: S3 Storage Classes
---

# S3 Storage Classes

Amazon S3 offers multiple **storage classes** so you can store data at the **right cost** based on how often it is accessed.

A common beginner mistake is:
> Putting all data into S3 Standard and never optimizing cost.

Understanding storage classes helps you:
- Reduce storage costs significantly
- Design efficient data lifecycles
- Answer cost-optimization interview questions confidently

---

## Why S3 Has Storage Classes

Not all data is accessed equally:
- Some data is accessed frequently
- Some data is rarely accessed
- Some data is kept only for compliance

S3 storage classes exist to:
- Match cost with access patterns
- Avoid paying for unnecessary performance

---

## Main S3 Storage Classes (You Must Know)

AWS provides several S3 storage classes.  
These are the **most commonly used ones**:

1. S3 Standard  
2. S3 Intelligent-Tiering  
3. S3 Standard-Infrequent Access (IA)  
4. S3 One Zone-IA  
5. S3 Glacier (Flexible Retrieval)  
6. S3 Glacier Deep Archive  

---

## 🟢 S3 Standard

### Best for
- Frequently accessed data
- Active applications
- Static website content

### Characteristics
- High availability
- Low latency
- Higher cost than other classes

👉 Default choice for most workloads.

---

## 🧠 S3 Intelligent-Tiering

### Best for
- Unknown or changing access patterns

### Characteristics
- Automatically moves data between tiers
- Small monitoring cost
- No retrieval fee for frequent tiers

👉 Great when you **don’t know access patterns in advance**.

---

## 🟡 S3 Standard-Infrequent Access (IA)

### Best for
- Data accessed less often
- Backups
- Disaster recovery data

### Characteristics
- Lower storage cost
- Retrieval fee applies
- Same durability as Standard

👉 Use when access is **predictable but rare**.

---

## 🔵 S3 One Zone-IA

### Best for
- Non-critical, reproducible data

### Characteristics
- Stored in a single AZ
- Cheaper than Standard-IA
- Lower availability

⚠️ Not suitable for critical data.

---

## ❄️ S3 Glacier (Flexible Retrieval)

### Best for
- Long-term archival
- Compliance data

### Characteristics
- Very low storage cost
- Retrieval takes minutes to hours

👉 Ideal for archives you rarely need.

---

## 🧊 S3 Glacier Deep Archive

### Best for
- Long-term compliance (years)

### Characteristics
- Lowest cost
- Retrieval takes hours

👉 Cheapest option for data you almost never access.

---

## Quick Comparison

| Storage Class | Access Frequency | Cost | Retrieval Time |
|-------------|-----------------|------|---------------|
| Standard | Frequent | High | Immediate |
| Intelligent-Tiering | Unknown | Medium | Immediate |
| Standard-IA | Infrequent | Low | Immediate |
| One Zone-IA | Infrequent | Very Low | Immediate |
| Glacier | Rare | Very Low | Minutes–Hours |
| Deep Archive | Very Rare | Lowest | Hours |

---

## Lifecycle Policies (Very Important)

Lifecycle rules allow you to:
- Automatically move objects between storage classes
- Delete objects after a period

Example:
- S3 Standard → IA after 30 days
- IA → Glacier after 90 days

👉 Lifecycle rules = **automatic cost optimization**.

---

## Common Mistakes

- Using Glacier for frequently accessed data
- Forgetting retrieval costs
- Not using lifecycle policies
- Using One Zone-IA for critical data

These mistakes **increase cost or risk data loss**.

---

## Interview Tip

If asked:
> “How do you reduce S3 storage cost?”

Strong answer:
> By choosing the correct S3 storage class and using lifecycle policies to move data automatically.

That answer shows **practical AWS knowledge**.

---

## Key Takeaways

- Different data = different storage class
- Intelligent-Tiering removes guesswork
- Glacier is for archives, not active data
- Lifecycle rules are essential
- Cost optimization starts at storage design

---

📌 **Next:** S3 Versioning and Lifecycle Rules
