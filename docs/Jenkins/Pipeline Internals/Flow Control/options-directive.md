---
sidebar_position: 5
---

# Options Directive

The `options` directive controls **pipeline-level behavior**.
It is critical for **stability, safety, and long-running pipelines**.

---

## What Is the `options` Directive?

The `options` block allows you to configure how a pipeline behaves, such as:
- Concurrency rules
- Build retention
- Timeouts
- Logging behavior

Options apply to the **entire pipeline** unless overridden.

---

## Basic Syntax

```groovy
pipeline {
  agent any
  options {
    timestamps()
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

---

## Commonly Used Options

### `disableConcurrentBuilds()`

Prevents multiple builds of the same job from running at the same time.

```groovy
options {
  disableConcurrentBuilds()
}
```

**Use case:**
- Shared environments
- Database tests
- Non-idempotent jobs

---

### `buildDiscarder()`

Controls how many old builds are kept.

```groovy
options {
  buildDiscarder(logRotator(numToKeepStr: '20'))
}
```

**Why it matters:**
- Prevents disk exhaustion
- Keeps Jenkins clean

---

### `timeout()`

Applies a global timeout to the pipeline.

```groovy
options {
  timeout(time: 30, unit: 'MINUTES')
}
```

> Prefer stage-level timeouts for long pipelines.

---

### `timestamps()`

Adds timestamps to console logs.

```groovy
options {
  timestamps()
}
```

Very useful for:
- Debugging delays
- Performance analysis

---

### `skipDefaultCheckout()`

Prevents automatic SCM checkout.

```groovy
options {
  skipDefaultCheckout()
}
```

Use when:
- You manage checkout manually
- Multiple repos are involved

---

## Global vs Stage-Level Options

- Most options are pipeline-level
- Some behaviors (like timeout) can be applied per stage

Example:
```groovy
stage('Test') {
  options {
    timeout(time: 10, unit: 'MINUTES')
  }
  steps {
    sh 'run-tests.sh'
  }
}
```

---

## Common Mistakes

- No build discarder configured
- No timeouts (pipelines hang forever)
- Allowing concurrent builds accidentally
- Overusing global timeout

---

## Best Practices

- Always configure build discarder
- Use timeouts everywhere (pipeline or stage)
- Disable concurrent builds for shared resources
- Enable timestamps by default

---

## Interview Traps

- **Where are options applied?**  
  → Pipeline level (unless stage-specific)

- **Should every pipeline have options?**  
  → Yes

- **What prevents disk space issues?**  
  → buildDiscarder