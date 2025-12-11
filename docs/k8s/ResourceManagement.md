---
sidebar_position: 19
---

# Kubernetes Resource Management 
Includes:  
- CPU & Memory Management  
- QoS Classes  
- Eviction Policies  
- Hands‑on Labs  
  - RBAC Creation for Users  
  - NetworkPolicy Implementation  
  - Monitoring with Prometheus + Grafana  

---

# 1. CPU & Memory Management in Kubernetes

Kubernetes ensures fair resource usage using **Requests**, **Limits**, and **cgroups**.

## 1.1 CPU Management
CPU is *compressible* → if a container exceeds CPU limit, it is **throttled**, not killed.

### CPU Requests
- Minimum guaranteed CPU  
- Used by scheduler to place Pods  

Example:
```yaml
resources:
  requests:
    cpu: "200m"      # 0.2 cores
```

### CPU Limits
- Maximum CPU allowed  
- Exceeding limit causes throttling  

Example:
```yaml
limits:
  cpu: "500m"        # 0.5 cores
```

---

## 1.2 Memory Management
Memory is *not compressible*.  
If a Pod exceeds memory **limit** → **OOMKilled**.

### Memory Request
- Minimum memory needed for stable scheduling  

### Memory Limit
- Maximum memory  
- Exceed → container killed  

Example:
```yaml
resources:
  requests:
    memory: "256Mi"
  limits:
    memory: "512Mi"
```

---

# 2. QoS Classes (Quality of Service)

Kubernetes assigns each Pod a QoS class based on its resource configuration.

| QoS Class | Condition | Behavior |
|-----------|-----------|----------|
| **Guaranteed** | CPU & memory requests == limits for all containers | Best protection from eviction |
| **Burstable** | Requests < limits or only partial resource set | Medium eviction priority |
| **BestEffort** | No requests or limits set | First to be evicted |

### Example Guaranteed Pod
```yaml
resources:
  requests:
    cpu: "500m"
    memory: "512Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

---

# 3. Eviction Policies

Nodes evict Pods when resources become scarce.

## 3.1 Reasons for Eviction
- Memory pressure  
- Disk pressure  
- Node conditions degraded  
- OOM  

Run:
```bash
kubectl describe node <node>
```

---

## 3.2 Eviction Priority Order

1. BestEffort Pods  
2. Burstable Pods  
3. Guaranteed Pods (last resort)  

---

## 3.3 Soft & Hard Eviction Thresholds

Example from node config:
```
--eviction-hard=memory.available<500Mi
--eviction-soft=memory.available<1Gi
```

---

# 4. HANDS‑ON LAB 1: RBAC Creation for Users

## Step 1 — Create a Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: dev-reader
  namespace: dev
rules:
  - apiGroups: [""]
    resources: ["pods", "services"]
    verbs: ["get", "list", "watch"]
```

---

## Step 2 — Bind the Role to a User

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-reader-binding
  namespace: dev
subjects:
  - kind: User
    name: devuser
roleRef:
  kind: Role
  name: dev-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## Expected Output
```bash
kubectl auth can-i get pods --as devuser -n dev
yes
```

---

# 5. HANDS‑ON LAB 2: NetworkPolicy Implementation

## Step 1 — Default Deny Policy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
  namespace: demo
spec:
  podSelector: {}
  policyTypes:
    - Ingress
```

---

## Step 2 — Allow Only Frontend → Backend

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
  namespace: demo
spec:
  podSelector:
    matchLabels:
      app: backend
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
```

---

## Expected Behavior
```
frontend → backend : ALLOWED
any other pod → backend : BLOCKED
```

---

# 6. HANDS‑ON LAB 3: Monitor Cluster With Prometheus + Grafana

## Step 1 — Install Prometheus

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prom prometheus-community/prometheus
```

---

## Step 2 — Install Grafana

```bash
helm install graf grafana/grafana
```

---

## Step 3 — Port Forward UI

Prometheus:
```bash
kubectl port-forward svc/prom-prometheus-server 9090:80
```

Grafana:
```bash
kubectl port-forward svc/graf-grafana 3000:80
```

---

## Step 4 — Add Prometheus as Grafana Data Source  
URL:
```
http://prom-prometheus-server
```

---

## Step 5 — Import Dashboards

Recommended IDs:
- **315** – Nginx metrics  
- **6417** – Kubernetes cluster monitoring  
- **8588** – Node Exporter Full  

---

## Step 6 — Validate Metrics

Run:
```bash
kubectl top nodes
kubectl top pods
```

PromQL example:
```
rate(container_cpu_usage_seconds_total[5m])
```

Expected dashboard:
- CPU usage graphs  
- Memory trends  
- Pod restarts  
- Node health  

---

# Summary

### Kubernetes Resource Management Includes:
- CPU/Memory requests & limits  
- QoS classes  
- Eviction policies  

### Hands‑on Covered:
- RBAC role creation for users  
- NetworkPolicy (deny-all + allow frontend)  
- Monitoring cluster with Prometheus + Grafana  

A proper resource management & observability strategy ensures:
- Stability  
- Performance  
- Security  
- Cost‑efficient cluster operations  

---



