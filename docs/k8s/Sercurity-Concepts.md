---
sidebar_position: 16
---


# Kubernetes Security Concepts

This document provides a complete explanation of Kubernetes security model components:
- **ServiceAccount**
- **RBAC (Role, ClusterRole)**
- **RoleBinding, ClusterRoleBinding**
- **Pod Security Standards (PSS)**
- **SecurityContext**
- **NetworkPolicy**

Each topic includes examples and clear explanations.

---

# 1. Kubernetes Security Model

Kubernetes security is built on multiple layers:

### 1. Identity
Who is making the request?
- User
- ServiceAccount
- Node (kubelet)

### 2. Authentication
How do we verify identity?
- Certificates
- Tokens
- ServiceAccount tokens
- OIDC

### 3. Authorization
What is the user allowed to do?
- RBAC
- ABAC (deprecated)
- Node authorizer

### 4. Admission Control
Should the request be allowed to change the cluster?
- Pod Security Admission (PSS)
- Image policy webhooks

### 5. Runtime Security
Securing containers at runtime:
- SecurityContext
- seccomp
- capabilities

---

# 2. ServiceAccount

A **ServiceAccount** provides an identity for Pods to interact with the API server.

### Why ServiceAccounts?
- Pods need to access Kubernetes API
- More secure than using user credentials
- Default ServiceAccount is automatically mounted unless disabled

---

## 2.1 Create ServiceAccount

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: app-sa
```

Assign it to a Pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sa-demo
spec:
  serviceAccountName: app-sa
  containers:
    - name: app
      image: nginx
```

---

# 3. RBAC (Role-Based Access Control)

RBAC controls **who can do what** on which objects.

### RBAC Components:

| Component | Scope | Purpose |
|----------|--------|---------|
| **Role** | Namespace | Permissions for resources in a namespace |
| **ClusterRole** | Cluster-wide | Global permissions |
| **RoleBinding** | Namespace | Bind Role to user/SA |
| **ClusterRoleBinding** | Cluster-wide | Bind ClusterRole to user/SA |

---

# 4. Role & RoleBinding

### 4.1 Create a Role (namespace-scoped)
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: dev
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
```

### 4.2 Bind Role to a ServiceAccount
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: dev
subjects:
  - kind: ServiceAccount
    name: app-sa
    namespace: dev
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

# 5. ClusterRole & ClusterRoleBinding

Use when permissions are needed **across all namespaces**.

### 5.1 Create ClusterRole
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: namespace-admin
rules:
  - apiGroups: [""]
    resources: ["namespaces"]
    verbs: ["get", "list"]
```

### 5.2 Create ClusterRoleBinding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ns-admin-binding
subjects:
  - kind: ServiceAccount
    name: app-sa
    namespace: dev
roleRef:
  kind: ClusterRole
  name: namespace-admin
  apiGroup: rbac.authorization.k8s.io
```

---

# 6. Pod Security Standards (PSS)

PSS defines three security levels:

| Level | Description |
|--------|-------------|
| **Privileged** | No restrictions |
| **Baseline** | Prevent known privilege escalations (recommended) |
| **Restricted** | Most secure; enforces strict isolation |

PSS replaces PodSecurityPolicy (deprecated).

### Example: Enforce "restricted" policy on a namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: secure-ns
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/audit: restricted
    pod-security.kubernetes.io/warn: restricted
```

---

# 7. SecurityContext

Controls how Pods and containers run at OS level.

### SecurityContext Features:
- Run as specific user/group
- Drop Linux capabilities
- Control file permissions
- Read-only root filesystem
- SELinux options
- allowPrivilegeEscalation

---

## 7.1 SecurityContext Example (Container-level)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: securitycontext-demo
spec:
  containers:
    - name: app
      image: nginx
      securityContext:
        runAsUser: 1000
        readOnlyRootFilesystem: true
        capabilities:
          drop: ["ALL"]
```

---

## 7.2 Pod-level SecurityContext
```yaml
securityContext:
  fsGroup: 2000
