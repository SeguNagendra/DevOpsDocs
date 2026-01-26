---
sidebar_position: 7
---

# Controller Performance Tuning

Controller performance tuning focuses on **keeping Jenkins responsive, stable, and predictable**
as usage grows. Most performance problems come from misconfiguration, not scale.

---

## Why Controller Performance Degrades

Common causes:
- Too many plugins
- Controller running builds
- High executor count
- Excessive logging
- Large job counts without folder structure

Performance issues accumulate slowly.

---

## Controller Responsibilities (Reminder)

Controller should handle:
- Scheduling
- Metadata
- UI
- Configuration
- Security

Controller should **not** execute builds.

---

## CPU & Memory Tuning

Guidelines:
- Allocate sufficient heap memory
- Avoid over-allocating heap
- Monitor GC pauses
- Tune JVM options carefully

Bad JVM tuning causes UI freezes.

---

## JVM Heap Sizing

General guidance:
- Small Jenkins: 4–8 GB heap
- Medium Jenkins: 8–16 GB heap
- Large Jenkins: 16–32 GB heap

Always observe real usage.

---

## Disk I/O Considerations

- Use fast storage for `JENKINS_HOME`
- Avoid network filesystems with high latency
- Monitor disk space and IOPS

Disk bottlenecks cause slow page loads.

---

## Plugin Impact on Performance

- Each plugin adds memory overhead
- Some plugins add background jobs
- Remove unused plugins aggressively

Plugin count directly affects startup time.

---

## Job & Folder Organization

Best practices:
- Use folders to group jobs
- Avoid flat job structures
- Archive old jobs

Large job counts slow Jenkins.

---

## Log Management

- Reduce log verbosity
- Rotate logs
- Avoid debug logging in production

Logs can exhaust disk and CPU.

---

## Monitoring Performance

Track:
- Controller CPU usage
- JVM heap and GC
- Thread counts
- Response time
- Queue length

Tune based on data.

---

## Common Performance Anti-Patterns

- Running builds on controller
- Excessive executors
- Massive Jenkinsfiles
- No cleanup policies

---

## Best Practices

- Controller executors = 0
- Minimal plugins
- Fast storage
- Monitor continuously
- Scale horizontally via agents

---

## Interview Focus Areas

- Why controller becomes slow
- Heap vs OS memory
- Plugin impact on performance

