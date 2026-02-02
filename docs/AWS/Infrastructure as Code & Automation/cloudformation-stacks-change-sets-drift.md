---
sidebar_position: 5
title: CloudFormation Stacks, Change Sets and Drift Detection
---

# CloudFormation Stacks, Change Sets and Drift Detection

Writing templates is only half the story.
**Operating CloudFormation safely in real environments** requires understanding stacks, updates, change sets, and drift detection.

This is where IaC becomes **production-ready**.

---

## What Is a CloudFormation Stack?

A stack is:
- A running instance of a CloudFormation template
- A collection of AWS resources managed together

Key rule:
> **CloudFormation manages the lifecycle of all resources in a stack**

---

## Stack Lifecycle

A CloudFormation stack goes through:

1. CREATE
2. UPDATE
3. DELETE
4. ROLLBACK (if failure)

Understanding lifecycle helps:
- Troubleshooting failures
- Safe updates

---

## Updating Stacks

Stack updates:
- Modify existing resources
- Add or remove resources
- Apply template changes

Best practice:
- Never update stacks blindly

---

## Change Sets (Very Important)

Change sets:
- Show what will change before execution
- Preview resource additions, modifications, deletions

Benefits:
- Prevent accidental deletions
- Increase confidence

Rule:
> **Always review change sets in production**

---

## Example: Change Set Output

A change set shows:
- Resources to add
- Resources to modify
- Resources to delete
- Replacement-required changes

This visibility prevents outages.

---

## Stack Rollbacks

If an update fails:
- CloudFormation rolls back automatically
- Restores previous state (where possible)

Rollback protects:
- Partial deployments
- Broken environments

---

## Stack Deletion Protection

Enable termination protection to:
- Prevent accidental stack deletion

Best practice:
- Enable for production stacks

---

## What Is Drift Detection?

Drift occurs when:
- Stack resources are changed manually
- Actual state differs from template

Example:
- Security group edited in console

Drift breaks IaC guarantees.

---

## Drift Detection in CloudFormation

CloudFormation can:
- Detect drift at stack or resource level
- Report drifted resources

Statuses:
- IN_SYNC
- DRIFTED
- NOT_CHECKED

---

## Handling Drift

Best practices:
- Avoid manual changes
- If drift exists, fix via template
- Re-sync infrastructure using IaC

Never:
> **Accept drift as normal**

---

## Stack Policies (Advanced Preview)

Stack policies:
- Protect critical resources
- Control update behavior

Example:
- Prevent accidental RDS replacement

---

## Common Beginner Mistakes

- No change set review
- Manual resource edits
- Large monolithic stacks
- No termination protection

These cause:
- Outages and drift

---

## Interview Tip

If asked:
> “How do you safely update CloudFormation stacks?”

Strong answer:
> By using change sets, rollback protection, and avoiding manual changes.

---

## Key Takeaways

- Stacks manage infrastructure lifecycle
- Change sets enable safe updates
- Rollbacks protect environments
- Drift detection enforces IaC discipline
- Essential for production use

---

📌 **Next:** Modular CloudFormation and Nested Stacks
