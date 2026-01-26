---
sidebar_position: 6
---

# Polling & Scan Schedules

This document explains **how Jenkins polls SCM and schedules multibranch scans**, and when (or if) you should use them.
Misuse of polling is a common cause of **controller overload**.

---

## What Is SCM Polling?

SCM polling means Jenkins periodically checks the repository for changes.

- Time-based (cron-like)
- Jenkins-initiated
- No event context (compared to webhooks)

Polling is a **fallback**, not the default choice.

---

## What Is Multibranch Scan Scheduling?

Scan scheduling controls **how often Jenkins re-indexes repositories** to discover:
- New branches
- Deleted branches
- New PRs

This is different from triggering a build.

---

## Polling vs Webhooks (Reinforced)

| Aspect | Polling | Webhooks |
|------|--------|----------|
| Initiator | Jenkins | SCM |
| Frequency | Scheduled | Event-driven |
| Load | High | Low |
| Context | Minimal | Rich |
| Recommendation | Fallback | Primary |

---

## Polling Syntax (If You Must)

```groovy
pipeline {
  triggers {
    pollSCM('H/5 * * * *')
  }
}
```

Use only when:
- Webhooks are impossible
- Repo is small
- Change rate is low

---

## Multibranch Scan Triggers

Common scan triggers:
- Webhook-based indexing (preferred)
- Periodic scan (cron)
- Manual scan

Webhook-based indexing should always be enabled when possible.

---

## Scan Frequency Guidelines

- Small repos: infrequent scans
- Large repos: webhook-only
- Avoid aggressive cron schedules

> Frequent scans = controller CPU + API quota consumption

---

## Common Misconfigurations

- Polling + webhooks together
- Very frequent polling (every minute)
- Scanning huge orgs too often
- Confusing scan with build trigger

---

## Performance & Scale Tips

- Prefer webhook indexing
- Disable polling when webhooks work
- Reduce scan frequency for large orgs
- Filter branches before scanning

---

## Troubleshooting

Check:
- Jenkins trigger configuration
- Multibranch scan logs
- SCM API rate limits
- Controller CPU usage

---

## Interview Focus Areas

- Polling vs webhook trade-offs
- Difference between scan and build trigger
- Why polling does not scale

