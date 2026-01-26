---
sidebar_position: 2
---

# when Conditions

The `when` directive allows Jenkins pipelines to **run stages conditionally**.
This is one of the most used and most misused pipeline features.

---

## What Is the `when` Directive?

The `when` directive controls **whether a stage executes or is skipped**.

It is evaluated:
- Before the stage starts
- On the controller
- Based on pipeline context

---

## Basic Syntax

```groovy
stage('Deploy') {
  when {
    branch 'main'
  }
  steps {
    sh 'deploy.sh'
  }
}
```

---

## Common `when` Conditions

### Branch Condition

```groovy
when {
  branch 'main'
}
```

Runs only on the specified branch.

---

### Expression Condition

```groovy
when {
  expression {
    return params.RUN_DEPLOY == true
  }
}
```

Allows custom Groovy logic.

---

### Environment Condition

```groovy
when {
  environment name: 'ENV', value: 'prod'
}
```

---

### Not Condition

```groovy
when {
  not {
    branch 'develop'
  }
}
```

---

### Any / All Conditions

```groovy
when {
  anyOf {
    branch 'main'
    branch 'release'
  }
}
```

```groovy
when {
  allOf {
    branch 'main'
    expression { params.DEPLOY == true }
  }
}
```

---

## `beforeAgent` Option

```groovy
when {
  beforeAgent true
  branch 'main'
}
```

- Prevents agent allocation if condition fails
- Saves resources

> Strongly recommended for expensive agents.

---

## Common Mistakes

- Putting `when` inside `steps`
- Using complex Groovy logic inline
- Forgetting `beforeAgent`
- Hardcoding branch names

---

## Best Practices

- Keep conditions simple
- Prefer parameters over hardcoding
- Use `beforeAgent true` when possible
- Move complex logic to shared libraries

---

## Interview Traps

- **When is `when` evaluated?**  
  → Before stage execution

- **Does `when` consume an agent?**  
  → Only if `beforeAgent` is false

- **Can `when` skip stages?**  
  → Yes