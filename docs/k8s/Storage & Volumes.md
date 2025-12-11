---
sidebar_position: 12
---

# K8s Volumes & Storage 

This document explains Kubernetes storage concepts with **detailed explanations and full YAML examples**, including:
- Why Kubernetes storage is needed  
- emptyDir  
- hostPath  
- ConfigMap & Secret as volumes  
- PersistentVolume (PV)  
- PersistentVolumeClaim (PVC)  
- StorageClass  
- Dynamic Provisioning  

---

# 1. Why Kubernetes Storage Is Needed

Kubernetes Pods are **ephemeral**:
- Pods restart → data inside container is lost
- Pods reschedule to another node → data does not move with them

### Problems without persistent storage:
❌ Application logs/data lost  
❌ Databases cannot run  
❌ Uploads disappear  
❌ Config/state cannot survive restarts  

### Kubernetes storage solves:
✅ Data persistence  
✅ Pod-to-Pod shared storage  
✅ Attach storage independent of nodes  
✅ Provision storage dynamically via storage classes  

---

# 2. Volumes Overview

A **Volume** in Kubernetes:
- Lives as long as the Pod lives
- Survives container restarts
- Can be local or remote storage

Volumes are defined inside Pod → `spec.volumes`  
And mounted inside containers → `volumeMounts`

---

# 3. emptyDir Volume

### What is emptyDir?
A temporary directory that exists **only while the Pod is running**.

Use Cases:
- Cache storage  
- Temporary work files  
- Scratch space  

### YAML Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-demo
spec:
  volumes:
    - name: cache-vol
      emptyDir: {}
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "echo Hello > /cache/hello.txt && sleep 3600"]
      volumeMounts:
        - name: cache-vol
          mountPath: /cache
```

❗ Data is deleted when Pod is deleted.

---

# 4. hostPath Volume

### What is hostPath?
Mounts a **directory from the node’s filesystem** into the Pod.

Use Cases:
- Accessing node logs  
- Using node-level tools  
- For development/testing  

⚠ **Not recommended for production** (node-specific, unsafe).

### YAML Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-demo
spec:
  volumes:
    - name: host-vol
      hostPath:
        path: /var/log
        type: Directory
  containers:
    - name: reader
      image: busybox
      command: ["sh", "-c", "ls /host"]
      volumeMounts:
        - name: host-vol
          mountPath: /host
```

---

# 5. ConfigMap & Secret as Volumes

## 5.1 ConfigMap as Volume

Used to mount configuration files.

### ConfigMap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  app.properties: |
    app.mode=production
    app.port=8080
```

### Pod Mounting ConfigMap
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-volume-demo
spec:
  volumes:
    - name: config-vol
      configMap:
        name: app-config
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "cat /config/app.properties && sleep 3600"]
      volumeMounts:
        - name: config-vol
          mountPath: /config
```

---

## 5.2 Secret as Volume

Used for sensitive information.

### Secret
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
stringData:
  username: admin
  password: pass123
```

### Pod Mounting Secret
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-volume-demo
spec:
  volumes:
    - name: secret-vol
      secret:
        secretName: db-secret
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "ls /secret && sleep 3600"]
      volumeMounts:
        - name: secret-vol
          mountPath: /secret
```

Files appear as:
```
/secret/username
/secret/password
```

---

# 6. PersistentVolume (PV)

PV is **cluster-wide storage** provisioned by admin.

### Key Features:
- Independent of Pods  
- Represents NFS, AWS EBS, Azure Disk, GCE PD, Ceph, etc.  
- Has capacity, access modes, reclaim policy  

### PV Example
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
  persistentVolumeReclaimPolicy: Retain
```

---

# 7. PersistentVolumeClaim (PVC)

PVC is a **request** for storage by a Pod.

### PVC Example
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

# 8. Pod Using PVC

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pvc-demo
spec:
  volumes:
    - name: data-vol
      persistentVolumeClaim:
        claimName: app-pvc
  containers:
    - name: app
      image: nginx
      volumeMounts:
        - name: data-vol
          mountPath: /data
```

---

# 9. StorageClass

StorageClass defines **dynamic provisioning rules**.

Useful for:
- AWS EBS
- GCE persistent disks
- Azure Disk
- Local provisioners

### StorageClass Example
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
```

---

# 10. Dynamic Provisioning

With StorageClass + PVC:
- When a PVC is created → Kubernetes **dynamically creates a PV**  
- No need for admin to manually create PVs  

### PVC Using StorageClass
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  storageClassName: fast-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
```

Kubernetes automatically provisions a PV.

---

# 11. Comparison Table

