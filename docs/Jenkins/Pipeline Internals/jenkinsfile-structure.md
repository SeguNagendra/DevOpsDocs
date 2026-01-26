---
sidebar_position: 3
---

# Jenkinsfile Structure

This document explains the **mandatory and optional sections of a Jenkinsfile** and how Jenkins executes them.
A clean structure is critical for **readability, reliability, and scalability**.

---

## What Is a Jenkinsfile?

A Jenkinsfile is a text file that defines a Jenkins Pipeline using code.
It is stored in **source control** and executed by Jenkins.

---

## Basic Jenkinsfile Skeleton

```groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'echo Building'
      }
    }
  }
}
```

This is the **minimum valid declarative Jenkinsfile**.

---

## Mandatory Sections

### 1. `pipeline`
- Root block of the Jenkinsfile
- All pipeline logic lives inside this block

---

### 2. `agent`
- Defines **where** the pipeline runs
- Can be global or stage-level

Examples:
```groovy
agent any
```
```groovy
agent { label 'linux' }
```

---

### 3. `stages`
- Groups all stages
- Executes stages in defined order

---

### 4. `stage`
- Represents a logical phase
- Improves visibility and debugging

Example:
```groovy
stage('Test') {
  steps {
    sh 'mvn test'
  }
}
```

---

### 5. `steps`
- Actual commands executed
- Runs inside a stage

---

## Optional but Important Sections

### `environment`
- Defines environment variables

```groovy
environment {
  ENV = 'qa'
}
```

---

### `tools`
- Declares tools required by pipeline

```groovy
tools {
  maven 'maven-3.9'
}
```

---

### `options`
- Controls pipeline behavior

Common options:
- `timeout`
- `retry`
- `disableConcurrentBuilds`

---

### `post`
- Runs after pipeline or stage completion
- Used for cleanup and notifications

```groovy
post {
  always {
    echo 'Pipeline finished'
  }
}
```

---

### `when`
- Conditional stage execution

```groovy
when {
  branch 'main'
}
```

---

## Execution Order (Important)

1. `agent`
2. `environment`
3. `tools`
4. `stages`
5. `post`

Understanding this order prevents surprises.

---

## Global vs Stage-Level Sections

Some sections can be declared at:
- Pipeline level
- Stage level

Example:
```groovy
stage('Test') {
  agent { label 'linux' }
}
```

---

## Common Structure Mistakes

- Very large stages
- Too many steps in one stage
- Hardcoded values
- Missing post cleanup

---

## Best Practices

- Keep stages small and meaningful
- One responsibility per stage
- Use shared libraries for reuse
- Avoid deep nesting

---

## Interview Traps

- **Is agent mandatory?**  
  → Yes

- **Can stages run without steps?**  
  → No

- **Does post run on failure?**  
  → Yes (depending on condition)