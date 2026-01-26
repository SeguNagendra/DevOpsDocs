---
sidebar_position: 2
---

# Credential Types

Jenkins supports multiple credential types to handle different authentication needs.
Choosing the **correct credential type** is critical for security and maintainability.

---

## Why Credential Types Matter

Using the wrong type can:
- Expose secrets
- Break integrations
- Limit automation capabilities

> Always match the credential type to the use case.

---

## Common Jenkins Credential Types

### Username & Password

**Use for:**
- Legacy systems
- Basic authentication

**Avoid when:**
- Tokens or keys are available

---

### Secret Text

**Use for:**
- API tokens
- OAuth tokens
- Webhook secrets

**Most commonly used credential type.**

---

### SSH Username with Private Key

**Use for:**
- Git over SSH
- Server access
- Secure deployments

Supports:
- Direct key entry
- File upload
- Jenkins-managed keys

---

### Certificate

**Use for:**
- Mutual TLS (mTLS)
- PKI-based authentication

Less common but important in regulated environments.

---

### Docker Registry Credentials

**Use for:**
- Authenticating to Docker registries
- Pulling private images

---

## Credential Scope (Reinforced)

- **Global** → All jobs (use carefully)
- **Folder** → Environment-specific (recommended)
- **Job** → Rare, special cases only

---

## Choosing the Right Credential Type

| Use Case | Recommended Type |
|--------|------------------|
| GitHub API | Secret Text |
| Git SSH | SSH Key |
| REST API | Secret Text |
| Legacy app | Username/Password |
| Docker registry | Docker creds |

---

## Common Mistakes

- Using username/password for APIs
- Reusing same credential everywhere
- Storing secrets as parameters
- Wrong scope selection

---

## Best Practices

- Prefer tokens over passwords
- Scope credentials tightly
- Rotate secrets regularly
- Name credentials clearly

---

## Interview Traps

- **Most secure credential type?**  
  → Depends on use case

- **Should secrets be parameters?**  
  → No

- **Where should PROD creds live?**  
  → Folder scope