---
sidebar_position: 14
---


# Kubernetes Autoscaling

This document explains Kubernetes autoscaling mechanisms in detail:

- **Horizontal Pod Autoscaler (HPA)**
- **Vertical Pod Autoscaler (VPA)**
- **Cluster Autoscaler**

Each topic includes clear explanations, real-world use cases, and YAML examples.

---

# 1. What Is Autoscaling in Kubernetes?

Autoscaling means Kubernetes can **automatically scale**:
- The **number of Pods**
- The **resources of Pods**
- The **number of Nodes in the cluster**

Autoscaling improves:
- Application performance
- Cost efficiency
- Resilience
- Resource utilization

---

# 2. Horizontal Pod Autoscaler (HPA)

HPA automatically scales the **number of Pod replicas** based on metrics such as:
- CPU utilization  
- Memory usage (if metrics server supports it)
- Custom metrics  
- External metrics  

### 🎯 When to Use HPA?
- Stateless applications  
- Web/API workloads  
- Applications with fluctuating traffic  

---

## 2.1 HPA Example (CPU-based Autoscaling)

### Step 1 — Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hpa-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hpa-app
  template:
    metadata:
      labels:
        app: hpa-app
    spec:
      containers:
        - name: app
          image: nginx
          resources:
            requests:
              cpu: 200m
```

### Step 2 — Create HPA
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hpa-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```

Meaning:
- If average CPU > 50% → Scale UP  
- When CPU < threshold → Scale DOWN  

### Check HPA Behavior
```bash
kubectl get hpa
```

---

## 2.2 Load Testing HPA

```bash
kubectl run load --image=busybox -- sh -c "while true; do wget -q -O- http://hpa-app; done"
```

HPA will increase replicas dynamically.

---

# 3. Vertical Pod Autoscaler (VPA)

VPA automatically adjusts **CPU & memory Requests/Limits** of containers.

VPA helps when:
- Workloads require more/less resources over time  
- You want accurate sizing  
- You don’t want to guess resource values  

---

## 3.1 VPA Modes

| Mode | Behavior |
|------|----------|
| **Off** | Only recommend resources |
| **Initial** | Apply recommendations at Pod creation |
| **Auto** | Evicts Pods and applies recommendations dynamically |

---

## 3.2 VPA Example

### VPA Resource
```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: vpa-demo
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hpa-app
  updatePolicy:
    updateMode: "Auto"
```

Meaning:
- VPA monitors Pod usage  
- Suggests or applies better CPU/memory settings  
- If `Auto`, it can evict Pods to resize them  

---

## 3.3 When to Use VPA?

- Batch jobs  
- ML workloads  
- Long-running backend systems  
- When CPU/memory patterns vary over time  

---

## 3.4 When NOT to Use VPA?

❌ Do NOT use VPA + HPA CPU mode together  
They will fight each other:
- VPA changes CPU requests  
- HPA calculates based on CPU requests  

You *can* combine:
- VPA (memory)
- HPA (CPU)

This is a recommended hybrid approach.

---

# 4. Cluster Autoscaler

Cluster Autoscaler automatically adds or removes **nodes** based on pending Pods.

### 🎯 When Cluster Autoscaler Adds Nodes
- A Pod cannot be scheduled  
- No node has enough free CPU/memory  
- NodeAffinity / Taints prevent scheduling

---

### 🎯 When Cluster Autoscaler Removes Nodes
- A node is underutilized  
- All Pods on it can be safely moved elsewhere  

---

## 4.1 How Cluster Autoscaler Works

1. Checks if any Pods are unschedulable  
2. Calculates if adding a new node helps  
3. Requests cloud provider to launch a node  
4. Schedules Pods on new node  
5. Watches node utilization  
6. Removes empty nodes  

Supported Clouds:
- AWS (ASG)  
- GCP (GKE)  
- Azure AKS  
- Cluster API  
- Karpenter (replacement for CA in EKS)  

---

# 5. Cluster Autoscaler Example (Conceptual)

### Node Group Config (AWS ASG / GKE Node Pool)
```
minSize: 2
maxSize: 10
desiredSize: 3
```

### Cluster Autoscaler Deployment Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cluster-autoscaler
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app: cluster-autoscaler
  template:
    metadata:
      labels:
        app: cluster-autoscaler
    spec:
      containers:
        - image: k8s.gcr.io/autoscaling/cluster-autoscaler:v1.27
          name: cluster-autoscaler
          command:
            - ./cluster-autoscaler
            - --cloud-provider=aws
            - --nodes=2:10:nodegroup-name
          resources:
            limits:
              cpu: 100m
              memory: 300Mi
```

Cluster Autoscaler dynamically manages node count.

---

# 6. Differences Between Autoscalers

| Feature | HPA | VPA | Cluster Autoscaler |
|--------|-----|-----|---------------------|
| What it scales | Pod replicas | Pod resources | Nodes |
| Uses metrics | CPU, memory, custom | Usage history | Pending Pods / Node usage |
| Reactivity | Fast | Medium | Slow |
| Best for | Web apps | Batch/ML workloads | Infrastructure scaling |
| Works with | Deployments, ReplicaSets | Deployments, StatefulSets | Node groups |

---

# 7. Real-World Autoscaling Architectures

---

## 🟢 Common Setup (Recommended)
- **HPA** → scales Pods based on traffic  
- **Cluster Autoscaler** → ensures enough nodes exist  

Architecture:
```
Traffic ↑ → Pods ↑ (HPA)
If no node capacity → Nodes ↑ (Cluster Autoscaler)
```

---

## 🟠 For ML / Batch systems
- **VPA** → adjusts Pod CPU/memory  
- **Cluster Autoscaler** → adds nodes  
- Usually no HPA needed  

---

## 🔵 Hybrid (Advanced)
- HPA scales Pods based on CPU  
- VPA scales memory only  
- Cluster Autoscaler scales node count  

---

# 8. Summary

| Autoscaler | Purpose | Key Benefit |
|------------|----------|--------------|
| **HPA** | Scale Pods horizontally | Handle traffic spikes |
| **VPA** | Adjust CPU/memory for Pods | Right-size workloads |
| **Cluster Autoscaler** | Scale nodes | Add capacity when needed |

Autoscaling ensures Kubernetes is:
- Efficient  
- Cost-optimized  
- Resilient  
- Self-healing  




