---
sidebar_position: 11
---

# Terraform Interview Questions

### Conceptual
- Why does Terraform need state?
- Provider vs backend difference
- count vs for_each

### Scenario-Based
- How do you prevent accidental deletion?
- How do teams manage prod Terraform?
- How do you handle drift?

### Advanced
- How do you refactor without downtime?
- How does Terraform dependency graph work?

---

## How Real Teams Use Terraform

- Terraform = infrastructure lifecycle
- CI/CD controls execution
- Humans approve changes
- Monitoring detects drift

Terraform is **not a one-person tool**.

---

## Common Career-Limiting Mistakes

❌ Running terraform apply on prod locally  
❌ Editing state files manually  
❌ Ignoring plan output  
❌ Treating Terraform like a script  

---

## Final Best Practices Checklist

✅ Remote state with locking  
✅ Version pinning  
✅ Modular code  
✅ CI/CD pipelines  
✅ Approval workflows  
✅ Environment isolation  

---

## Final Summary

You now understand:
- Terraform from fundamentals to production
- How Terraform behaves internally
- How to troubleshoot failures
- How to answer real interview questions
- How to use Terraform safely at scale

Terraform mastery is about **discipline, not commands**.

---

🎉 **Congratulations! You now have a complete, production-grade Terraform handbook.**
