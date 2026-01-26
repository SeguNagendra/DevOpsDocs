---
sidebar_position: 4
---

# Input Step (Manual Approval)

The `input` step allows a Jenkins pipeline to **pause and wait for human approval**.
This is essential for **production deployments and gated workflows**.

---

## What Is the `input` Step?

The `input` step:
- Pauses pipeline execution
- Waits for user interaction
- Collects approval or input
- Resumes execution after approval

> Commonly used before PROD deployments.

---

## Basic Syntax

```groovy
input {
  message 'Deploy to production?'
}
```

This pauses the pipeline until someone clicks **Proceed** or **Abort**.

---

## Input with Confirmation Message

```groovy
input message: 'Approve deployment to PROD'
```

---

## Input with Parameters

The `input` step can also collect values:

```groovy
input(
  message: 'Approve deployment',
  parameters: [
    string(name: 'RELEASE_VERSION', defaultValue: '1.0.0')
  ]
)
```

---

## Input with Timeout (Important)

Never leave pipelines waiting forever.

```groovy
timeout(time: 10, unit: 'MINUTES') {
  input message: 'Approve PROD deployment'
}
```

---

## Where Input Is Typically Used

- Before production deployment
- Before destructive operations
- Before data migrations

---

## Security Considerations

- Only authorized users should approve
- Use role-based access control
- Avoid approvals from service accounts

---

## Common Mistakes

- No timeout on input
- Placing input too early in pipeline
- Allowing too many users to approve
- Using input in non-critical stages

---

## Best Practices

- Use input only for high-risk steps
- Always add a timeout
- Combine with branch checks
- Log approval decisions

---

## Interview Traps

- **Does input block an executor?**  
  → Yes, unless `beforeAgent` logic avoids it

- **Can input collect parameters?**  
  → Yes

- **Should input be used in DEV?**  
  → Usually no