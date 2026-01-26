---
sidebar_position: 2
---

# Declarative vs Scripted Pipeline

Jenkins supports two pipeline syntaxes: **Declarative** and **Scripted**.
Understanding the difference is essential for **correct design decisions** and **interviews**.

---

## High-Level Comparison

| Aspect | Declarative Pipeline | Scripted Pipeline |
|------|---------------------|------------------|
| Syntax | Structured | Groovy-based |
| Readability | High | Medium–Low |
| Flexibility | Limited | Very High |
| Safety | Built-in safeguards | No safeguards |
| Recommended | ✅ Yes | ⚠️ Only when needed |

---

## Declarative Pipeline

### What It Is
Declarative Pipeline provides a **structured, opinionated syntax** that enforces best practices.

### Characteristics
- Uses predefined blocks
- Easier to read and maintain
- Built-in validation
- Safer for teams

### Example
```groovy
pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
  }
}
```

---

## Scripted Pipeline

### What It Is
Scripted Pipeline is written using **Groovy** and provides full control over pipeline logic.

### Characteristics
- Very flexible
- Powerful conditional logic
- Harder to read
- Easier to misuse

### Example
```groovy
node {
  stage('Test') {
    sh 'mvn test'
  }
}
```

---

## When to Use Declarative Pipeline

Use Declarative when:
- You are building standard CI/CD pipelines
- Team size is medium to large
- Readability and maintainability matter
- You want safer defaults

> This covers **90% of real-world use cases**.

---

## When Scripted Pipeline Is Justified

Scripted pipeline is justified when:
- Complex dynamic logic is required
- Advanced loops or conditions are needed
- Declarative syntax becomes limiting

> Even then, prefer **shared libraries**.

---

## Mixing Declarative and Scripted

Declarative pipelines can include scripted blocks:

```groovy
script {
  if (env.BRANCH_NAME == 'main') {
    sh 'deploy.sh'
  }
}
```

This provides flexibility without losing structure.

---

## Common Mistakes

- Starting directly with scripted pipeline
- Writing unreadable Groovy logic
- Ignoring shared libraries
- Overengineering pipelines

---

## Interview Traps

- **Which pipeline type is recommended?**  
  → Declarative

- **Can scripted logic be used in declarative?**  
  → Yes, using `script {}`

- **Is scripted pipeline deprecated?**  
  → No, but discouraged for most use cases
