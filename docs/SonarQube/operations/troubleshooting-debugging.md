---
sidebar_position: 19
---

# Troubleshooting & Debugging – Fixing Real SonarQube Issues

No matter how well SonarQube is set up, issues will happen.
What matters is **how quickly and confidently** you can diagnose and fix them.

This chapter teaches a **problem-solving mindset**, not just a list of errors.

---

## How to Think When Something Breaks

When SonarQube behaves unexpectedly:
- Do not panic
- Do not randomly change settings
- Start with understanding **where the failure happened**

Most issues fall into one of these areas:
- Scanner
- Server
- Database
- Elasticsearch
- CI/CD integration

---

## Common Scanner Failures

Typical scanner-related problems:
- Authentication failures
- Wrong project key
- Unsupported language version
- Missing permissions

First step:
- Check scanner logs
- Enable debug mode if needed

Scanner issues are usually configuration-related.

---

## Quality Gate Not Triggering

Common causes:
- CI pipeline not waiting for gate result
- Missing webhook configuration
- Incorrect branch type

Checklist:
- Verify webhook connectivity
- Ensure pipeline waits for Quality Gate
- Confirm branch/PR configuration

---

## Coverage Missing or Incorrect

Common reasons:
- Tests not executed before scan
- Coverage reports not generated
- Wrong report paths configured

SonarQube does not run tests — it only reads reports.

---

## UI Slow or Unresponsive

Possible causes:
- Elasticsearch memory pressure
- Disk I/O bottlenecks
- Overloaded server

Check:
- Elasticsearch health
- System resources
- Disk space

Most UI issues are infrastructure-related.

---

## Analysis Succeeds but Results Look Wrong

Possible reasons:
- Wrong project key
- Incorrect baseline configuration
- Old cache or index issues

Steps:
- Verify project configuration
- Review baseline settings
- Consider reindexing if needed

---

## Logs You Should Always Check

Important log locations:
- Scanner logs
- SonarQube server logs
- Elasticsearch logs

Logs usually explain the problem clearly if you read them carefully.

---

## Common Troubleshooting Mistakes

Avoid these patterns:
- Restarting services blindly
- Editing the database
- Ignoring logs
- Making multiple changes at once

These actions often make problems worse.

---

## Key Takeaway

Effective troubleshooting is about **systematic thinking**, not memorizing errors.

With a clear mental model:
- Issues are easier to isolate
- Fixes become predictable
- Confidence grows with experience

---

➡️ **Next:** Logs, Backup & Upgrades  