| Feature | emptyDir | hostPath | PV | PVC | StorageClass |
|--------|----------|----------|----|-----|--------------|
| Lifetime | Pod | Node | Manual | Pod request | Cluster |
| Persistence | No | Node | Yes | Yes | Yes |
| Cluster-scoped | No | No | Yes | No | Yes |
| Dynamic provisioning | No | No | No | No | Yes |
| Best for | Cache/temp | Dev/test | Admin storage | App request | Cloud storage |

---

# 12. Best Practices

- Use **PVC + StorageClass** for production  
- Avoid hostPath in real clusters  
- Use Secrets for sensitive info  
- Use ConfigMap for configurations  
- Use emptyDir only for temp data  

---

# Summary

Kubernetes storage enables:
- Persistent state  
- Portable workloads  
- Dynamic storage provisioning  
- Secure config & secret management  

Core components:
- Volumes (emptyDir, hostPath)
- ConfigMap/Secret as volumes  
- PV + PVC  
- StorageClass  
- Dynamic provisioning  

These are essential for running real-world applications in Kubernetes.

# Kubernetes Storage Hands‑On Labs (With Expected Output)

This document extends the previous **Kubernetes Storage Deep Dive** by adding **hands‑on labs**, **step‑by‑step commands**, and **expected outputs**.

It includes labs for:
- emptyDir  
- hostPath  
- ConfigMap & Secret volumes  
- PersistentVolume (PV)  
- PersistentVolumeClaim (PVC)  
- StorageClass  
- Dynamic Provisioning  

---

# LAB 1 — emptyDir Volume

## Objective
Use an `emptyDir` volume to share temporary data between containers.

## YAML
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-lab
spec:
  volumes:
    - name: shared-data
      emptyDir: {}
  containers:
    - name: writer
      image: busybox
      command: ["sh", "-c", "echo 'hello from writer' > /data/msg && sleep 300"]
      volumeMounts:
        - name: shared-data
          mountPath: /data

    - name: reader
      image: busybox
      command: ["sh", "-c", "cat /data/msg && sleep 300"]
      volumeMounts:
        - name: shared-data
          mountPath: /data
```

## Commands
```bash
kubectl apply -f emptydir.yaml
kubectl logs emptydir-lab -c reader
```

## Expected Output
```
hello from writer
```

---

# LAB 2 — hostPath Volume

⚠ For testing only.

## YAML
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-lab
spec:
  volumes:
    - name: host-logs
      hostPath:
        path: /var/log
        type: Directory
  containers:
    - name: inspect
      image: busybox
      command: ["sh", "-c", "ls /host && sleep 200"]
      volumeMounts:
        - name: host-logs
          mountPath: /host
```

## Commands
```bash
kubectl apply -f hostpath.yaml
kubectl logs hostpath-lab
```

## Expected Output
```
dmesg
syslog
kern.log
...
```

---

# LAB 3 — ConfigMap as a Volume

## Step 1 — Create ConfigMap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  settings.conf: |
    environment=dev
    version=1.0
```

Apply:
```bash
kubectl apply -f configmap.yaml
```

## Step 2 — Mount ConfigMap
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-vol-lab
spec:
  volumes:
    - name: cfg
      configMap:
        name: app-config
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "cat /cfg/settings.conf && sleep 300"]
      volumeMounts:
        - name: cfg
          mountPath: /cfg
```

## Expected Output
```
environment=dev
version=1.0
```

---

# LAB 4 — Secret as Volume

## Step 1 — Create Secret
```bash
kubectl create secret generic db-secret   --from-literal=username=admin   --from-literal=password=mypass
```

## Step 2 — Pod Mounting Secret
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-vol-lab
spec:
  volumes:
    - name: creds
      secret:
        secretName: db-secret
  containers:
    - name: debug
      image: busybox
      command: ["sh", "-c", "ls /creds && sleep 300"]
      volumeMounts:
        - name: creds
          mountPath: /creds
```

## Expected Output
```
password
username
```

---

# LAB 5 — PersistentVolume + PersistentVolumeClaim

## Step 1 — Create PV
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-lab
spec:
  capacity:
    storage: 1Gi
  accessModes: ["ReadWriteOnce"]
  hostPath:
    path: /mnt/data
```

## Step 2 — Create PVC
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-lab
spec:
  accessModes: ["ReadWriteOnce"]
  resources:
    requests:
      storage: 1Gi
```

Apply:
```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl get pv,pvc
```

### Expected Output
```
pv-lab   Bound
pvc-lab  Bound
```

## Step 3 — Pod Using PVC
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pvc-client
spec:
  volumes:
    - name: storage
      persistentVolumeClaim:
        claimName: pvc-lab
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "echo 'stored data' > /data/file && sleep 300"]
      volumeMounts:
        - name: storage
          mountPath: /data
```

---

# LAB 6 — StorageClass + Dynamic Provisioning

