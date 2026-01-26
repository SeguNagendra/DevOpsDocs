---
sidebar_position: 4
---

# Stages vs Steps

Understanding the difference between **stages** and **steps** is critical for
pipeline design, debugging, visualization, and interviews.

---

## What Is a Stage?

A **stage** represents a **logical phase** in the pipeline.

Examples:
- Checkout
- Build
- Test
- Deploy

Stages:
- Improve readability
- Appear clearly in Jenkins UI
- Help identify where failures occur

---

## What Is a Step?

A **step** is an **actual executable action** inside a stage.

Examples:
- `sh`
- `bat`
- `checkout`
- `echo`
- `script`

Steps:
- Perform real work
- Run commands on agents
- Execute sequentially inside a stage

---

## Structural Relationship

- A pipeline contains **stages**
- A stage contains **steps**
- Steps cannot exist outside a stage

```groovy
stage('Test') {
  steps {
    sh 'mvn test'
  }
}
```

---

## Execution Behavior

### Stage Execution
- Stages run sequentially by default
- Can be run in parallel using `parallel`
- Failure in a stage fails the pipeline (unless handled)

### Step Execution
- Steps run sequentially inside a stage
- Failure of a step fails the stage

---

## Why Jenkins UI Cares About Stages

- Jenkins visualizes pipelines **by stage**
- Restart-from-stage works at stage level
- Stage timing and logs are tracked

> Steps are not first-class UI elements.

---

## Common Anti-Patterns

- One giant stage with many steps
- Meaningless stage names (`stage('Step1')`)
- Business logic inside steps instead of libraries

---

## Best Practices

- One logical responsibility per stage
- Keep steps short and focused
- Use stages to represent CI/CD phases
- Move reusable logic to shared libraries

---

## Interview Traps

- **Can steps exist without stages?**  
  → No

- **What does Jenkins visualize?**  
  → Stages

- **Does restart work at step level?**  
  → No
