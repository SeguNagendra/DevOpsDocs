---
sidebar_position: 4
---

# Writing Groovy Classes with `src/`

The `src/` directory is used for **structured, reusable Groovy code** inside Jenkins Shared Libraries.
This is where **complex logic belongs**, not in Jenkinsfiles or `vars/`.

---

## Purpose of `src/`

Use `src/` for:
- Complex business logic
- Utilities and helpers
- Validation logic
- Reusable services

Avoid:
- Defining pipeline stages directly
- Long shell scripts

---

## Mandatory Package Structure

All classes in `src/` **must** use a package name.

Example structure:
```
src/
└── com/company/ci/
    └── PipelineUtils.groovy
```

Package declaration:
```groovy
package com.company.ci
```

Without a package, Jenkins will fail to load the class.

---

## Example Utility Class

```groovy
package com.company.ci

class PipelineUtils {

  def validateEnv(String env) {
    if (!['dev','qa','prod'].contains(env)) {
      throw new IllegalArgumentException("Invalid env: ${env}")
    }
  }

  def notifyTeam(String msg) {
    println "NOTIFY: ${msg}"
  }
}
```

---

## Using `src` Classes from `vars`

```groovy
def call(Map cfg = [:]) {
  def utils = new com.company.ci.PipelineUtils()
  utils.validateEnv(cfg.env)
  echo "Environment validated"
}
```

This keeps:
- `vars` → orchestration
- `src` → logic

---

## Accessing Pipeline Steps

Important rule:
- `src` classes **do not automatically have access** to pipeline steps

Correct pattern:
```groovy
class PipelineUtils {
  def steps

  PipelineUtils(steps) {
    this.steps = steps
  }

  def runCmd(String cmd) {
    steps.sh cmd
  }
}
```

Usage:
```groovy
def utils = new com.company.ci.PipelineUtils(this)
utils.runCmd('ls -la')
```

---

## Error Handling in `src`

- Throw exceptions for invalid states
- Let Jenkins handle failures
- Avoid swallowing errors

```groovy
throw new RuntimeException("Validation failed")
```

---

## Common Mistakes

- No package declaration
- Putting pipeline stages in `src`
- Trying to call `sh` directly without steps
- Overengineering small logic

---

## Best Practices

- Keep `src` classes pure and testable
- Pass `steps` explicitly when needed
- Keep Jenkinsfile and `vars` thin
- Use meaningful package names

---

## Interview Focus Areas

- Why `src` needs package names
- Difference between `vars` and `src`
- How pipeline steps are accessed safely

