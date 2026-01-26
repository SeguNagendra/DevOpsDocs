---
sidebar_position: 6
---

# Timeouts & Retries

Timeouts and retries are essential for **resilient Jenkins pipelines**.
They protect Jenkins from hanging builds and reduce failures caused by flaky steps.

---

## Why Timeouts Are Mandatory

Without timeouts:
- Pipelines can hang forever
- Executors remain blocked
- Jenkins queues back up
- Manual intervention is required

> Every production pipeline must have timeouts.

---

## Timeout at Pipeline Level

Apply a global timeout using `options`:

```groovy
pipeline {
  agent any
  options {
    timeout(time: 45, unit: 'MINUTES')
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
  }
}
```

### When to Use
- Small pipelines
- Predictable execution time

---

## Timeout at Stage Level (Preferred)

Stage-level timeouts give finer control:

```groovy
stage('Regression Tests') {
  options {
    timeout(time: 20, unit: 'MINUTES')
  }
  steps {
    sh 'run-regression.sh'
  }
}
```

### Why Preferred
- Different stages need different limits
- Prevents over-restricting short stages

---

## Timeout with `timeout {}` Step

```groovy
timeout(time: 5, unit: 'MINUTES') {
  sh 'long-running-task.sh'
}
```

Useful for:
- Individual commands
- Scripted logic

---

## Retry Step

The `retry` step reruns a block if it fails.

```groovy
retry(3) {
  sh 'run-flaky-tests.sh'
}
```

---

## Retry + Timeout Combined

```groovy
retry(2) {
  timeout(time: 10, unit: 'MINUTES') {
    sh 'api-tests.sh'
  }
}
```

This handles:
- Temporary failures
- Network glitches
- Intermittent test issues

---

## What Should Be Retried?

Safe to retry:
- API tests
- Network calls
- UI tests (carefully)

Do NOT retry:
- Deployments
- Data migrations
- Destructive operations

---

## Common Mistakes

- Retrying entire pipelines blindly
- No timeout inside retry
- Retrying non-idempotent steps
- Very high retry counts

---

## Best Practices

- Always combine retry with timeout
- Retry only flaky-safe steps
- Keep retry count low (1–3)
- Log retry attempts

---

## Interview Traps

- **Difference between pipeline vs stage timeout?**  
  → Scope

- **Can retry hide real failures?**  
  → Yes, if overused

- **Should PROD deploys be retried?**  
  → No