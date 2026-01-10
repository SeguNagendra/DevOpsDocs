
# AWS IAM – Complete Notes (DevOps & Cloud Architect)

> Easy to read • Real-world • Visual memory • Practical JSON

---

## 1. What is AWS IAM?

AWS Identity and Access Management (IAM) controls:
- WHO can access AWS
- WHAT actions they can perform
- WHICH resources they can access

![IAM Overview](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-overview.png)

---

## 2. IAM Dashboard (Console View)

This is the first screen you see when opening IAM.

![IAM Dashboard](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-dashboard.png)

IAM is a **global service** (no region selector).

---

## 3. IAM Users

IAM users represent people or service accounts.

![IAM Users](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-users-list.png)

Best practices:
- Do NOT use root user
- Enable MFA
- Avoid long-term access keys

---

## 4. IAM Groups

Groups simplify permission management.

![IAM Groups](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-groups-list.png)

Example:
- Dev → EC2 read
- QA → Read-only
- DevOps → Full infra

---

## 5. IAM Policies (Most Important)

Policies define permissions using JSON.

![IAM Policy Editor](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-policy-editor-visual.png)

### EC2 Read-Only Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    }
  ]
}
```

### S3 Upload Only Policy
```json
{
  "Effect": "Allow",
  "Action": "s3:PutObject",
  "Resource": "arn:aws:s3:::dev-bucket/*"
}
```

Policy evaluation:
1. Explicit Deny
2. Explicit Allow
3. Default Deny

---

## 6. IAM Roles (DevOps Core)

Roles provide **temporary access** without storing credentials.

![IAM Roles](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-roles-list.png)

Used by:
- EC2
- Lambda
- EKS
- CI/CD pipelines

---

## 7. Trust Policy

Defines who can assume a role.

![Trust Policy](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-role-trust-policy.png)

```json
{
  "Effect": "Allow",
  "Principal": {
    "Service": "ec2.amazonaws.com"
  },
  "Action": "sts:AssumeRole"
}
```

---

## 8. Real Scenario – EC2 Accessing S3

![EC2 S3 Role Flow](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-roles-how-it-works.png)

Flow:
EC2 → IAM Role → Temporary Credentials → S3

---

## 9. IAM for CI/CD (OIDC)

![OIDC IAM](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-oidc-github-actions.png)

Best practice:
- Use IAM Role + OIDC
- No AWS keys stored

---

## 10. Security Best Practices

![IAM MFA](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/iam-mfa.png)

- Enable MFA on root
- Disable root keys
- Use least privilege
- Enable CloudTrail

---

## 11. Interview Cheat Sheet

- User vs Role → Permanent vs Temporary
- IAM default → Deny
- Secure CI/CD → OIDC + Role
- Auditing → CloudTrail

---

## Final Advice

IAM is the foundation of AWS security.
Strong IAM = Secure cloud.
