---
sidebar_position: 3
---

# Kubernetes Architecture 

This document provides **expanded and detailed explanations** of Kubernetes internal components,
their responsibilities, how they work together, and key foundational definitions.


---

## 1.1 Control Plane Components (Detailed)

The **Control Plane** is the brain of the Kubernetes cluster.
It makes **global decisions** and continuously ensures the cluster runs in the desired state.

---

### ✅ API Server

The **API Server** is the **central communication hub** of Kubernetes.

#### What it does
- Acts as the **entry point** to the Kubernetes cluster
- Exposes Kubernetes APIs via REST
- Handles **all read and write operations**
- Authenticates and authorizes requests

#### How it works internally
- Receives requests from:
  - kubectl
  - CI/CD tools
  - Controllers
  - kubelets
- Validates:
  - Authentication (who you are)
  - Authorization (what you can do)
  - Resource schema (YAML correctness)
- Stores accepted requests in etcd

#### Key takeaway
> Nothing happens in Kubernetes without going through the API Server.

---

### ✅ etcd

**etcd** is a **distributed, consistent key-value store**.

#### What it stores
- Entire cluster state:
  - Pods
  - Deployments
  - Services
  - ConfigMaps
  - Secrets
  - Node information

#### Why etcd is critical
- Acts as the **single source of truth**
- Supports high availability via replication
- Guarantees consistency using the Raft consensus algorithm

#### Important note
- If etcd is lost → cluster state is lost
- Regular backups are critical in production

---

### ✅ Scheduler

The **Scheduler** is responsible for **Pod placement**.

#### What it does
- Picks the best node for newly created Pods
- Does NOT run Pods itself

#### Decision factors
- CPU & memory availability
- Pod resource requests
- Node affinity / anti-affinity rules
- Taints and tolerations
- Pod priority

#### Scheduler Flow
1. Filters nodes that cannot run the Pod
2. Scores remaining nodes
3. Chooses the best-scoring node

---

### ✅ Controller Manager

The **Controller Manager** runs multiple controllers.

#### What is a controller?
A controller is a **watch-and-reconcile loop** that ensures desired state = actual state.

#### Examples
- ReplicaSet Controller → ensures correct Pod count
- Node Controller → monitors node health
- Endpoint Controller → maintains service endpoints

#### How controllers work
1. Watch cluster state via API Server
2. Detect differences
3. Take corrective action automatically

---

## 1.2 Worker Node Components (Detailed)

Worker Nodes are where **actual applications run**.

---

### ✅ kubelet

kubelet is the **node-level agent**.

#### Responsibilities
- Registers the node with the cluster
- Watches Pod manifests assigned to the node
- Communicates with container runtime
- Reports node and Pod status back to API Server

#### Key point
> kubelet ensures containers described in Pod specs are running and healthy.

---

### ✅ Container Runtime

The **Container Runtime** is responsible for running containers.

#### What it does
- Pulls container images
- Starts and stops containers
- Manages container lifecycle

#### Supported runtimes
- containerd (most common)
- CRI-O

#### Communication
- kubelet talks to the runtime using **CRI (Container Runtime Interface)**

---

### ✅ kube-proxy

kube-proxy manages **networking and load balancing**.

#### Responsibilities
- Implements Kubernetes Services
- Routes traffic to correct Pods
- Maintains iptables/IPVS rules

#### What it enables
- Pod-to-pod communication
- Service-to-pod load balancing
- Stable Service IPs and DNS names

---

## 2. Kubernetes Workflow (End-to-End – Detailed)

This explains what happens when you apply a YAML file.

### Step-by-step Flow
1. User runs `kubectl apply -f app.yaml`
2. API Server authenticates and validates the request
3. Desired state is stored in etcd
4. Scheduler selects the suitable worker node
5. kubelet receives Pod assignment
6. Container runtime pulls image and runs containers
7. Controllers continuously monitor and take corrective action

---

### Workflow Diagram

```
kubectl
   |
   v
API Server  --->  etcd (store desired state)
   |
   v
Scheduler ---> chooses node
   |
   v
kubelet ---> container runtime ---> running containers
```

---

## 3. Key Definitions (Extended)

### ✅ Cluster
A Kubernetes cluster is a **collection of control plane and worker nodes**
that work together to run containerized applications.

---

### ✅ Node
A node is a **machine (VM or physical)** that runs application workloads.
Each node runs kubelet, kube-proxy, and a container runtime.

---

### ✅ Pod
A pod is the **smallest deployable unit in Kubernetes**.
It can contain:
- One container (most common)
- Multiple tightly-coupled containers

---

### ✅ Desired State
The desired state is **what the user defines** using YAML manifests.
Example:
```yaml
replicas: 3
```

---

### ✅ Actual State
The actual state is **what is currently running** in the cluster.

---

### ✅ Reconciliation Loop
Kubernetes continuously compares:
- Desired State
- Actual State

If they differ, Kubernetes **automatically fixes the system**.

---

### ✅ Declarative Model
In the declarative model:
- You describe *what* you want
- Kubernetes decides *how* to achieve it

There is no need to manage steps manually.

---

## 4. Summary

- The Control Plane manages the cluster
- Worker Nodes run applications
- API Server is the single entry point
- etcd stores cluster state
- Scheduler decides Pod placement
- Controllers enforce desired state
- kubelet and container runtime run containers
- kube-proxy enables networking
- Kubernetes continuously self-heals and reconciles