```

Makes mounted volumes writable by group 2000.

---

# 8. NetworkPolicy

NetworkPolicies restrict **which Pods can talk to which Pods**.

### Purpose:
- Block all traffic by default (zero trust)
- Allow only necessary communication
- Control ingress and egress

NetworkPolicies work **only if your CNI supports them**:
- Calico  
- Cilium  
- Weave Net  

---

## 8.1 Default Deny Policy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
  namespace: dev
spec:
  podSelector: {}
  policyTypes:
    - Ingress
    - Egress
```

Blocks all traffic in namespace `dev`.

---

## 8.2 Allow Traffic Only from Specific App

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
  namespace: dev
spec:
  podSelector:
    matchLabels:
      app: backend
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
      ports:
        - protocol: TCP
          port: 80
```

Meaning:
- Only Pods with `app=frontend` can access backend Pods.

---

# 9. Summary

| Security Component | Purpose |
|---------------------|---------|
| **ServiceAccount** | Identity for Pods |
| **RBAC** | What a user/SA can perform |
| **PSS** | Defines allowed Pod-level security |
| **SecurityContext** | OS-level container restrictions |
| **NetworkPolicy** | Network-level traffic control |

Kubernetes uses multiple layers of security working together:
- Identity  
- Permissions  
- Runtime restrictions  
- Network isolation  

This multi-layer security model helps ensure cluster safety and workload isolation.

---

# Kubernetes RoleBinding Types 
This document provides a **clean and detailed explanation** of all RoleBinding types in Kubernetes, including:  
- Role vs ClusterRole  
- RoleBinding vs ClusterRoleBinding  
- How permissions propagate  
- Real-world examples  
- Common interview questions  

---

# 1. Understanding Kubernetes RBAC  
Kubernetes RBAC (Role-Based Access Control) defines **who** can perform **what action** on **which resource**.

It uses four primary objects:

| Object | Scope | Purpose |
|--------|--------|----------|
| **Role** | Namespace | Permissions for that namespace |
| **ClusterRole** | Cluster-wide | Global or reusable permissions |
| **RoleBinding** | Namespace | Grants a Role or ClusterRole to a subject |
| **ClusterRoleBinding** | Cluster-wide | Grants a ClusterRole cluster-wide |

---

# 2. RoleBinding – Detailed Explanation  
A **RoleBinding** grants permissions *within a specific namespace*.  
It can bind:

- A **Role** → namespace-scoped permissions  
- A **ClusterRole** → apply ClusterRole permissions *inside the namespace only*  

**Important:** RoleBinding CANNOT grant cluster-wide permissions.

---

## 2.1 Syntax of a RoleBinding  
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: dev
subjects:
  - kind: User
    name: dev-user
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

# 3. Types of RoleBindings (Based on RoleRef)

## 🔹 Type 1: RoleBinding → Role (Common Use Case)  
This gives permissions defined in a **Role** for that namespace.

### Example: Allow reading Pods in namespace `dev`
```yaml
roleRef:
  kind: Role
  name: pod-reader
```

➡ Only resources inside **dev** namespace are accessible.

---

## 🔹 Type 2: RoleBinding → ClusterRole (Namespace-Scoped Access)  
You can bind a **ClusterRole** to a namespace using a RoleBinding.

Useful when:
- You want standardized permissions across many namespaces  
- Example: “view” ClusterRole used by many teams  

### Example:
```yaml
roleRef:
  kind: ClusterRole
  name: view
```

➡ ClusterRole permissions apply **only within the RoleBinding namespace**.

---

# 4. ClusterRoleBinding – Detailed Explanation  
ClusterRoleBinding grants permissions **cluster-wide**.

It can bind a **ClusterRole** to:
- Users  
- Groups  
- ServiceAccounts  

---

## 4.1 Example ClusterRoleBinding  
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding
subjects:
  - kind: User
    name: admin-user
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```

➡ User gets **full cluster-wide access**.

---

# 5. Key Differences Between RoleBinding & ClusterRoleBinding

| Feature | RoleBinding | ClusterRoleBinding |
|---------|--------------|---------------------|
| Scope | Namespace only | Cluster-wide |
| Grants Role | Yes | No |
| Grants ClusterRole | Yes (namespace only) | Yes (cluster-wide) |
| Common Use | Team-level access | Admin/system-level access |

---

# 6. Real-World Use Cases

