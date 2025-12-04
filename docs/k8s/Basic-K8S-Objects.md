---
sidebar_position: 4
---

# Basic Kubernetes Objects

---

## 1. Pod

### What is a Pod?
A **Pod** is the **smallest deployable unit** in Kubernetes.
It represents **one or more containers** that:
- Share the same network IP
- Share storage volumes
- Are scheduled together on the same node

> In most real-world cases, a Pod contains **one container**.

---

### Basic Pod YAML
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:1.25
      ports:
        - containerPort: 80
```

### Create Pod
```bash
kubectl apply -f pod.yaml
kubectl get pods
```

---

## 2. ReplicationController (Legacy Object)

### What is a ReplicationController?
A **ReplicationController (RC)** ensures that a **specified number of Pod replicas** are always running.

⚠️ Note:
- ReplicationController is **deprecated**
- It is replaced by **ReplicaSet**

### Key Responsibilities
- Maintains a fixed number of Pods
- Recreates Pods if they fail or are deleted
- Uses **equality-based selectors**

### Limitations
- Cannot handle advanced selectors
- No rolling updates
- No rollback support
- Not scalable for modern workloads

### When to use?
✅ Only for **legacy understanding**  
❌ Not recommended for new deployments


---

### Basic ReplicationController YAML
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-rc
spec:
  replicas: 2
  selector:
    app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

---

## 3. ReplicaSet

### What is a ReplicaSet?
A **ReplicaSet** ensures that a **desired number of identical Pods** are always running.

✅ Automatically replaces failed Pods  
✅ Supports **label selectors**  
❌ Does not manage rolling updates by itself


### Improvements Over ReplicationController
- Supports **set-based label selectors**
- Better pod selection flexibility
- More robust than RC

### Key Responsibilities
- Maintains desired Pod replica count
- Automatically replaces failed Pods

### Limitations
- Does NOT support rolling updates or rollbacks
- Rarely created directly by users

### When to use?
✅ Managed automatically by Deployments  
❌ Not used directly in most cases

- Note : In replicaset container block is 


---

### Basic ReplicaSet YAML
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rs
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-rs
  template:
    metadata:
      labels:
        app: nginx-rs
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

---

## 4. Deployment (Most Used)

### What is a Deployment?
A **Deployment** is a **higher-level controller** that manages ReplicaSets and Pods.

It provides:
- Rolling updates
- Rollbacks
- Scaling
- Declarative updates

✅ Recommended way to deploy applications

---

### Basic Deployment YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-deploy
  template:
    metadata:
      labels:
        app: nginx-deploy
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

### Scale Deployment
```bash
kubectl scale deployment nginx-deployment --replicas=4
```

---

## 5. Namespace

### What is a Namespace?
A **Namespace** is a **logical isolation mechanism** in Kubernetes.

It is used for:
- Environment separation (dev, qa, prod)
- Resource organization
- Access control (RBAC)

---

### Basic Namespace YAML
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

### Use Namespace
```bash
kubectl apply -f namespace.yaml
kubectl get ns
```

---

## 6. Service

### What is a Service?
A **Service** provides:
- Stable IP address
- DNS name
- Load balancing
- Pod discovery

Services expose Pods using **labels**.

---

## 6.1 ClusterIP Service (Default)

### When to use
- Internal communication within the cluster
- Backend services

### YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-clusterip
spec:
  type: ClusterIP
  selector:
    app: nginx-deploy
  ports:
    - port: 80
      targetPort: 80
```

---

## 6.2 NodePort Service

### When to use
- External access without cloud load balancer
- Testing and labs

### YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  selector:
    app: nginx-deploy
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

### Access
```text
http://<NodeIP>:30007
```

---

## 6.3 LoadBalancer Service

### When to use
- Cloud environments (AWS, Azure, GCP)
- Production external traffic

### YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-loadbalancer
spec:
  type: LoadBalancer
  selector:
    app: nginx-deploy
  ports:
    - port: 80
      targetPort: 80
