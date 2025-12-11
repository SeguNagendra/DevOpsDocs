---
sidebar_position: 13
---

# K8s Scheduling, Requests & Limits
This document provides detailed explanations and YAML examples for:

- **NodeSelector**
- **NodeAffinity**
- **PodAffinity / PodAntiAffinity**
- **Taints & Tolerations**
- **Resource Requests & Limits**

---

# 1. Introduction to Kubernetes Scheduling

Kubernetes scheduler decides **which node** a Pod should run on by evaluating:

- Node resource availability  
- Labels and affinity rules  
- Taints & tolerations  
- Pod resource requests  
- Node readiness  

The Scheduler’s goal is to place Pods on the “best-fit” node while respecting **constraints** defined by users and cluster policies.

---

# 2. NodeSelector (Basic Scheduling Constraint)

`nodeSelector` is the simplest way to force a Pod to run on nodes that have specific labels.

### Step 1 — Label a Node
```bash
kubectl label node worker-1 disk=ssd
```

### Step 2 — Pod with NodeSelector
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: node-selector-pod
spec:
  nodeSelector:
    disk: ssd
  containers:
    - name: app
      image: nginx
```

### Behavior
The Pod will run **only** on nodes where:
```
disk=ssd
```

---

# 3. NodeAffinity (Advanced Node Selection)

NodeAffinity is a flexible version of nodeSelector.

Two main types:

### 1️⃣ **requiredDuringSchedulingIgnoredDuringExecution**
- Hard requirement
- Scheduler must follow these rules

### 2️⃣ **preferredDuringSchedulingIgnoredDuringExecution**
- Soft preference
- Scheduler chooses the best option if possible

---

## 3.1 Hard NodeAffinity Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hard-affinity-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: disk
                operator: In
                values:
                  - ssd
  containers:
    - name: app
      image: nginx
```

Pod **must** run on nodes with `disk=ssd`.

---

## 3.2 Soft NodeAffinity Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: soft-affinity-pod
spec:
  affinity:
    nodeAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
        - weight: 80
          preference:
            matchExpressions:
              - key: region
                operator: In
                values:
                  - us-east
  containers:
    - name: app
      image: nginx
```

Scheduler *tries* to place the Pod in `region=us-east`, but will fallback if needed.

---

# 4. PodAffinity & PodAntiAffinity

Pod affinity controls Pod placement based on **other Pods**.

---

## 4.1 PodAffinity (Stay together)

Used when Pods need to run **on the same node/zone** for:
- High performance
- Data locality

Example:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-affinity
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchLabels:
              app: backend
          topologyKey: "kubernetes.io/hostname"
  containers:
    - name: app
      image: nginx
```

Meaning:
- This Pod must run on a node where another Pod with label `app=backend` exists.

---

## 4.2 PodAntiAffinity (Stay apart)

Used when Pods must avoid co-location for:
- High availability  
- Spreading across nodes/zones  

Example:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-antiaffinity
spec:
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        - labelSelector:
            matchLabels:
              app: api
          topologyKey: "kubernetes.io/hostname"
  containers:
    - name: app
      image: nginx
```

Meaning:
- No two Pods with label `app=api` should run on the same node.

---

# 5. Taints & Tolerations

Taints prevent Pods from being scheduled on specific nodes unless they tolerate the taint.

---

## 5.1 Taint a Node
```bash
kubectl taint nodes worker-2 env=prod:NoSchedule
```

This means:
- No Pod can run on `worker-2` unless it tolerates the taint.

---

## 5.2 Pod with Toleration
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: toleration-pod
spec:
  tolerations:
    - key: "env"
      operator: "Equal"
      value: "prod"
      effect: "NoSchedule"
  containers:
    - name: app
      image: nginx
```

Now Pod **is allowed** to run on tainted node `worker-2`.

---

## 5.3 Types of Effects

| Effect | Meaning |
|--------|---------|
| **NoSchedule** | Pod will not be scheduled unless it tolerates the taint |
| **PreferNoSchedule** | Scheduler *tries* to avoid the node |
| **NoExecute** | Existing Pods without toleration are evicted |

---

# 6. Resource Requests & Limits

Requests and limits control **Pod resource allocation** on nodes.

---

## 6.1 Resource Requests
The *minimum* amount of CPU/memory a Pod needs.

Scheduler uses these values to decide on Pod placement.

---

## 6.2 Resource Limits
The *maximum* amount of CPU/memory a Pod is allowed to use.

If a container exceeds limits:
- CPU: throttled  
- Memory: container **OOMKilled**

---

## Example: Pod with Requests & Limits
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
    - name: app
      image: nginx
      resources:
        requests:
          cpu: "200m"
          memory: "256Mi"
        limits:
          cpu: "500m"
          memory: "512Mi"