## Step 1 — Create StorageClass
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
```

*(Use CSI provisioner in real cloud clusters)*

## Step 2 — PVC Requesting Dynamic Storage
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dyn-pvc
spec:
  accessModes: ["ReadWriteOnce"]
  storageClassName: fast
  resources:
    requests:
      storage: 2Gi
```

## Apply & Verify
```bash
kubectl apply -f sc.yaml
kubectl apply -f dyn-pvc.yaml
kubectl get pvc
```

### Expected Output
```
dyn-pvc  Bound
```

---

# Quick Troubleshooting Guide

### PVC stuck in Pending?
Check for matching PV:
```bash
kubectl get pv
```

### PV stuck in Released?
Reclaim policy is probably **Retain**.

### VolumeMount errors?
Check:
```bash
kubectl describe pod <name>
```

---

# Summary

This lab covers:
- Runtime volumes (emptyDir, hostPath)  
- Configuration volumes (ConfigMap, Secret)  
- Persistent storage (PV, PVC)  
- Full automation (StorageClass + dynamic provisioning)
---


# PersistentVolume (PV) & PersistentVolumeClaim (PVC) Binding — Detailed Explanation, Reclaim Policies & Examples

This document explains **how PV and PVC bind**, the **lifecycle of that binding**, **access modes**, **reclaim policies**, and includes **clear YAML examples** and troubleshooting commands. Use this as an operational reference or training note.

---

## 1. High-level overview: PV vs PVC

- **PersistentVolume (PV)** — a cluster resource that represents actual storage (NFS, cloud disk, local disk, etc.). Created by cluster admin or dynamically by provisioner.
- **PersistentVolumeClaim (PVC)** — a user/request resource that asks for storage of certain size, access mode and optionally a `storageClassName`.

Binding is the process where a **PVC is matched to a PV** and both transition into the **Bound** phase so the Pod can mount the volume.

---

## 2. How PV ⇄ PVC binding works (step-by-step)

1. **Admin creates PV(s)** (static provisioning), or a **StorageClass** exists for dynamic provisioning.
2. **User creates a PVC** specifying:
   - `storageClassName` (optional)
   - `accessModes` (e.g., `ReadWriteOnce`)
   - `resources.requests.storage` (e.g., `10Gi`)
3. Kubernetes controller (the *volume controller*) attempts to find a matching PV:
   - PV must be `Available` (not already Bound)
   - PV capacity >= PVC requested size
   - PV `accessModes` must satisfy PVC `accessModes` (PVC requests a subset)
   - If PVC has `selector` labels, PV must match them
   - If PVC requests a `storageClassName`, PV must have that StorageClass (or empty for "" / default)
4. If a suitable PV is found -> PV and PVC are bound:
   - PV `status.phase` becomes `Bound`
   - PVC `status.phase` becomes `Bound`
   - PV `spec.claimRef` is set to the PVC
5. If no suitable PV exists and `storageClassName` is set and dynamic provisioning is available:
   - The provisioner creates a PV dynamically according to the StorageClass parameters, then binds it to the PVC.
6. When a Pod references the PVC, kubelet attaches/mounts the PV to the node running the Pod.

---

## 3. Binding Modes & Timing

- **Immediate binding (volumeBindingMode: Immediate)**  
  PV is provisioned (or selected) immediately when PVC is created. Default in older clusters.

- **WaitForFirstConsumer (volumeBindingMode: WaitForFirstConsumer)**  
  The PV provisioning (or binding) is delayed until a Pod using the PVC is scheduled. This ensures the PV is created in the correct zone/node and avoids provisioning in a zone where the Pod cannot run. Use this for multi-zone clusters and topology-aware provisioning.

---

## 4. Access Modes (what Pods can do with the volume)

- **ReadWriteOnce (RWO)** — The volume can be mounted read-write by a single node. Most cloud block volumes (EBS, PD) are RWO.
- **ReadOnlyMany (ROX)** — The volume can be mounted read-only by many nodes.
- **ReadWriteMany (RWX)** — The volume can be mounted read-write by many nodes (requires shared filesystem like NFS, or supported CSI driver).

PVC `accessModes` must be satisfied by PV's `accessModes` (PV can support multiple modes).

---

## 5. Reclaim Policies (what happens after PVC is deleted)

A PV has a `persistentVolumeReclaimPolicy` field with common values:

- **Delete**  
  When the bound PVC is deleted, the underlying storage asset (cloud disk, dynamic PV) is **deleted** by the provisioner. Use this for ephemeral workloads where you want automatic cleanup.

- **Retain**  
  The underlying storage is **retained** for manual recovery. The PV enters the `Released` phase and still contains data. An admin must manually clean up or recreate a PV to reuse the storage. Use this for backups or data recovery scenarios.

