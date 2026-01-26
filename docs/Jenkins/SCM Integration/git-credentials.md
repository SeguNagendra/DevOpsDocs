---
sidebar_position: 2
---

# Git Credentials & Access Methods

This document explains **how Jenkins authenticates with Git repositories**.
Choosing the correct access method is critical for security, reliability, and automation.

---

## Git Access Methods in Jenkins

Jenkins can access Git repositories using:

- HTTPS with token
- SSH with private key

> Password-based Git access is deprecated and insecure.

---

## HTTPS Access (Token-Based)

### When to Use
- GitHub / GitLab / Bitbucket
- API-driven platforms
- Simpler setup

### Recommended Credential Type
- **Secret Text** (Personal Access Token)

---

### Example (Pipeline)

```groovy
withCredentials([
  string(credentialsId: 'git-token', variable: 'GIT_TOKEN')
]) {
  sh 'git clone https://$GIT_TOKEN@github.com/org/repo.git'
}
```

> Prefer Jenkins SCM configuration over manual clone in pipelines.

---

## SSH Access (Key-Based)

### When to Use
- Private repositories
- Enterprise environments
- Long-lived automation

### Recommended Credential Type
- **SSH Username with Private Key**

---

### Example (Pipeline)

```groovy
withCredentials([
  sshUserPrivateKey(
    credentialsId: 'git-ssh-key',
    keyFileVariable: 'SSH_KEY',
    usernameVariable: 'SSH_USER'
  )
]) {
  sh 'GIT_SSH_COMMAND="ssh -i $SSH_KEY" git clone git@github.com:org/repo.git'
}
```

---

## HTTPS vs SSH (Comparison)

| Aspect | HTTPS (Token) | SSH (Key) |
|-----|---------------|-----------|
| Setup | Easy | Moderate |
| Security | Good | Very Good |
| Token rotation | Easy | Harder |
| Firewall friendly | Yes | Sometimes |
| Enterprise use | Common | Very common |

---

## Recommended Practices

- Prefer **SSH keys** for long-term automation
- Use **tokens** for SaaS Git providers
- Scope credentials per repository or folder
- Rotate tokens and keys periodically

---

## Credential Scope Guidance

- **Global** → Avoid unless shared infra
- **Folder** → Best practice
- **Job** → Rare edge cases

---

## Common Mistakes

- Using Git username/password
- Reusing same credential for all repos
- Hardcoding repo URLs with secrets
- Storing SSH keys on agents

---

## Security Notes

- Never commit credentials
- Do not echo Git URLs with tokens
- Restrict who can configure SCM

---

## Interview Focus Areas

- HTTPS vs SSH trade-offs
- Why passwords are unsafe
- How Jenkins injects Git credentials

