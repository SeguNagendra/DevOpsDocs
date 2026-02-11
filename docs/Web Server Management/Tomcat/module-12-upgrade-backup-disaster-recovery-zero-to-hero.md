---
sidebar_position: 12
title: Upgrade, Backup & Disaster Recovery
---

# Upgrade, Backup & Disaster Recovery

Production systems are not "set and forget".

Over time you must:

-   Upgrade Tomcat versions
-   Apply security patches
-   Backup configurations
-   Plan for failures
-   Recover from crashes

If you do not plan upgrades and backups properly, you risk long downtime
and data loss.

In this module, you will clearly understand:

-   Tomcat upgrade strategy
-   Rolling upgrade concept
-   What to backup
-   Backup best practices
-   Disaster Recovery (DR) basics
-   Recovery runbook concept
-   Real-world crash recovery steps

------------------------------------------------------------------------

# 1. Why Upgrades Are Important

Tomcat upgrades may include:

-   Security fixes
-   Performance improvements
-   Bug fixes
-   Compatibility updates

Running outdated Tomcat can expose system to vulnerabilities.

DevOps responsibility: Regularly check for new stable versions and CVE
announcements.

------------------------------------------------------------------------

# 2. Types of Upgrades

Minor Upgrade: Example: 9.0.70 → 9.0.80\
Usually safe, low risk.

Major Upgrade: Example: 9.x → 10.x\
May include breaking changes (API differences).

Always test in Dev/QA before production.

------------------------------------------------------------------------

# 3. Safe Upgrade Strategy (Basic Production Approach)

Never upgrade directly on live instance without backup.

Safe steps:

1.  Backup current Tomcat directory.
2.  Download new version.
3.  Extract in separate directory.
4.  Copy required configurations (carefully).
5.  Deploy application.
6.  Test functionality.
7.  Switch traffic (if behind Load Balancer).

This reduces risk.

------------------------------------------------------------------------

# 4. Rolling Upgrade Concept

If you have two Tomcat instances:

Instance A\
Instance B

Upgrade process:

1.  Remove A from Load Balancer.
2.  Upgrade A.
3.  Test A.
4.  Add A back to Load Balancer.
5.  Repeat same steps for B.

Users never experience downtime.

Rolling upgrade is best practice in HA environments.

------------------------------------------------------------------------

# 5. What Should You Backup?

Critical items:

✔ conf/ directory\
✔ server.xml\
✔ context.xml\
✔ web.xml\
✔ WAR files\
✔ SSL keystore\
✔ setenv.sh\
✔ Logs (if needed for audit)

Never rely on memory. Always take structured backups.

------------------------------------------------------------------------

# 6. Backup Best Practices

-   Store backups outside server (remote storage).
-   Use versioned backups.
-   Automate backup process.
-   Test restore process occasionally.

Backup that cannot be restored is useless.

------------------------------------------------------------------------

# 7. Disaster Recovery (DR) Basics

Disaster can be:

-   Server crash
-   Disk failure
-   Data corruption
-   Cloud instance termination
-   Accidental deletion

DR means: Ability to restore service quickly.

Key concepts:

RTO (Recovery Time Objective) → How fast system must recover.

RPO (Recovery Point Objective) → How much data loss is acceptable.

------------------------------------------------------------------------

# 8. Basic DR Strategy for Tomcat

Scenario: Server crashed completely.

Steps:

1.  Provision new server (VM or cloud instance).
2.  Install Java.
3.  Install Tomcat.
4.  Restore backup configurations.
5.  Deploy WAR file.
6.  Restore SSL certificate.
7.  Verify connectivity.
8.  Add back to Load Balancer.

If automation exists, recovery is faster.

------------------------------------------------------------------------

# 9. Importance of Documentation (Runbook)

Every production system should have a runbook.

Runbook includes:

-   Installation steps
-   Upgrade steps
-   Backup steps
-   Recovery steps
-   Contact information
-   Monitoring setup

During outage, clear documentation saves time.

------------------------------------------------------------------------

# 10. Common Upgrade Mistakes

❌ Upgrading without backup\
❌ Directly modifying production config\
❌ Skipping testing\
❌ Ignoring compatibility issues\
❌ Not validating after upgrade

Always validate:

-   Application working
-   Logs clean
-   Health checks passing
-   Performance normal

------------------------------------------------------------------------

# 11. Real-World Crash Scenario

Scenario:

Server disk corrupted.

If no backup: Application rebuild may take hours.

If backup available: Restore within minutes.

Difference between chaos and control is preparation.

------------------------------------------------------------------------

# 12. Production Upgrade Checklist

Before upgrade:

✔ Backup taken\
✔ Downtime window planned (if needed)\
✔ QA validation done\
✔ Rollback plan ready

After upgrade:

✔ Logs verified\
✔ Health checks passing\
✔ Load balancer routing properly\
✔ Monitoring alerts normal

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Understand why upgrades matter\
✔ Perform safe Tomcat upgrade\
✔ Execute rolling upgrade\
✔ Know what to backup\
✔ Understand DR basics\
✔ Follow structured recovery steps\
✔ Maintain runbook documentation

Next: Real-World Production Scenarios & Interview Preparation.
