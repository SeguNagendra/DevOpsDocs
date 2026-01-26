---
sidebar_position: 3
---

# Credentials Binding

Credentials Binding is the **safe and recommended way** to inject secrets into Jenkins pipelines.
It ensures secrets are **masked, scoped, and short-lived**.

---

## What Is Credentials Binding?

Credentials Binding allows Jenkins to:
- Inject secrets into environment variables
- Mask secrets in console logs
- Limit secret exposure to a specific scope

> This is safer than using plain environment variables.

---

## Why Credentials Binding Is Important

Without binding:
- Secrets may appear in logs
- Secrets may leak into workspace files
- Secrets may persist longer than required

Binding ensures **least privilege and minimal exposure**.

---

## Basic Binding Example

```groovy
pipeline {
  agent any
  stages {
    stage('Call API') {
      steps {
        withCredentials([
          string(credentialsId: 'api-token', variable: 'API_TOKEN')
        ]) {
          sh 'curl -H "Authorization: Bearer $API_TOKEN" https://api.example.com'
        }
      }
    }
  }
}
```

---

## Supported Binding Types

Common bindings:
- `string` → Secret Text
- `usernamePassword`
- `sshUserPrivateKey`
- `file`

Example:
```groovy
withCredentials([
  usernamePassword(credentialsId: 'git-creds',
                   usernameVariable: 'GIT_USER',
                   passwordVariable: 'GIT_PASS')
]) {
  sh 'git clone https://$GIT_USER:$GIT_PASS@repo'
}
```

---

## Masking Behavior

- Jenkins masks secret values in logs
- Masking applies only inside binding scope
- Secrets echoed outside scope may leak

---

## Scope & Lifetime

| Aspect | Credentials Binding |
|------|---------------------|
| Scope | Block-level |
| Lifetime | Temporary |
| Masked in logs | Yes |
| Stored in workspace | No |

---

## Common Mistakes

- Using `env.VAR` for secrets
- Echoing secrets explicitly
- Binding secrets globally
- Writing secrets to files unnecessarily

---

## Best Practices

- Always use `withCredentials`
- Keep binding scope minimal
- Never log secrets
- Rotate credentials regularly

---

## Interview Traps

- **Is masking guaranteed?**  
  → Only within binding scope

- **Can secrets leak to files?**  
  → Yes, if written explicitly

- **Should credentials be global env vars?**  
  → No
