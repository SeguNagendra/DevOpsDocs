---
sidebar_position: 3
title: S3 Versioning and Lifecycle Rules
---

# S3 Versioning and Lifecycle Rules

Amazon S3 is often used to store **critical data**:
- Backups
- Logs
- Application assets
- Compliance records

Because of this, AWS provides **Versioning** and **Lifecycle Rules** to:
- Protect data from accidental deletion
- Automatically manage data over time
- Optimize storage cost without manual effort

---

## Why Versioning and Lifecycle Matter

Real-world problems:
- Someone deletes a file by mistake
- An application overwrites important data
- Old data keeps increasing storage cost

S3 Versioning and Lifecycle Rules exist to **solve these problems safely**.

---

## 🔁 S3 Versioning

### What Is Versioning?
S3 Versioning keeps **multiple versions of the same object** in a bucket.

Instead of replacing or deleting data:
- S3 stores a new version
- Older versions remain accessible

Think of it as:
> **Git for objects in S3 (very simplified)**

---

## How Versioning Works

- Every object gets a version ID
- Deleting an object creates a *delete marker*
- Older versions are still retrievable

👉 Data is never truly lost unless you delete all versions.

---

## Why Enable Versioning

Versioning protects against:
- Accidental deletion
- Application bugs
- Ransomware attacks

This makes versioning **critical for production buckets**.

---

## Things to Be Careful About

- Versioning increases storage usage
- Old versions still cost money
- You must manage versions properly

👉 Versioning **protects data**, but must be paired with lifecycle rules.

---

## ♻️ S3 Lifecycle Rules

### What Are Lifecycle Rules?
Lifecycle rules define **what happens to objects over time**.

They allow you to:
- Move objects between storage classes
- Expire (delete) old objects automatically

Lifecycle rules are **automation for storage management**.

---

## Common Lifecycle Actions

### 1. Transition Actions
Move data between classes:
- Standard → IA
- IA → Glacier
- Glacier → Deep Archive

### 2. Expiration Actions
Delete data:
- After X days
- After compliance period

---

## Real-World Lifecycle Example

Typical log bucket:
- Days 0–30 → S3 Standard
- Days 31–90 → S3 IA
- After 90 days → Glacier
- After 1 year → Delete

This setup:
- Protects recent data
- Reduces long-term cost automatically

---

## Versioning + Lifecycle Together (Best Practice)

Best practice:
- Enable versioning for protection
- Use lifecycle rules to:
  - Expire old versions
  - Control storage cost

👉 Using one without the other is **incomplete**.

---

## Common Mistakes

- Enabling versioning but never cleaning old versions
- No lifecycle rules on large buckets
- Deleting buckets without understanding versioned objects

These mistakes cause:
- High AWS bills
- Unexpected deletion failures

---

## Interview Tip

If asked:
> “How do you protect data in S3?”

Strong answer:
> By enabling versioning to prevent accidental deletion and using lifecycle rules to manage cost and retention.

This answer shows **real production experience**.

---

## Key Takeaways

- Versioning protects data integrity
- Lifecycle rules automate storage management
- Both are essential for production S3 usage
- Cost optimization and data safety go together
- Critical for backups and compliance

---

📌 **Next:** S3 Encryption
