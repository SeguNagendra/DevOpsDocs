---
sidebar_position: 21
---

# K8s High Availability (HA) 
Covers:  
- HA Control Plane  
- Multi-Master Setup  
- Load Balancer for API Server  
- etcd High Availability  

This document explains production-grade HA cluster architecture with clear diagrams and example configurations.

---

# 1. What Is High Availability in Kubernetes?

High Availability (HA) ensures the cluster continues operating even when one or more components fail.  
HA requires redundancy for:

- Control Plane  
- etcd  
- Networking  
- Load Balancing  

A production HA cluster should survive:

- Master node failure  
- etcd node failure  
- Load balancer failure  

---

# 2. HA Control Plane (High Availability Control Plane)

The Kubernetes Control Plane consists of:

- kube-apiserver  
- kube-controller-manager  
- kube-scheduler  
- etcd  

In HA mode:

- **Multiple API servers** run across several master nodes  
- Controller-manager & scheduler run in “active/passive” mode (leader election)  
- All masters point to a single virtual API endpoint (load balancer)

---

## 2.1 HA Control Plane Diagram

```
                +------------------------+
                |    External Load Balancer|
                |  VIP: https://k8s-api:6443|
                +-----------+------------+
                            |
        +-------------------+-------------------+
        |                   |                   |
+---------------+   +---------------+   +---------------+
| Master-1      |   | Master-2      |   | Master-3      |
| kube-apiserver|   | kube-apiserver|   | kube-apiserver|
| controller-mgr|   | controller-mgr|   | controller-mgr|
| scheduler     |   | scheduler     |   | scheduler     |
| etcd member   |   | etcd member   |   | etcd member   |
+---------------+   +---------------+   +---------------+
                            |
                        Worker Nodes
```

---

# 3. Multi-Master Setup

A multi-master cluster typically has **three control-plane nodes** for quorum safety.

### Why 3 Nodes?
- etcd uses RAFT consensus
- Needs majority vote (quorum) to function
- 3 nodes allow 1 to fail  
- 5 nodes allow 2 to fail, etc.

### Multi-master requirements:
- Shared Load Balancer for API Server  
- Shared etcd cluster (external or stacked)  
- Same kubeadm join command for all masters  

---

## 3.1 kubeadm Multi-master initialization flow

### Step 1 — Initialize first control plane:
```
kubeadm init --control-plane-endpoint "k8s-api.example.com:6443"   --upload-certs
```

### Step 2 — kubeadm prints commands:
- Control-plane join command  
- Worker join command  
- Certificate upload key  

### Step 3 — Join additional control-planes:
```
kubeadm join k8s-api.example.com:6443   --token <token>   --discovery-token-ca-cert-hash sha256:<hash>   --control-plane   --certificate-key <cert-key>
```

### Step 4 — Join worker nodes as usual.

---

# 4. Load Balancer for API Server (Mandatory for HA)

The kube-apiserver must have a **single stable endpoint**.

### API Server Load Balancer Requirements:

- TCP passthrough on port 6443  
- Health check on `/livez`  
- Must forward requests only to healthy API servers  
- Supports high availability (VIP or multi-node LB)

---

## 4.1 Example HAProxy configuration

```
frontend k8s-api
    bind *:6443
    mode tcp
    default_backend k8s-masters

backend k8s-masters
    mode tcp
    option tcp-check
    balance roundrobin
    server master1 10.0.0.11:6443 check
    server master2 10.0.0.12:6443 check
    server master3 10.0.0.13:6443 check
```

Test:
```
curl -k https://k8s-api.example.com:6443/livez
```

Expected:
```
ok
```

---

# 5. etcd High Availability

etcd stores cluster state.  
HA etcd is critical — if etcd is down, the cluster cannot function.

---

## 5.1 etcd HA Architecture

```
           +----------------------------+
           |     etcd Cluster (3 nodes) |
           +------+----------+----------+
                  |          |
     +------------+----------+------------+
     |            |          |            |
 +--------+ +--------+  +--------+
 | etcd-1| | etcd-2|  | etcd-3|
 | RAFT  | | RAFT  |  | RAFT  |
 +--------+ +--------+  +--------+

Majority needed: 2 out of 3
```

---

## 5.2 etcd Topologies

### Option A — Stacked etcd (default kubeadm)
- etcd runs **inside** control-plane nodes  
- Simpler  
- Recommended for most users  
- Fewer servers needed  

```
Master-1: kube-apiserver + etcd-1  
Master-2: kube-apiserver + etcd-2  
Master-3: kube-apiserver + etcd-3  
```

### Option B — External etcd cluster
- etcd runs on separate nodes  
- Best for large and mission-critical deployments  
- Higher complexity  

```
etcd nodes separate → control-plane nodes separate
```

---

## 5.3 etcd quorum explanation

| etcd members | Quorum required | Failures tolerated |
|--------------|------------------|---------------------|
| 1 | 1 | 0 |
| 3 | 2 | 1 |
| 5 | 3 | 2 |
| 7 | 4 | 3 |

NEVER deploy an even-numbered etcd cluster.

---

# 6. Kubernetes HA Deployment Scenarios

## Scenario 1 — Stacked Control-Plane + Stacked etcd
- Common for kubeadm
- 3 control-plane nodes
- 3 etcd nodes (co-located)

```
3 masters + API LB + workers
```

## Scenario 2 — External etcd
- Control-plane nodes run without embedded etcd
- etcd nodes deployed separately

Used by:  
- Large enterprises  
- Multi-region HA clusters  

---

# 7. Step-by-Step HA Setup (kubeadm)

### Step 1 — Prepare external load balancer  
Add backend master nodes, configure health checks.

### Step 2 — Initialize first master
```
kubeadm init --control-plane-endpoint "LB:6443" --upload-certs
```

### Step 3 — Install CNI plugin

### Step 4 — Join additional control plane nodes
```
kubeadm join LB:6443 --control-plane --token <token> --discovery-token-ca-cert-hash <hash>
```

### Step 5 — Join worker nodes

---

# 8. Failure Scenarios & HA Behavior

### 8.1 Control-plane node fails
```
Remaining API servers continue serving traffic via load balancer
Scheduler + Controller Manager elect new leaders
Cluster remains functional
```

### 8.2 etcd node fails (1 out of 3)
```
Cluster still has quorum
No outage
Recommended to replace failed node
```

### 8.3 Load balancer fails
```
Cluster becomes unreachable
API servers are healthy but no entrypoint exists
LB must be HA itself (keepalived, VRRP, or cloud LB)
```

---

# 9. Best Practices for Production HA

- Use at least **3 control-plane nodes**  
- Use at least **3 etcd nodes**  
- Never use even-sized etcd clusters  
- Use separate nodes for etcd if cluster is huge  
- Make the load balancer HA  
- Enable audit logs & logging  
- Back up etcd regularly  
- Test disaster recovery procedures

---

# 10. Summary Table

| Component | HA Strategy |
|-----------|-------------|
| Control Plane | Multi-master cluster with LB |
| kube-apiserver | Behind TCP LB |
| scheduler | Leader election, runs on all masters |
| controller-manager | Leader election |
| etcd | 3-node RAFT cluster required |
| Load-balancer | Must be redundant |

---