- **Recycle** (deprecated)  
  Attempts a basic scrub (e.g., `rm -rf`) and makes PV available again. This is deprecated and not recommended; dynamic provisioning + proper cleanup is preferred.

**Examples of usage:**
- Databases: use `Retain` to avoid accidental data loss.
- Temporary test environments: use `Delete` to automatically remove cloud disks.

---

## 6. Phases & Status you will observe

- **PV phases**: `Available` → `Bound` → `Released` → (`Failed`)  
  - `Available`: free PV ready to be claimed  
  - `Bound`: claimed by a PVC  
  - `Released`: PVC deleted but PV not yet reclaimed/cleaned  
  - `Failed`: something went wrong (rare)

- **PVC phases**: `Pending` → `Bound` → (deleted)  
  - `Pending`: waiting for PV  
  - `Bound`: matched to PV

---

## 7. YAML Example: Static Provisioning (admin creates PV, user claims with PVC)

### PV (admin)
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-local-1
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/disks/vol1
  persistentVolumeReclaimPolicy: Retain
```

### PVC (user)
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-request-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

**Apply (as admin/user):**
```bash
kubectl apply -f pv-local-1.yaml
kubectl apply -f pvc-request-1.yaml
kubectl get pv,pvc
```

**Expected:**
- `pvc-request-1` moves from `Pending` → `Bound`
- `pv-local-1` status becomes `Bound` and `spec.claimRef` points to the PVC

---

## 8. YAML Example: Dynamic Provisioning with StorageClass (recommended)

### StorageClass (admin)
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs     # example for AWS; use appropriate CSI provisioner in your cluster
parameters:
  type: gp2
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
```

### PVC (user)
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```

**Apply:**
```bash
kubectl apply -f storageclass-standard.yaml
kubectl apply -f pvc-dynamic.yaml
kubectl get pvc
```

**Behavior:**
- PVC will be `Pending` until a Pod is scheduled (because `WaitForFirstConsumer`).
- When a Pod is created that uses the PVC, the provisioner creates a PV in the correct zone and binds it to the PVC.
- Since `reclaimPolicy: Delete`, deleting the PVC will delete the underlying cloud disk.

---

## 9. Observability & Debugging Commands

- Show PVs and PVCs:
```bash
kubectl get pv
kubectl get pvc
kubectl get pv,pvc -o wide
```

- Describe objects to see events:
```bash
kubectl describe pv pv-local-1
kubectl describe pvc pvc-request-1
```

- See StorageClasses:
```bash
kubectl get storageclass
kubectl describe storageclass standard
```

- View the controller events:
```bash
kubectl get events --sort-by='.lastTimestamp'
```

---

## 10. What happens when PVC is deleted? (ReclaimPolicy examples)

### ReclaimPolicy = Delete
- Action: PVC deleted → PV and underlying storage deleted (by provisioner)
- Observed: `kubectl get pv` shows PV removed (or PV in Terminating while provisioner deletes cloud disk)

### ReclaimPolicy = Retain
- Action: PVC deleted → PV moves to `Released` state, underlying data remains
- Admin must manually:
  - Inspect underlying storage and decide to delete or recover
  - Optionally delete `spec.claimRef` and re-provision PV (or create a new PV referring to cleaned storage)

---

## 11. Common Issues & How to Fix

### PVC remains in `Pending`
- No matching PV: check capacity, accessModes, storageClassName
- For dynamic provisioning: ensure a StorageClass with correct provisioner exists
- Use `kubectl describe pvc <name>` to see events

### PV stuck in `Released`
- Underlying volume still has data or reclaim policy is `Retain`; manually inspect and clean
- To reuse PV, remove `spec.claimRef` (careful and usually discouraged) or create a new PV/PVC pair

### Binding to wrong zone
- Use `volumeBindingMode: WaitForFirstConsumer` in StorageClass
- Use topology-aware provisioners/parameters

---

## 12. Best Practices

- Prefer **dynamic provisioning** with StorageClass for cloud environments
- Use **WaitForFirstConsumer** for multi-zone clusters
- Use **Retain** for critical data (manual cleanup), **Delete** for ephemeral volumes
- Set appropriate **accessModes** based on application needs (RWO vs RWX)
- Monitor PV/PVC lifecycle in automation (CI/CD) to avoid orphaned storage

---

## 13. Summary

- **PVC -> PV binding** is automatic when criteria match (size, accessModes, storageClass, labels)
- **Dynamic provisioning** via StorageClass is the recommended approach in modern clusters
- **Reclaim policies** control lifecycle of the physical storage after PVC deletion:
  - `Delete` — automatic cleanup
  - `Retain` — manual cleanup / recovery
  - `Recycle` — deprecated
- Use `kubectl describe` and `kubectl get pv,pvc` to inspect and debug binding issues




