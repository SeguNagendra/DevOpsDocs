---
sidebar_position: 3
---

# Writing Reusable Steps with `vars/`

The `vars/` directory is used to define **global, reusable pipeline steps**.
These steps are callable directly from a Jenkinsfile and are the most common entry point for shared libraries.

---

## What Goes into `vars/`

Use `vars/` for:
- High-level pipeline steps
- Reusable stages or stage groups
- Thin orchestration logic

Avoid:
- Heavy business logic
- Complex class hierarchies

---

## Naming Rules

- Filename = step name
- Must be a valid Groovy identifier
- Case-sensitive

Example:
```
vars/
└── buildAndTest.groovy
```

Callable as:
```groovy
buildAndTest()
```

---

## Mandatory `call()` Method

Each `vars` file **must** implement a `call()` method.

```groovy
def call() {
  stage('Build') {
    sh 'mvn clean package'
  }
}
```

Without `call()`, Jenkins cannot invoke the step.

---

## Accepting Parameters

Reusable steps can accept parameters like normal Groovy methods.

```groovy
def call(Map config = [:]) {
  def envName = config.get('env', 'qa')
  echo "Running for ${envName}"
}
```

Usage:
```groovy
buildAndTest(env: 'prod')
```

---

## Using Pipeline Steps Inside `vars`

Pipeline steps (`sh`, `echo`, `stage`, etc.) are available automatically.

```groovy
def call() {
  sh 'echo Running inside shared lib'
}
```

No imports required.

---

## Accessing Environment Variables

```groovy
def call() {
  echo "Build number: ${env.BUILD_NUMBER}"
}
```

Use `env` safely for read-only access.

---

## Error Handling

```groovy
def call() {
  try {
    sh 'run-tests.sh'
  } catch (e) {
    error "Tests failed"
  }
}
```

Use `error()` to fail the pipeline explicitly.

---

## Common Mistakes

- Putting too much logic in `vars`
- Forgetting `call()` method
- Hardcoding environment values
- Mixing credentials logic directly

---

## Best Practices

- Keep `vars` steps small and readable
- Delegate complex logic to `src` classes
- Use Map-based parameters for flexibility
- Version shared libraries

---

## Interview Focus Areas

- Why `call()` is required
- How `vars` steps are loaded
- Difference between `vars` and `src` usage

