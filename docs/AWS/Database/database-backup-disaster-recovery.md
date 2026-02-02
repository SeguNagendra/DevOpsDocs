---
sidebar_position: 9
title: Database Backup and Disaster Recovery
---

# Database Backup and Disaster Recovery

Databases store **critical business data**.
Failures are not a question of *if*, but *when*.

Database Backup and Disaster Recovery (DR) strategies ensure:
- Data is not lost
- Systems can recover quickly
- Business impact is minimized

---

## Why Backup and DR Matter

Without backups:
- Accidental deletes are permanent
- Corruption causes data loss
- Recovery is impossible

Without DR:
- Regional outages cause downtime
- Recovery takes too long
- SLA violations occur

👉 Backup protects **data**, DR protects **availability**.

---

## Backup vs Disaster Recovery (Clear Difference)

- **Backup** → Data protection
- **Disaster Recovery** → System recovery

Both are required for production systems.

---

## RDS Backup Strategy

### Automated Backups
- Enabled by default
- Daily snapshots + transaction logs
- Point-in-Time Recovery (PITR)

Retention:
- 1 to 35 days

---

### Manual Snapshots
- User-triggered
- Retained until deleted
- Used for long-term backups

Best practice:
- Combine automated + manual snapshots

---

## RDS Disaster Recovery

RDS DR options:
- Multi-AZ (same region HA)
- Cross-region read replicas
- Snapshot restore to another region

Choose based on:
- RTO (Recovery Time Objective)
- RPO (Recovery Point Objective)

---

## Aurora Backup and DR

Aurora provides:
- Continuous backups to S3
- PITR without performance impact

Aurora DR features:
- Multi-AZ by default
- Cross-region Aurora Global Database

Global Database:
- Low-latency global reads
- Fast regional failover

---

## DynamoDB Backup Strategy

### On-Demand Backups
- Full table backups
- Retained until deleted

### Point-in-Time Recovery (PITR)
- Restore to any second (last 35 days)

👉 PITR is strongly recommended.

---

## DynamoDB Disaster Recovery

DR options:
- Global Tables (multi-region active-active)
- Backup restore to another region

Global Tables provide:
- Regional resilience
- Near-zero RTO

---

## Backup Storage Considerations

- Backups are stored in S3 (managed by AWS)
- Encrypted by default
- Access controlled via IAM

Never:
- Rely on single backup method
- Ignore retention policies

---

## RTO and RPO (Must Know)

### RTO (Recovery Time Objective)
- How fast you need to recover

### RPO (Recovery Point Objective)
- How much data you can afford to lose

Lower RTO/RPO:
- Higher cost
- More complex architecture

---

## Choosing the Right DR Strategy

| Requirement | Recommended Strategy |
|-----------|---------------------|
| Basic protection | Automated backups |
| High availability | Multi-AZ |
| Cross-region DR | Replicas / Global DB |
| Near-zero downtime | Active-active design |

---

## Common Beginner Mistakes

- No PITR enabled
- Assuming Multi-AZ is backup
- No cross-region strategy
- Not testing restores

These mistakes cause:
- Data loss
- Long outages

---

## Testing Backups (Very Important)

Always:
- Perform restore tests
- Validate data integrity
- Practice DR drills

Backups without testing are **false confidence**.

---

## Interview Tip

If asked:
> “How do you protect databases in AWS?”

Strong answer:
> By enabling automated backups and PITR, using Multi-AZ for availability, and designing cross-region DR strategies based on RTO and RPO.

---

## Key Takeaways

- Backups protect data
- DR protects availability
- RTO and RPO guide design
- AWS provides managed backup tools
- Testing is mandatory

---

📌 **Next:** Database Summary and Comparison
