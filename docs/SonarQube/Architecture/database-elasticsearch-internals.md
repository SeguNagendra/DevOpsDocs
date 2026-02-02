---
sidebar_position: 7
---

# Database & Elasticsearch Internals – Storage, Indexing, Performance

SonarQube relies heavily on its storage layer.
Many production issues are not caused by bad scans or rules, but by **database or Elasticsearch problems**.

This chapter explains these internals in a clear, practical way.

---

## Why Storage Matters in SonarQube

Every scan produces:
- Issues
- Metrics
- Quality Gate results
- Historical data

If storage is unstable:
- UI becomes slow
- Results appear inconsistent
- Scans may succeed but data looks wrong

Understanding storage helps you run SonarQube **reliably in production**.

---

## The Database – Source of Truth

SonarQube uses a relational database to store **authoritative data**.

### What Is Stored in the Database
- Projects and configuration
- Issues and their status
- Metrics and measures
- Users, roles, and permissions
- Quality Profiles and Quality Gates

The database is the **single source of truth**.

---

## Why PostgreSQL Is Recommended

For production, SonarQube strongly recommends PostgreSQL because:
- It is stable and well-tested
- Handles concurrent access reliably
- Works well with SonarQube upgrades
- Has strong community and tooling support

Other databases may work for testing, but PostgreSQL is safest for long-term use.

---

## Important Database Rules

Follow these rules strictly:
- ❌ Never edit the database manually
- ❌ Never run custom queries to “fix” issues
- ✅ Always use the SonarQube UI or API

Manual DB changes can corrupt data and break upgrades.

---

## Elasticsearch – Search and Performance Engine

Elasticsearch is used by SonarQube to:
- Index issues and metrics
- Enable fast searching
- Power dashboards and filtering
- Improve UI responsiveness

Without Elasticsearch, the UI would be extremely slow.

---

## What Lives in Elasticsearch vs Database

Understanding the split helps troubleshooting.

- **Database** → authoritative data  
- **Elasticsearch** → indexed, searchable views  

If Elasticsearch data is lost:
- SonarQube can rebuild indexes
- No permanent data loss occurs

If database data is lost:
- Data is gone permanently

---

## Common Elasticsearch Problems

Typical Elasticsearch-related issues:
- OutOfMemory errors
- Disk space exhaustion
- Slow queries
- Index corruption

Most of these are caused by:
- Insufficient memory
- Poor disk performance
- Large projects without tuning

---

## Performance & Memory Considerations

Basic best practices:
- Allocate sufficient RAM
- Monitor disk usage
- Avoid running SonarQube on overloaded hosts
- Separate DB from SonarQube server in production

Good infrastructure prevents most problems.

---

## Reindexing and Maintenance

Sometimes Elasticsearch indexes need rebuilding:
- After upgrades
- After crashes
- After disk issues

SonarQube provides built-in reindexing tools.
Always prefer official methods over manual fixes.

---

## Key Takeaway

SonarQube is not just an application — it is a **data platform**.

Treating the database and Elasticsearch properly:
- Improves reliability
- Prevents data loss
- Makes performance predictable

---

➡️ **Next:** Installation & Setup  
