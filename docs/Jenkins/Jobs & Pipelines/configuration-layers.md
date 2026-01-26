---
sidebar_position: 5
---

# Configuration Layers (Global vs Folder vs Job)

Jenkins configuration exists at **multiple levels**.
Understanding configuration layers prevents **unexpected behavior and overrides** in real projects.

---

## Why Configuration Layers Matter

Misunderstanding configuration scope can lead to:
- Jobs behaving differently than expected
- Security gaps
- Hard-to-debug failures
- Environment inconsistencies

> Always know **where** a configuration is applied.

---

## Jenkins Configuration Levels

Jenkins supports three primary configuration layers:

1. Global Configuration
2. Folder-Level Configuration
3. Job-Level Configuration

Each layer has a **different scope and precedence**.

---

## 1. Global Configuration

### What It Controls
- Global tools (JDK, Maven, Node, Git)
- Credentials
- System-wide environment variables
- Email & notification settings
- Security & authorization

### Where It Is Configured
```
Manage Jenkins → Configure System
Manage Jenkins → Global Tool Configuration
```

### Scope
- Applies to **all jobs**
- Lowest priority (can be overridden)

---

## 2. Folder-Level Configuration

### What It Controls
- Shared credentials
- Environment variables
- Properties inherited by jobs inside the folder

### Why Use Folders
- Logical grouping of jobs
- Environment separation (DEV / QA / PROD)
- Reduced duplication

### Scope
- Applies to jobs inside the folder
- Overrides global configuration

---

## 3. Job-Level Configuration

### What It Controls
- Job-specific settings
- SCM configuration
- Triggers
- Parameters
- Job-level environment variables

### Scope
- Applies only to that job
- **Highest priority**

---

## Configuration Precedence

Order of precedence (highest → lowest):

1. Job-level
2. Folder-level
3. Global-level

> Job-level settings override everything else.

---

## Real-World Example

- Global Git credentials configured
- Folder overrides credentials for PROD
- Job overrides credentials for a special case

Result:
- Job uses its own credentials

---

## Common Misconfigurations

- Hardcoding credentials at job level
- Duplicating config across jobs
- Forgetting folder-level overrides
- Mixing environment configs

---

## Best Practices

- Use global config for shared tools
- Use folders for environment separation
- Keep jobs lightweight
- Document configuration ownership

---

## Interview Traps

- **Which config takes precedence?**  
  → Job-level

- **Where should environment-specific values live?**  
  → Folder-level

- **Should secrets be job-level?**  
  → No, use folder or global credentials
