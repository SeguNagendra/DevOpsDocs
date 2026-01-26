---
sidebar_position: 6
---

# Environment & Tools

This document explains how Jenkins pipelines manage **environment variables** and **tools**.
Correct usage is essential for **portable, repeatable, and secure pipelines**.

---

## Environment Variables in Jenkins

Environment variables allow you to:
- Parameterize pipelines
- Avoid hardcoding values
- Share data between steps

---

## `environment {}` Block

The `environment` block defines variables available to:
- All stages (global)
- Or a specific stage

### Global Environment
```groovy
pipeline {
  agent any
  environment {
    ENV = 'qa'
    APP_NAME = 'billing-service'
  }
}
```

---

### Stage-Level Environment
```groovy
stage('Deploy') {
  environment {
    ENV = 'prod'
  }
  steps {
    sh 'deploy.sh'
  }
}
```

Stage-level variables override global ones.

---

## Accessing Environment Variables

Inside steps:
```groovy
sh 'echo $ENV'
```

In Groovy:
```groovy
echo env.ENV
```

---

## Built-in Jenkins Environment Variables

Common examples:
- `BUILD_NUMBER`
- `BUILD_ID`
- `JOB_NAME`
- `BRANCH_NAME`
- `WORKSPACE`

These are automatically available.

---

## `withEnv` Usage

Temporary environment variables:

```groovy
withEnv(['JAVA_HOME=/opt/java17']) {
  sh 'java -version'
}
```

Scope is limited to the block.

---

## Tools in Jenkins

The `tools` directive ensures required tools are available.

Common tools:
- JDK
- Maven
- NodeJS
- Gradle

---

## `tools {}` Block

```groovy
pipeline {
  agent any
  tools {
    maven 'maven-3.9'
    jdk 'jdk-17'
  }
}
```

Tools must be defined in **Global Tool Configuration**.

---

## Tool Auto-Installation vs Preinstalled

### Auto-Installation
- Jenkins downloads tools automatically
- Convenient for learning

### Preinstalled Tools
- Tools installed on agents manually
- Preferred in production

---

## Common Mistakes

- Hardcoding paths
- Overusing environment variables
- Mixing secrets with env vars
- Forgetting tool configuration

---

## Best Practices

- Use environment variables for configuration
- Use credentials for secrets
- Keep environment blocks small
- Prefer preinstalled tools in production

---

## Interview Traps

- **Are env vars global by default?**  
  → Only within defined scope

- **Should secrets be in environment block?**  
  → No

- **Do tools install automatically?**  
  → Only if configured