---
sidebar_position: 5
---

# Common Credential Mistakes

Credential-related mistakes are the **most frequent cause of security incidents** in Jenkins.
This document focuses on **real-world failures** and how to avoid them.

---

## Hardcoding Secrets in Jenkinsfile

### ❌ Bad Practice
```groovy
sh 'curl -H "Authorization: Bearer abc123" https://api.example.com'
```

### ✅ Correct
```groovy
withCredentials([
  string(credentialsId: 'api-token', variable: 'API_TOKEN')
]) {
  sh 'curl -H "Authorization: Bearer $API_TOKEN" https://api.example.com'
}
```

---

## Printing Secrets to Logs

### ❌ Bad Practice
```groovy
echo "Token is $API_TOKEN"
```

Even masked values can leak via transformations.

### ✅ Correct
Never log secrets or derived values.

---

## Using Environment Block for Secrets

### ❌ Bad Practice
```groovy
environment {
  DB_PASSWORD = 'secret'
}
```

Environment blocks are **not secure** for secrets.

### ✅ Correct
Use `withCredentials` only.

---

## Passing Secrets as Parameters

### ❌ Bad Practice
- Parameters are visible in UI
- Parameters may be logged

### ✅ Correct
Use Jenkins credentials store.

---

## Global Scope Overuse

### Problem
- One credential used everywhere
- Hard to rotate
- High blast radius

### Better Approach
- Folder-scoped credentials
- Environment separation (DEV / QA / PROD)

---

## Writing Secrets to Files

### Risk
- Files may be archived
- Files may be stashed
- Files may leak

### Mitigation
- Use file credentials
- Delete files after use

---

## Masking Assumptions

### Reality
Masking fails when:
- Secrets are split
- Encoded
- Manipulated

Never rely on masking alone.

---

## Reusing Credentials Across Systems

### Risk
- One leak compromises multiple systems

### Best Practice
- One credential per integration
- Rotate regularly

---

## Missing Access Control

### Problem
- Too many users can access secrets

### Fix
- Role-based access
- Least privilege

---

## Production Checklist

- No secrets in Jenkinsfile
- No secrets in parameters
- Folder-level credentials used
- Secrets rotated periodically
- Access reviewed regularly

---

## Interview Focus Areas

- Why parameters are unsafe for secrets
- How masking works and fails
- Folder vs global credential scope

