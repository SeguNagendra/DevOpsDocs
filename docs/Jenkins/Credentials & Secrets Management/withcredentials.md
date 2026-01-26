---
sidebar_position: 4
---

# withCredentials – Deep Dive

`withCredentials` is the **core mechanism** Jenkins uses to inject secrets securely into pipelines.
Every secure Jenkins pipeline relies on this block.

---

## What Is `withCredentials`?

`withCredentials`:
- Temporarily injects secrets into environment variables
- Masks secrets in console output
- Limits secret exposure to a defined block

Secrets exist **only inside the block**.

---

## Basic Pattern

```groovy
withCredentials([
  string(credentialsId: 'api-token', variable: 'API_TOKEN')
]) {
  sh 'curl -H "Authorization: Bearer $API_TOKEN" https://api.example.com'
}
```

Once the block exits, `API_TOKEN` is no longer available.

---

## Using Multiple Credentials

You can bind multiple credentials in a single block:

```groovy
withCredentials([
  string(credentialsId: 'api-token', variable: 'API_TOKEN'),
  usernamePassword(
    credentialsId: 'git-creds',
    usernameVariable: 'GIT_USER',
    passwordVariable: 'GIT_PASS'
  )
]) {
  sh 'git clone https://$GIT_USER:$GIT_PASS@repo'
}
```

---

## Nested `withCredentials` (Allowed but Discouraged)

```groovy
withCredentials([string(credentialsId: 'token1', variable: 'T1')]) {
  withCredentials([string(credentialsId: 'token2', variable: 'T2')]) {
    sh 'echo using tokens'
  }
}
```

Prefer **one block** for clarity.

---

## SSH Key Binding Example

```groovy
withCredentials([
  sshUserPrivateKey(
    credentialsId: 'ssh-key',
    keyFileVariable: 'SSH_KEY',
    usernameVariable: 'SSH_USER'
  )
]) {
  sh 'ssh -i $SSH_KEY $SSH_USER@server'
}
```

The private key file is created temporarily and deleted after the block.

---

## File Credential Binding

```groovy
withCredentials([
  file(credentialsId: 'config-file', variable: 'CONF')
]) {
  sh 'cat $CONF'
}
```

Use this for:
- Config files
- Certificates
- Service account JSON files

---

## Masking Limitations (Important)

Masking can fail if:
- Secrets are transformed (base64, substrings)
- Secrets are echoed character by character
- Secrets are written to files and printed

Never assume masking is foolproof.

---

## Scope & Lifetime

| Property | Behavior |
|-------|---------|
| Scope | Block-level |
| Lifetime | Temporary |
| Masked | Yes |
| Workspace persistence | No |

---

## Common Mistakes

- Binding secrets globally
- Logging secret-derived values
- Using `env.SECRET` outside block
- Passing secrets to parallel steps carelessly

---

## Best Practices

- Use one `withCredentials` block per stage
- Keep blocks small
- Never print secrets (even masked)
- Prefer folder-scoped credentials
- Rotate credentials regularly

---

## Interview Checks

- `withCredentials` scope and lifetime
- Difference between file and string bindings
- Why masking can fail