### ✅ Use RoleBinding When:
- Creating developer access to only one namespace  
- Allowing read-only access to team resources  
- Binding ClusterRole “view/edit” per namespace  

### Example:
Dev team gets access ONLY to `dev` namespace.

---

### ✅ Use ClusterRoleBinding When:
- User needs cluster-wide access  
- Granting permissions to system components  
- Granting node-level or storage-level permissions  

### Example:
Cluster autoscaler, metrics server, kubelet use ClusterRoleBinding.

---

# 7. Common Mistakes to Avoid
❌ Using RoleBinding to give cluster-wide permissions  
→ Not possible. RoleBinding applies only to its namespace.

❌ Binding a Role with ClusterRoleBinding  
→ Not allowed. ClusterRoleBinding requires a *ClusterRole*.

❌ Forgetting to specify namespace  
→ RoleBinding automatically becomes namespace-scoped.

---

# 8. Frequently Asked Interview Questions

### Q1: Can RoleBinding bind a ClusterRole?  
✔ **Yes**, but permissions apply *only in the RoleBinding’s namespace*.

---

### Q2: Can ClusterRoleBinding bind a Role?  
❌ **No**, ClusterRoleBinding can bind only ClusterRoles.

---

### Q3: Which RBAC object is used to give namespace-level access?  
✔ **RoleBinding**

---

### Q4: Which RBAC object grants permissions cluster-wide?  
✔ **ClusterRoleBinding**

---

### Q5: Why does Kubernetes separate RoleBinding and ClusterRoleBinding?  
✔ To maintain strict namespace isolation  
✔ Prevent accidental cluster-wide privilege escalation  

---

# 9. Summary

| Concept | Explanation |
|--------|-------------|
| Role | Namespaced permission set |
| ClusterRole | Cluster/global permission set |
| RoleBinding | Grants Role/ClusterRole inside namespace |
| ClusterRoleBinding | Grants ClusterRole across entire cluster |

RBAC is essential for:
- Secure multi-team Kubernetes clusters  
- Least privilege access  
- Compliance & auditing  

---


# Kubernetes RBAC – Real-World Scenario Labs + Troubleshooting Guide

This document includes:
- Real-world RBAC scenarios with hands-on labs
- Expected outputs
- Common RBAC issues and troubleshooting steps

---

# 🧪 LAB 1 — Create a Read-Only Developer User (Namespace-Scoped)

## Objective  
Allow user **dev-user** to only *view* resources in namespace **dev**.

---

## Step 1 — Create Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: readonly
  namespace: dev
rules:
  - apiGroups: [""]
    resources: ["pods", "services", "configmaps"]
    verbs: ["get", "list", "watch"]
```

Apply:
```bash
kubectl apply -f readonly-role.yaml
```

---

## Step 2 — Bind Role to User

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: readonly-binding
  namespace: dev
subjects:
  - kind: User
    name: dev-user
roleRef:
  kind: Role
  name: readonly
  apiGroup: rbac.authorization.k8s.io
```

Apply:
```bash
kubectl apply -f readonly-binding.yaml
```

---

## Step 3 — Test Access

```bash
kubectl auth can-i delete pod --as dev-user -n dev
```

Expected:
```
no
```

Check read:
```bash
kubectl auth can-i get pod --as dev-user -n dev
```

Expected:
```
yes
```

---

# 🧪 LAB 2 — Allow CI/CD Pipeline to Deploy Apps

## Objective  
Allow ServiceAccount **cicd-sa** to manage Deployments but NOT Secrets.

---

## Step 1 — Create ServiceAccount

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: cicd-sa
  namespace: prod
```

---

## Step 2 — Create Role for Deployment Management

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: deploy-manager
  namespace: prod
rules:
  - apiGroups: ["apps"]
    resources: ["deployments"]
    verbs: ["create", "update", "patch", "get"]
```

---

## Step 3 — Bind Role to ServiceAccount

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: deploy-manager-binding
  namespace: prod
subjects:
  - kind: ServiceAccount
    name: cicd-sa
roleRef:
  kind: Role
  name: deploy-manager
  apiGroup: rbac.authorization.k8s.io
