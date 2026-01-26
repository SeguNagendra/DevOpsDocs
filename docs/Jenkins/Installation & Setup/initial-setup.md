---
sidebar_position: 4
---

# Jenkins Initial Setup

This guide walks through the **first-time Jenkins setup** after installation.
Correct initial setup is critical for **security, stability, and maintainability**.

---

## Unlock Jenkins

When Jenkins starts for the first time, it is locked.

### Retrieve Initial Admin Password

#### Local / Linux / macOS
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

#### Docker
```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Paste the password into the Jenkins UI to continue.

---

## Plugin Installation Strategy

### Install Suggested Plugins?
- ❌ Not recommended for production
- Installs many unused plugins

### Recommended Approach
- Install **minimal required plugins**
- Add plugins only when needed

Core plugins usually required:
- Git
- Pipeline
- Credentials Binding
- SSH Agent
- Workspace Cleanup

---

## Create Admin User

- Create a dedicated admin user
- Do not continue using the initial admin password
- Use a strong password

---

## Configure Jenkins URL

Set:
```
Manage Jenkins → Configure System → Jenkins URL
```

This is required for:
- Webhooks
- Email notifications
- External integrations

---

## Global Security Settings

### Authentication
- Jenkins internal user database (for learning)
- LDAP / SSO (enterprise)

### Authorization
- Matrix-based security (recommended)
- Avoid “Anyone can do anything”

---

## Disable Controller Executors (Important)

```
Manage Jenkins → Nodes → Built-in Node → Executors → 0
```

> Prevents builds from running on controller.

---

## Basic Hardening Checklist

- Disable anonymous access
- Enable CSRF protection
- Limit admin users
- Regularly update plugins
- Backup JENKINS_HOME

---

## Verify Setup

Confirm:
- Jenkins dashboard loads
- Admin user login works
- No warnings in system logs

---

## Common Mistakes

- Too many plugins installed initially
- Leaving controller executors enabled
- Weak admin passwords
