---
sidebar_position: 8
---

# Installation & Setup – Running SonarQube the Right Way

Installing SonarQube looks simple on the surface, but many production issues start with
**improper installation and sizing**.

This chapter focuses on installing SonarQube **correctly**, not just quickly.

---

## Choosing the Right Installation Model

SonarQube can be installed in multiple ways. Each serves a different purpose.

### Local Installation
Best for:
- Learning
- Demos
- Quick experiments

Not recommended for production due to limited scalability.

---

### Docker Installation
Best for:
- Development and testing
- Consistent environments
- Quick setup

Docker simplifies setup but still requires proper memory and volume configuration.

---

### VM / Bare Metal Installation
Best for:
- Production environments
- Long-term stability
- Better performance control

This is the most common enterprise setup.

---

### Kubernetes (High-Level View)
Used in:
- Large organizations
- Platform teams

Requires advanced knowledge and careful tuning.
For most teams, VM-based deployment is simpler and safer.

---

## System Requirements (Why They Matter)

SonarQube is resource-intensive.

Key requirements:
- Java version compatible with SonarQube release
- Adequate RAM (very important)
- Fast disk I/O
- Sufficient file descriptors

Under-provisioning leads to slow UI, failed scans, and Elasticsearch crashes.

---

## Java & OS Considerations

- Use the Java version recommended by SonarQube
- Avoid unsupported Java versions
- Tune OS limits for:
  - Open files
  - Memory usage

These settings directly affect stability.

---

## Database Setup

Production best practice:
- Use PostgreSQL
- Run DB on a separate server
- Enable backups from day one

Never use embedded or test databases in production.

---

## First-Time Startup

When starting SonarQube for the first time:
- Access the Web UI
- Change the default admin password
- Configure base settings
- Create authentication tokens

This initial setup is critical for security.

---

## Token Creation & Usage

Tokens are used for:
- Scanner authentication
- CI/CD integration

Best practices:
- One token per project or pipeline
- Store tokens in secret managers
- Rotate tokens periodically

Never commit tokens to source control.

---

## Common Installation Mistakes

Avoid these issues:
- Running SonarQube with insufficient memory
- Using unsupported Java versions
- Sharing disk with heavy workloads
- Skipping backups

Most problems are preventable with proper setup.

---

## Key Takeaway

A stable SonarQube installation:
- Prevents performance issues
- Simplifies maintenance
- Saves hours of troubleshooting later

Install it once, install it right.

---

➡️ **Next:** First Project Analysis  
