---
sidebar_position: 2
---

# Shared Library Structure

This document explains the **mandatory directory structure** of a Jenkins Shared Library.
Incorrect structure is the #1 reason shared libraries fail to load.

---

## Standard Shared Library Layout

A Jenkins shared library **must** follow this structure:

```
(shared-library-repo)
├── vars/
│   └── buildPipeline.groovy
├── src/
│   └── com/company/pipeline/Utils.groovy
├── resources/
│   └── templates/
│       └── notification.json
└── README.md
```

Jenkins relies on **convention**, not configuration.

---

## `vars/` Directory

Purpose:
- Defines **global pipeline steps**
- Functions are callable directly from Jenkinsfile

Example:
```groovy
buildPipeline()
```

File rules:
- Filename = function name
- Must contain `call()` method

---

### Example `vars/buildPipeline.groovy`

```groovy
def call() {
  stage('Build') {
    sh 'mvn clean install'
  }
}
```

---

## `src/` Directory

Purpose:
- Contains reusable **Groovy classes**
- Used for complex logic
- Must follow Java package naming

Example usage:
```groovy
def utils = new com.company.pipeline.Utils()
utils.notify()
```

---

### Example `src` Class

```groovy
package com.company.pipeline

class Utils {
  def notify() {
    println "Notifying team"
  }
}
```

---

## `resources/` Directory

Purpose:
- Store non-Groovy files
- Templates, JSON, YAML, shell scripts

Accessed via:
```groovy
libraryResource 'templates/notification.json'
```

---

## Why Structure Matters

- Jenkins auto-loads based on folders
- Misplaced files are ignored
- No runtime error for missing structure
- Failures appear confusing

---

## Common Mistakes

- Putting logic directly in Jenkinsfile
- Not using `call()` in vars files
- Incorrect package names in `src`
- Expecting resources to auto-load

---

## Best Practices

- Use `vars` for simple steps
- Use `src` for logic-heavy code
- Keep Jenkinsfiles thin
- Version shared libraries

---

## Interview Focus Areas

- Difference between `vars` and `src`
- Why `call()` is required
- How resources are accessed

