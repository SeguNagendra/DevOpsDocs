---
sidebar_position: 3
---

# Webhooks & Build Triggers

Webhooks are the **preferred and most efficient way** to trigger Jenkins builds from SCM.
They enable fast, event-driven CI instead of slow polling.

---

## What Is a Webhook?

A webhook is an HTTP callback sent by the SCM system to Jenkins when an event occurs.

Common events:
- Code push
- Pull request creation/update
- Merge events

Jenkins reacts immediately to these events.

---

## Why Webhooks Are Recommended

Compared to polling, webhooks:
- Trigger builds instantly
- Reduce load on Jenkins
- Scale better with many repositories
- Provide accurate event context

---

## Polling vs Webhooks

| Aspect | Polling | Webhooks |
|------|--------|----------|
| Trigger type | Time-based | Event-based |
| Load on Jenkins | High | Low |
| Latency | Slow | Near-instant |
| Scalability | Poor | Excellent |
| Recommended | ❌ | ✅ |

---

## Jenkins Webhook Endpoint

Typical webhook URL:
```
https://<jenkins-url>/github-webhook/
```

> The exact endpoint may vary by SCM and plugin.

---

## Webhook Setup (High-Level)

### In SCM (GitHub/GitLab)
- Add Jenkins webhook URL
- Select relevant events (push, PR)
- Configure secret/token (if supported)

### In Jenkins
- Ensure SCM plugin is installed
- Enable webhook trigger in job or multibranch config
- Verify Jenkins URL is reachable

---

## Multibranch Pipeline Behavior

- Webhooks trigger **branch indexing**
- Jenkins discovers new branches/PRs
- Pipelines are created/updated automatically

---

## Securing Webhooks

- Use webhook secrets/tokens
- Restrict webhook source IPs (if possible)
- Use HTTPS only
- Avoid exposing Jenkins publicly without auth

---

## Common Webhook Issues

- Jenkins URL misconfigured
- Firewall blocking inbound traffic
- Wrong webhook endpoint
- Missing permissions
- Webhook secret mismatch

---

## Debugging Webhooks

Check:
- SCM webhook delivery logs
- Jenkins system logs
- Multibranch scan logs
- Jenkins URL configuration

---

## Common Mistakes

- Using polling and webhooks together unnecessarily
- Forgetting to enable triggers in Jenkins
- Not validating webhook delivery
- Exposing Jenkins without protection

---

## Interview Focus Areas

- Polling vs webhooks differences
- How multibranch pipelines react to webhooks
- Webhook security considerations