```

---

## Step 4 — Test Access

```bash
kubectl auth can-i create deployment --as system:serviceaccount:prod:cicd-sa -n prod
```

Expected:
```
yes
```

```bash
kubectl auth can-i get secret --as system:serviceaccount:prod:cicd-sa -n prod
```

Expected:
```
no
```

---

# 🧪 LAB 3 — Provide Cluster-Wide Read Access

## Objective  
Allow user **auditor** to view resources in ALL namespaces.

---

## Step 1 — Use Default `view` ClusterRole

Bind using ClusterRoleBinding:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: auditor-binding
subjects:
  - kind: User
    name: auditor
roleRef:
  kind: ClusterRole
  name: view
  apiGroup: rbac.authorization.k8s.io
```

---

## Step 2 — Test Access

```bash
kubectl auth can-i list pods --as auditor -A
```

Expected:
```
yes
```

---

# 🧪 LAB 4 — Grant Admin Access to Namespace Only

## Objective  
User **team-lead** should have full control of namespace `team`.

---

## Step 1 — Bind Admin Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: team-admin-binding
  namespace: team
subjects:
  - kind: User
    name: team-lead
roleRef:
  kind: ClusterRole
  name: admin
  apiGroup: rbac.authorization.k8s.io
```

---

## Step 2 — Test

```bash
kubectl auth can-i delete pod --as team-lead -n team
yes
kubectl auth can-i delete namespace team --as team-lead
no
```

**Admin role does NOT allow namespace deletion.**

---

# 🧪 LAB 5 — Allow Monitoring System to Read Metrics Across Cluster

## Objective  
Prometheus needs cluster-wide access to `/metrics` endpoints.

---

Bind built-in role:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: prometheus-read
subjects:
  - kind: ServiceAccount
    name: prometheus-sa
    namespace: monitoring
roleRef:
  kind: ClusterRole
  name: system:metrics-reader
  apiGroup: rbac.authorization.k8s.io
```

---

# 🚨 RBAC Troubleshooting Guide (Full)

## ❌ Problem 1 — “Forbidden” Error  
Example:
```
Error from server (Forbidden): pods is forbidden
```

### ✔ Fix
Run:
```bash
kubectl auth can-i get pods --as <user> -n <ns>
```

Possible causes:
- Missing RoleBinding  
- Wrong namespace  
- Wrong RoleRef (Role vs ClusterRole)  
- Subject name mismatch  

---

## ❌ Problem 2 — ServiceAccount cannot access API

### Cause:
Pod not using correct ServiceAccount.

### Fix:
Check Pod spec:
```bash
kubectl get pod mypod -o jsonpath='{.spec.serviceAccountName}'
```

---

## ❌ Problem 3 — RoleBinding does NOT work for cluster-wide permissions

RoleBinding is **namespace-scoped**.

### Fix:
Use ClusterRoleBinding:
```bash
kind: ClusterRoleBinding
```

---

## ❌ Problem 4 — ClusterRoleBinding referencing a Role (INVALID)

Only ClusterRoles can be used.

---

## ❌ Problem 5 — Wrong User or ServiceAccount Name

Check exact K8s subject name:
```bash
kubectl get sa -A
kubectl get clusterrolebinding -A
kubectl get rolebinding -A
```

---

## ❌ Problem 6 — RBAC not applied due to missing apiGroup

Correct:
```yaml
apiGroup: rbac.authorization.k8s.io
```

---

# 🔍 Useful Debugging Commands

### Check who can access a resource
```bash
kubectl auth who-can delete pods
```

### Check permissions of a user
```bash
kubectl auth can-i list deployments --as dev-user -n dev
```

### Describe RoleBinding
```bash
kubectl describe rolebinding -n dev
```

### View all RBAC objects
```bash
kubectl get roles,rolebindings,clusterroles,clusterrolebindings -A
```

---

# Summary

You learned:

### ✔ Real-world RBAC scenarios  
- Read-only Dev access  
- CI/CD Deployment access  
- Auditor read access  
- Namespace admin permissions  
- Monitoring access  

### ✔ Troubleshooting RBAC errors  
- Forbidden issues  
- Namespace mismatch  
- Wrong RoleBindings  
- Wrong subject types  
- Missing apiGroups  

RBAC is critical for multi-team, secure Kubernetes clusters.