```

---

## 7. Object Comparison (Quick View)

| Object | Purpose |
|------|--------|
| Pod | Runs containers |
| ReplicationController | Legacy pod replica manager |
| ReplicaSet | Ensures pod replicas |
| Deployment | Manages ReplicaSets & Pods |
| Namespace | Logical isolation |
| Service | Exposes Pods |


| Feature | ReplicationController | ReplicaSet | Deployment |
|------|----------------------|-----------|------------|
| Kubernetes status | Deprecated | Active | Active (Recommended) |
| Manages Pods | Yes | Yes | Yes (via ReplicaSet) |
| Rolling updates | ❌ No | ❌ No | ✅ Yes |
| Rollbacks | ❌ No | ❌ No | ✅ Yes |
| Auto scaling | ❌ Limited | ✅ Yes | ✅ Yes |
| Selector types | Equality-based | Set-based | Set-based |
| Direct usage | ❌ No | ❌ Rare | ✅ Yes |
| Production use | ❌ No | ❌ Indirect | ✅ Yes |
---

## 8. Best Practices

✅ Use Deployments instead of Pods directly  
✅ Avoid ReplicationController in new setups  
✅ Use Namespaces for environments  
✅ Use Services for Pod access  
✅ Label everything properly  

---

## 9. Summary

- Pods run containers
- ReplicaSets manage Pods
- Deployments manage ReplicaSets
- Namespaces isolate resources
- Services provide networking and load balancing


# Why Do We Use Deployment Instead of ReplicaSet?

This document explains **why Kubernetes Deployments are preferred over ReplicaSets**,
from a **real-world production**, **DevOps**, and **interview perspective**.

---

## 1. Understanding the Basics

### ReplicaSet
A **ReplicaSet** ensures that a specified number of **Pod replicas** are running at all times.

Its core responsibility is:
> Maintain Pod count

Nothing more.

---

### Deployment
A **Deployment** is a **higher-level Kubernetes object** that:
- Manages ReplicaSets
- Manages Pods
- Adds deployment-level features needed for production

> Deployment uses ReplicaSet internally but provides much more functionality.

---

## 2. Limitations of ReplicaSet

A ReplicaSet can:
✅ Create Pods  
✅ Replace failed Pods  

But it **cannot**:

❌ Perform rolling updates  
❌ Roll back to a previous version  
❌ Maintain version history  
❌ Support deployment strategies  
❌ Integrate safely with CI/CD  

📌 ReplicaSet only manages **quantity**, not **application lifecycle**.

---

## 3. What Deployment Adds on Top of ReplicaSet

Deployment provides everything ReplicaSet does **plus**:

✅ Rolling updates (zero or minimal downtime)  
✅ Rollback to previous versions  
✅ Deployment strategies  
✅ Controlled upgrades  
✅ Declarative lifecycle management  
✅ CI/CD friendliness  

---

## 4. Real-World Example

### Scenario: Update Application from v1 to v2

#### Using ReplicaSet
- Delete old Pods manually
- Create a new ReplicaSet
- Risk downtime
- No easy rollback

❌ High risk, manual, error-prone

---

#### Using Deployment
- Change image version in YAML
- Apply the manifest

Kubernetes automatically:
✅ Creates a new ReplicaSet  
✅ Gradually starts new Pods  
✅ Gradually removes old Pods  
✅ Monitors health  
✅ Allows rollback if needed  

✅ Safe and automated

---

## 5. Versioning and Rollback (Critical Difference)

### ReplicaSet
❌ No revision history  
❌ No rollback  

### Deployment
✅ Stores revision history  
✅ Supports rollback instantly  

```bash
kubectl rollout undo deployment my-app
```

This feature alone makes Deployment superior.

---

## 6. Deployment Strategies

Deployment supports advanced strategies:

| Strategy | Deployment |
|--------|------------|
| Rolling Update | ✅ Yes |
| Recreate | ✅ Yes |
| Canary | ✅ Yes |
| Blue-Green | ✅ Yes |

ReplicaSet:
❌ Supports none of these

---

## 7. CI/CD and Production Readiness

Modern production environments require:
- Frequent deployments
- Safe upgrades
- Instant rollback
- No downtime

CI/CD tools expect:
✅ Rolling updates  
✅ Rollback capability  

➡️ All provided by Deployments.

---

## 8. Kubernetes Best Practice

> **ReplicaSets are not meant to be used directly.**  
> They are designed to be **managed by Deployments**.

---

## 9. Comparison Summary

| Feature | ReplicaSet | Deployment |
|------|-----------|------------|
| Ensures pod count | ✅ | ✅ |
| Rolling updates | ❌ | ✅ |
| Rollback | ❌ | ✅ |
| Version history | ❌ | ✅ |
| Deployment strategies | ❌ | ✅ |
| Production ready | ❌ | ✅ |

---

## 10. Interview-Ready Answer

✅ **Why do we use Deployment instead of ReplicaSet?**

> Deployment provides rolling updates, rollback, version control, and safe application lifecycle management, while ReplicaSet only ensures pod count.

---

## 11. Final One-Liner

> **ReplicaSet keeps Pods running; Deployment safely releases applications.**




