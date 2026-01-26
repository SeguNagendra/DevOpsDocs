---
sidebar_position: 3
---

# Build Parameters

Build parameters make Jenkins pipelines **dynamic and reusable**.
They allow users and systems to control pipeline behavior at runtime.

---

## What Are Build Parameters?

Build parameters are inputs provided when triggering a pipeline.
They can influence:
- Which stages run
- Which environment is targeted
- What actions are performed

Without parameters, pipelines are static.

---

## Where Parameters Are Defined

Parameters are defined at the **pipeline level**:

```groovy
pipeline {
  agent any
  parameters {
    booleanParam(name: 'RUN_TESTS', defaultValue: true)
  }
}
```

---

## Common Parameter Types

### String Parameter

```groovy
string(name: 'ENV', defaultValue: 'qa', description: 'Target environment')
```

---

### Boolean Parameter

```groovy
booleanParam(name: 'DEPLOY', defaultValue: false)
```

---

### Choice Parameter

```groovy
choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'])
```

---

## Accessing Parameters

Inside pipeline logic:

```groovy
if (params.DEPLOY) {
  sh 'deploy.sh'
}
```

Parameters are accessed using the `params` object.

---

## Parameters with `when`

Parameters are often combined with `when`:

```groovy
stage('Deploy') {
  when {
    expression { params.DEPLOY == true }
  }
  steps {
    sh 'deploy.sh'
  }
}
```

---

## Default Values Matter

- Always define default values
- Prevents accidental behavior
- Improves usability

---

## Common Mistakes

- Forgetting default values
- Hardcoding parameter logic
- Too many parameters
- Mixing secrets with parameters

---

## Best Practices

- Use parameters sparingly
- Name parameters clearly
- Combine parameters with `when`
- Never pass secrets as parameters

---

## Interview Traps

- **How do you access parameters?**  
  → Using `params.<NAME>`

- **Can parameters control stage execution?**  
  → Yes

- **Are parameters evaluated at runtime?**  
  → Yes