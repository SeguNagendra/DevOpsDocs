---
sidebar_position: 22
---


# Kubernetes Deployment Strategies

This document explains common Kubernetes deployment strategies with explanations, use cases, and examples.

---

## 1. Rolling Update

### Definition
Rolling Update is the **default Kubernetes deployment strategy** where Pods are replaced incrementally to ensure **application availability** during updates.

### Internal Working
- Kubernetes creates new Pods with the updated version
- Gradually terminates old Pods
- Managed by:
  - `maxSurge`: Extra Pods allowed during update
  - `maxUnavailable`: Pods allowed to be unavailable

### Why it works well
- Ensures **continuous service**
- Kubernetes Service load-balances traffic automatically

### Pros
✅ No downtime  
✅ Easy rollback  
✅ Production safe  

### Cons
❌ Old & new versions run simultaneously  
❌ Not suitable for breaking schema changes

### When to use
- Production workloads
- Stateless applications
- Most real-world use cases

### How it works
- Updates Pods incrementally
- Controlled by `maxSurge` and `maxUnavailable`

### Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rolling-app
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: rolling
  template:
    metadata:
      labels:
        app: rolling
    spec:
      containers:
      - name: app
        image: nginx:1.25
        ports:
        - containerPort: 80
```

---

## 2. Recreate Strategy

### Definition
Recreate strategy **stops all existing Pods first**, then starts Pods with the new version.

### Internal Working
- Kubernetes deletes all old Pods
- Once terminated, new Pods are created

### Why it is used
- Prevents running multiple versions together
- Avoids data or schema conflicts

### Pros
✅ Simple  
✅ No version conflict  

### Cons
❌ Application downtime  
❌ Not user-friendly

### When to use
- Applications that cannot run multiple versions
- Database schema changes
- Legacy applications


### Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: recreate-app
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: recreate
  template:
    metadata:
      labels:
        app: recreate
    spec:
      containers:
      - name: app
        image: nginx:1.25
```

---

## 3. Blue-Green Deployment

### Definition
Blue-Green deployment runs **two identical environments**:
- Blue → current production
- Green → new version

Only one receives live traffic.

### Internal Working
- Both versions run simultaneously
- Kubernetes Service selector switches traffic

### Why it works
- Instant traffic switch
- Immediate rollback

### Pros
✅ Zero downtime  
✅ Fast rollback  
✅ High confidence releases  

### Cons
❌ Requires double resources  
❌ Manual management unless automated

### When to use
- Zero downtime deployments
- Fast rollback

### Example
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
    version: green
  ports:
  - port: 80
    targetPort: 80
```

---

## 4. Canary Deployment

### Definition
Canary deployment releases a new version to a **small subset of users** first.

### Internal Working
- Two Deployments run (stable + canary)
- Traffic split based on replicas or Ingress rules
- Gradual traffic increase

### Why it is safe
- Limits exposure of failures
- Early detection of issues

### Pros
✅ Very low risk  
✅ Real production testing  
✅ Easy rollback  

### Cons
❌ Complex traffic management  
❌ Requires monitoring setup

### When to use
- Risky updates
- Behavior testing

### Real-world Use
- Performance-sensitive updates
- Critical apps

### Example
```yaml
# Stable version
replicas: 9
image: nginx:1.24

# Canary version
replicas: 1
image: nginx:1.25
```

---

## 5. A/B Deployment

### Definition
A/B deployment runs **multiple versions simultaneously** for **feature testing**, not version rollout.

### Internal Working
- Routes traffic based on:
  - Headers
  - Cookies
  - User groups

### Why it is used
- Compare features
- Measure user behavior

### Pros
✅ Product optimization  
✅ Data-driven decisions  

### Cons
❌ Not meant for app upgrades  
❌ Complex routing


### When to use
- UI/UX experiments
- Marketing experiments

### Example (Ingress Annotation)
```yaml
annotations:
  nginx.ingress.kubernetes.io/canary: "true"
  nginx.ingress.kubernetes.io/canary-weight: "50"
```

---

## Strategy Comparison

| Strategy | Downtime | Risk | Rollback | Complexity |
|--------|----------|------|----------|------------|
| Rolling Update | No | Low | Easy | Low |
| Recreate | Yes | High | Easy | Low |
| Blue-Green | No | Low | Instant | Medium |
| Canary | No | Very Low | Easy | High |
| A/B | No | Low | Easy | High |

---

## Summary
- Rolling Update is the safest default
- Recreate causes downtime but avoids version conflicts
- Blue-Green offers instant rollback
- Canary minimizes risk
- A/B is for feature testing, not releases