```

Meaning:
- Scheduler needs a node with at least **200m CPU** & **256Mi memory**
- Pod cannot exceed **500m CPU** & **512Mi memory**

---

# 7. How Scheduling Works Together (Real-World Scenario)

Example:
- NodeSelector → restrict nodes  
- NodeAffinity → soft/hard preferences  
- PodAntiAffinity → spread Pods  
- Taints → block nodes  
- Tolerations → allow exceptions  
- Requests → ensure capacity  

All rules apply **together**.

---

# 8. Summary

| Feature | Purpose |
|---------|---------|
| NodeSelector | Simple exact-match scheduling |
| NodeAffinity | Advanced matching using expressions |
| PodAffinity | Co-locate Pods together |
| PodAntiAffinity | Spread Pods across nodes |
| Taints | Block nodes |
| Tolerations | Allow Pods on tainted nodes |
| Requests | Scheduler uses for placement |
| Limits | Runtime enforcement |

---


# Why Resource Requests & Limits Are Important in Kubernetes  
### What Happens If You Don't Set Them? (Deep Explanation + Examples)

Resource **Requests** and **Limits** are core to how Kubernetes schedules Pods, protects nodes, and ensures application stability.  
This document explains **why they are important**, **what problems they prevent**, and **what happens if you don’t set them**, with clear examples.

---

# 1. What Are Resource Requests?

`requests` = Minimum amount of **CPU** and **memory** a Pod needs to run.

Kubernetes **scheduler uses requests** to decide:
- Which node has enough free resources?
- Can the node host this Pod without overload?

Example:
```yaml
resources:
  requests:
    cpu: "200m"
    memory: "256Mi"
```

Meaning:  
This container needs **0.2 CPU** and **256Mi memory** at minimum.

---

# 2. What Are Resource Limits?

`limits` = Maximum amount of CPU/memory a Pod may use.

Limits protect the node from overloaded containers.

Example:
```yaml
limits:
  cpu: "500m"
  memory: "512Mi"
```

---

# 3. What Happens If You DO NOT Set Requests?

## 🔥 (A) Scheduler places Pods randomly  
Without resource requests, the scheduler **assumes the Pod needs 0 CPU & 0 memory**.  
So:
- Heavy Pods may get scheduled onto already busy nodes  
- Nodes get overloaded  
- Random performance issues occur

---

## 🔥 (B) Risk of Node Overload  
Pods may land on a low-resource node and consume more than available, causing:

- Slowdown of all Pods
- Kernel OOM kills
- Node becoming NotReady

---

## 🔥 (C) Critical workloads may be starved  
Database / backend services may not get enough CPU or memory because "no reservations" exist.

Imagine:
- Logging agent consumes too much CPU  
- Your main API Pod slows down  

---

# 4. What Happens If You DO NOT Set Limits?

## 🔥 (A) Pod can consume **unlimited CPU**
CPU bursting may:
- Slow down other critical Pods  
- Saturate the node  
- Impact latency-sensitive apps  

Kubernetes **throttles only when limits exist**.

---

## 🔥 (B) Pod can consume **unlimited memory** → Node OOM  
Memory is NOT compressible.  
If a container tries to use more memory than the node has:

- The **kernel OOM killer** terminates Pods
- Often it kills random Pods (not always your culprit!)
- Node becomes unstable

Symptoms:
```
OOMKilled
CrashLoopBackOff
Node pressure conditions
```

---

## 🔥 (C) No resource isolation → No multitenancy  
In multi-team clusters:
- One faulty Pod can consume all node resources
- Other team Pods crash

This violates Kubernetes' goal of fairness.

---

# 5. Combined Risks When Neither Requests nor Limits Are Set

| Problem | Explanation |
|--------|-------------|
| Unpredictable Pod scheduling | Scheduler assumes 0 resource need |
| Node overload | Too many Pods placed on same node |
| OOM kills | No memory limits to protect node |
| CPU starvation | Misbehaving Pods slow down cluster |
| Critical apps fail | No guaranteed resources |
| Multi-tenancy becomes unsafe | One team can crash entire node |
| Hard to debug performance | No predictable resource usage |

---

# 6. Example: Pod Without Requests & Limits

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: no-limits
spec:
  containers:
    - name: app
      image: nginx
```

### Risks:
- Scheduler spreads Pods arbitrarily  
- Pod can consume entire node CPU  
- If memory usage spikes → Pod is **OOMKilled**  
- May impact other Pods running on the same node  

---

# 7. Example: Proper Resource Settings

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: with-limits
spec:
  containers:
    - name: app
      image: nginx
      resources:
        requests:
          cpu: "200m"
          memory: "256Mi"
        limits:
          cpu: "500m"
          memory: "512Mi"
```

### Benefits:
- Scheduler places Pod correctly  
- Pod guaranteed minimum resources  
- Pod prevented from consuming more than 0.5 CPU or 512Mi memory  
- Node protected from overload  
- Stable and predictable performance  

---

# 8. Real-World Situations Requiring Requests & Limits

### 🟢 Production microservices  
Avoid CPU starvation and unexpected crashes.

### 🟢 Multi-tenant clusters  
Protect different teams from each other.

### 🟢 Databases / Stateful workloads  
Need guaranteed resources.

### 🟢 Auto-scaling (HPA)  
HPA uses **CPU requests** to calculate scaling thresholds.

If no requests → HPA scaling will **not work correctly**.

---

# 9. Summary (Interview-Ready)

### Why resource requests are important:
- Scheduler uses them to place Pods correctly  
- Guarantees minimum CPU & memory  
- Prevents node overload  

### Why limits are important:
- Protects node from excessive CPU/memory usage  
- Prevents OOM kill storms  
- Ensures stability in shared environments  

### What happens if you don’t set them?
- Nodes get overloaded  
- Pods get OOMKilled  
- Unpredictable performance  
- Fairness breaks in multi-tenant setups  
- Auto-scaling becomes inaccurate  

Setting **requests & limits** is one of the most important best practices in Kubernetes.

---



