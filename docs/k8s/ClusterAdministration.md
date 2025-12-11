---
sidebar_position: 20
---


# Kubernetes Cluster Administration 

This document covers core cluster administration tasks with **practical, step-by-step instructions** and example commands:

- Cluster setup with `kubeadm`
- Upgrading Kubernetes
- Backup & restore `etcd`
- Node maintenance
- Draining & cordoning nodes

> Assumptions: You have root/administrator access to the nodes, `ssh` access, and basic network connectivity. Commands use `sudo` where appropriate. Adjust usernames, IPs and file paths for your environment.

---

## 1. Cluster Setup (kubeadm)

This section shows a minimal kubeadm-based Kubernetes cluster setup (1 control-plane + multiple worker nodes).

### 1.1 Prerequisites (on all nodes)
- OS: Ubuntu/CentOS (example uses Ubuntu)
- Swap **disabled**
  ```bash
  sudo swapoff -a
  sudo sed -i '/ swap / s/^/#/' /etc/fstab
  ```
- Install container runtime (containerd example)
  ```bash
  # install containerd
  sudo apt update
  sudo apt install -y containerd
  sudo mkdir -p /etc/containerd
  sudo containerd config default | sudo tee /etc/containerd/config.toml
  sudo systemctl restart containerd
  sudo systemctl enable containerd
  ```
- Ensure required sysctl settings
  ```bash
  sudo modprobe overlay
  sudo modprobe br_netfilter
  sudo tee /etc/sysctl.d/k8s.conf <<EOF
  net.bridge.bridge-nf-call-iptables  = 1
  net.ipv4.ip_forward                 = 1
  net.bridge.bridge-nf-call-ip6tables = 1
  EOF
  sudo sysctl --system
  ```

### 1.2 Install kubeadm, kubelet, kubectl (on all nodes)
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main"   | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### 1.3 Initialize Control Plane (on control-plane node)
```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
- Example output includes `kubeadm join ...` command — **save** it to join workers.
- After success, configure kubectl for admin user:
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### 1.4 Install Pod Network (example: Calico)
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### 1.5 Join Worker Nodes
On each worker node, run the `kubeadm join ...` command printed at control-plane initialization, e.g.:
```bash
sudo kubeadm join 10.0.0.10:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### 1.6 Verify Cluster
```bash
kubectl get nodes
kubectl get pods -n kube-system
```
- Expect control-plane and worker nodes in `Ready` state and CNI pods `Running`.

---

## 2. Upgrading Kubernetes

This section discusses upgrading kubeadm clusters in a safe, recommended order:
1. Control plane
2. Worker nodes
3. kubelet/kubectl

### 2.1 Check current versions
```bash
kubectl version --short
kubeadm version
```

### 2.2 Plan upgrade path
- Follow Kubernetes version skew policy: upgrade one minor version at a time (e.g., 1.21 → 1.22)
- Read release notes for breaking changes

### 2.3 Upgrade kubeadm package (on control plane)
```bash
sudo apt-get update
sudo apt-get install -y kubeadm=<new-version>-00
```

### 2.4 Drain control plane (optional single-control-plane)
For single-control-plane clusters you may upgrade in-place; for HA clusters, upgrade one control-plane at a time.

### 2.5 Plan with `kubeadm upgrade plan`
```bash
sudo kubeadm upgrade plan
```

### 2.6 Apply control plane upgrade
```bash
sudo kubeadm upgrade apply v1.26.0
```
- This updates control plane static Pods (kube-apiserver, controller-manager, scheduler)

### 2.7 Upgrade kubelet and kubectl on control plane & nodes
```bash
sudo apt-get install -y kubelet=<new-version>-00 kubectl=<new-version>-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

### 2.8 Upgrade worker nodes
1. Drain a node:
   ```bash
   kubectl drain worker-1 --ignore-daemonsets --delete-local-data
   ```
2. SSH to node and upgrade packages:
   ```bash
   sudo apt-get update
   sudo apt-get install -y kubelet=<new-version>-00 kubectl=<new-version>-00
   sudo systemctl restart kubelet
   ```
3. Uncordon:
   ```bash
   kubectl uncordon worker-1
   ```
4. Repeat for each worker.

### 2.9 Verify
```bash
kubectl get nodes
kubectl get cs
kubectl get pods -A
```

---

## 3. Backup & Restore etcd

`etcd` holds cluster state — backup before any critical changes.

> Note: Commands assume a kubeadm-managed static etcd (control-plane) using `/var/lib/etcd`.

### 3.1 Backup etcd (snapshot) — Example (v3 client)
On control-plane node:
```bash
sudo ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379   --cacert=/etc/kubernetes/pki/etcd/ca.crt   --cert=/etc/kubernetes/pki/etcd/server.crt   --key=/etc/kubernetes/pki/etcd/server.key   snapshot save /tmp/etcd-snapshot-$(date +%F).db
```
- Confirm snapshot:
```bash
ls -lh /tmp/etcd-snapshot-*.db
```

### 3.2 Restore etcd from snapshot (single-node example)
> WARNING: Restoring etcd can be destructive — follow docs for HA clusters.

1. Stop kube-apiserver / kubelet or scale static pods down as needed.
2. Restore:
```bash
sudo ETCDCTL_API=3 etcdctl snapshot restore /tmp/etcd-snapshot-2023-09-01.db   --data-dir /var/lib/etcd-from-backup
```
3. Move/replace data dir (example):
```bash
sudo systemctl stop kubelet
sudo mv /var/lib/etcd /var/lib/etcd-old
sudo mv /var/lib/etcd-from-backup /var/lib/etcd
sudo chown -R etcd:etcd /var/lib/etcd
sudo systemctl start kubelet
```
4. Start etcd / kube-apiserver and verify cluster health:
```bash
kubectl get componentstatus
kubectl get nodes
```

### 3.3 Verify snapshot (etcdctl)
```bash
sudo ETCDCTL_API=3 etcdctl --write-out=json   --endpoints=https://127.0.0.1:2379   --cacert=/etc/kubernetes/pki/etcd/ca.crt   --cert=/etc/kubernetes/pki/etcd/server.crt   --key=/etc/kubernetes/pki/etcd/server.key   snapshot status /tmp/etcd-snapshot-*.db
```

---

## 4. Node Maintenance

Routine tasks: apply OS patches, kernel updates, replace disk, etc.

### 4.1 Safe maintenance steps
1. **Cordon** node (mark unschedulable):
   ```bash
   kubectl cordon node-1
   ```
2. **Drain** node (evict user Pods, keep DaemonSets):
   ```bash
   kubectl drain node-1 --ignore-daemonsets --delete-local-data --force
   ```
3. SSH into node and perform maintenance:
   ```bash
   sudo apt-get update && sudo apt-get upgrade -y
   sudo reboot
   ```
4. After node is back, **uncordon**:
   ```bash
   kubectl uncordon node-1
   ```

### 4.2 Best practices
- Drain nodes one at a time.
- Use PodDisruptionBudgets (PDBs) to protect application availability.
- Monitor the cluster during maintenance.

---

## 5. Draining & Cordoning Nodes (Detailed)

### 5.1 Cordon — Mark node unschedulable
```bash
kubectl cordon <node-name>
```
- Node remains running existing Pods but scheduler won't place new Pods.

### 5.2 Drain — Evict pods safely
```bash
kubectl drain <node-name> --ignore-daemonsets --delete-local-data
```
Flags:
- `--ignore-daemonsets`: Do not evict DaemonSets (they run on every node).
- `--delete-local-data`: Allow deletion of Pods with local data (use with caution).
- `--force`: Force eviction of mirror pods or pods that don't respect eviction API.

### 5.3 Uncordon — Re-enable scheduling
```bash
kubectl uncordon <node-name>
```

### 5.4 Draining with PodDisruptionBudgets (PDB)
PDB ensures a minimum number of replicas are always available.

Example PDB:
```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: web-pdb
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: web
```
When draining, `kubectl drain` will respect PDBs and may fail to evict if it would violate the budget.

---

## Appendix — Useful Commands & Checks

### Check node conditions
```bash
kubectl get nodes
kubectl describe node <node>
```

### List pods on a node
```bash
kubectl get pods --all-namespaces --field-selector spec.nodeName=<node-name>
```

### Force delete stuck pods
```bash
kubectl delete pod <pod-name> --grace-period=0 --force
```

### View kubeadm token(s)
```bash
kubeadm token list
```

### Create new join token
```bash
kubeadm token create --print-join-command
```

---

## Final Notes & Safety

- Always snapshot `etcd` before making cluster-state changes.
- Use HA control-plane for production; avoid single-control-plane for production clusters.
- Test upgrades in staging first.
- Keep `kubeadm`, `kubelet`, and `kubectl` versions consistent and follow the official upgrade matrix.
- Maintain secure backups of certificates and etcd snapshots.

---


# Kubernetes Cluster Administration — Diagrams + Hands-On Labs

This document bundles **architecture diagrams (ASCII)** and **hands-on cluster administration labs** with step-by-step commands and expected outputs. It's an add-on to the kubeadm guide and covers:

- Diagrams: kubeadm flow, control plane & worker node lifecycle, etcd backup/restore, drain/cordon flows
- Labs:
  - Lab A: kubeadm cluster setup (mini)
  - Lab B: Upgrade control plane & workers (simulation)
  - Lab C: etcd snapshot backup & restore (safe practice)
  - Lab D: Node maintenance (cordon/drain/uncordon) with PDB
  - Lab E: Recovery from failed node (force-delete + rejoin)
- Verification commands and expected outputs for each lab

> NOTE: Replace placeholder IPs, filenames, and tokens with values from your environment.

---

## PART 1 — ASCII DIAGRAMS

### 1.1 kubeadm Init & Join Flow
```
Control-plane (kubeadm init)
   |
   |-- generates certs, kubeconfig, static Pods (kube-apiserver, controller-manager, scheduler, etcd)
   |
   |-- prints "kubeadm join <IP>:6443 --token ... --discovery-token-ca-cert-hash sha256:..."
   |
Workers (kubeadm join) -- run the join command --> register with API Server
```

### 1.2 Control Plane Static Pods Lifecycle
```
kubelet (on control-plane) watches /etc/kubernetes/manifests
  └─> kube-apiserver static pod manifest placed here
  └─> kube-scheduler
  └─> kube-controller-manager
  └─> etcd (if stacked)
Static Pods are managed by kubelet; kubeadm upgrades replace these manifests during 'kubeadm upgrade apply'
```

### 1.3 etcd snapshot + restore (high level)
```
backup:
  etcdctl (TLS) --> snapshot save /tmp/etcd-snap.db  (store safely off-node)

restore:
  stop kube-apiserver/kubelet (or use restore workflow)
  etcdctl snapshot restore /tmp/etcd-snap.db --data-dir /var/lib/etcd-from-backup
  swap data dir, chown, start services
```

### 1.4 Node maintenance & drain flow
```
kubectl cordon node-1
kubectl drain node-1 --ignore-daemonsets --delete-local-data
  └─> Scheduler will not schedule new Pods
  └─> Eviction API requests Pods to be evicted (respecting PDB)
  └─> DaemonSets remain on node
Perform maintenance (patch, reboot)
kubectl uncordon node-1
```

---

## PART 2 — HANDS-ON LABS (Step-by-step)

### LAB A — kubeadm Minimal Cluster Setup (Hands-on)
**Goal:** Create a minimal cluster (1 control-plane, 1 worker) for testing.

**Prereqs:** Two VMs (control-plane, worker) accessible via SSH. Swap disabled on both.

#### Step A1 — On all nodes: install containerd + kubeadm/kubelet/kubectl
(Commands same as the main guide; abbreviated here)
```bash
# Install containerd, kubeadm, kubelet, kubectl (Ubuntu example)
sudo swapoff -a
# install containerd...
# install kubeadm kubelet kubectl...
sudo systemctl enable --now containerd kubelet
```

#### Step A2 — Initialize control plane
```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
**Expected output snippet:**
```
Your Kubernetes control-plane has initialized successfully!
You can now join any number of worker nodes by running the following on each as root:
kubeadm join 10.0.0.10:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

#### Step A3 — Configure kubectl for admin
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

#### Step A4 — Install CNI (Calico example)
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```
**Verify:**
```bash
kubectl get pods -n kube-system
```
**Expected:** CNI pods `Running`, control-plane node `Ready`.

#### Step A5 — Join worker
On worker node, run:
```bash
sudo kubeadm join 10.0.0.10:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```
**Verify cluster:**
```bash
kubectl get nodes
```
**Expected output (example):**
```
NAME           STATUS   ROLES           AGE   VERSION
control-plane  Ready    control-plane   5m    v1.26.0
worker-1       Ready    <none>          2m    v1.26.0
```

---

### LAB B — Upgrade Control Plane & Worker (Simulation / Safe Steps)
**Goal:** Practice upgrade workflow on a non-production cluster.

> Always test in staging. This lab simulates a minor upgrade (e.g., v1.26.0 -> v1.27.0).

#### Step B1 — On control-plane: check plan
```bash
sudo apt-get update
sudo apt-get install -y kubeadm=1.27.0-00
sudo kubeadm upgrade plan
```
**Expected:** Shows available versions and recommended upgrade target.

#### Step B2 — Apply control plane upgrade
```bash
sudo kubeadm upgrade apply v1.27.0
# watch kube-system pods update
kubectl get pods -n kube-system -w
```
**Expected:** kube-apiserver, kube-controller-manager static pods are replaced; control plane becomes `Ready`.

#### Step B3 — Upgrade kubelet/kubectl & drain worker
On each worker:
```bash
kubectl drain worker-1 --ignore-daemonsets --delete-local-data
sudo apt-get install -y kubelet=1.27.0-00 kubectl=1.27.0-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet
kubectl uncordon worker-1
```
**Expected:** Node re-enters `Ready` with new kubelet version.

---

### LAB C — etcd Snapshot Backup & Restore (Safe Practice)
**Goal:** Take an etcd snapshot and perform a safe restore in a single-control-plane lab.

> CAUTION: Restoring etcd in HA requires more careful orchestration. This lab demonstrates the steps for a single-control-plane test cluster.

#### Step C1 — Take snapshot (control-plane)
```bash
sudo ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379   --cacert=/etc/kubernetes/pki/etcd/ca.crt   --cert=/etc/kubernetes/pki/etcd/server.crt   --key=/etc/kubernetes/pki/etcd/server.key   snapshot save /tmp/etcd-snap-$(date +%F).db
```
**Expected:**
```
Snapshot saved at /tmp/etcd-snap-2025-12-07.db
```

#### Step C2 — Verify snapshot
```bash
sudo ETCDCTL_API=3 etcdctl snapshot status /tmp/etcd-snap-*.db
```
**Expected:** JSON status with `dbSize`, `revision`, `totalKey` fields.

#### Step C3 — Simulate data loss & restore
1. Stop control-plane components:
```bash
sudo systemctl stop kubelet
# or move static pod manifests temporarily
sudo mv /etc/kubernetes/manifests /etc/kubernetes/manifests.disabled
```
2. Restore snapshot:
```bash
sudo ETCDCTL_API=3 etcdctl snapshot restore /tmp/etcd-snap-2025-12-07.db   --data-dir /var/lib/etcd-from-backup
```
3. Replace data-dir (CAREFUL: this is destructive)
```bash
sudo mv /var/lib/etcd /var/lib/etcd-old
sudo mv /var/lib/etcd-from-backup /var/lib/etcd
sudo chown -R etcd:etcd /var/lib/etcd
```
4. Restore manifests and start kubelet:
```bash
sudo mv /etc/kubernetes/manifests.disabled /etc/kubernetes/manifests
sudo systemctl start kubelet
```
**Expected:** Control plane components come up and `kubectl get nodes` returns nodes. Validate cluster state.

---

### LAB D — Node Maintenance: Cordon, Drain, Uncordon with PDB
**Goal:** Safely perform maintenance while respecting PodDisruptionBudget.

#### Step D1 — Create Deployment with PDB
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: web-pdb
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: web
```
Apply and verify:
```bash
kubectl apply -f web-deploy.yaml
kubectl get pdb
```
**Expected:** PDB exists with `minAvailable=2`.

#### Step D2 — Cordon & Drain node
```bash
kubectl cordon worker-1
kubectl drain worker-1 --ignore-daemonsets --delete-local-data
```
**Expected behavior:** Drain will fail if evicting would violate PDB. If it succeeds, Pods are rescheduled to other nodes.

#### Step D3 — Perform maintenance and uncordon
```bash
# perform updates, reboot
kubectl uncordon worker-1
kubectl get nodes
```
**Expected:** Node returns to `Ready`.

---

### LAB E — Recovery from Failed Node (Force delete + Rejoin)
**Goal:** Handle a node that will not come back (hardware failure simulation).

#### Step E1 — Mark node as NotReady or remove
```bash
kubectl get nodes
# If stuck NotReady, remove from cluster:
kubectl delete node failed-node
```
#### Step E2 — Force-delete pods if necessary
```bash
kubectl get pods --all-namespaces --field-selector spec.nodeName=failed-node
kubectl delete pod <pod-name> --grace-period=0 --force
```
#### Step E3 — Rebuild & rejoin worker (on new node)
Install kubeadm/kubelet and run join command (from control-plane):
```bash
kubeadm join 10.0.0.10:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```
**Expected:** New node appears in `kubectl get nodes` as `Ready`.

---

## PART 3 — Verification & Useful Commands (Quick Reference)

- Check nodes: `kubectl get nodes -o wide`
- List pods by node: `kubectl get pods -A --field-selector spec.nodeName=<node>`
- Cordon a node: `kubectl cordon <node>`
- Drain a node: `kubectl drain <node> --ignore-daemonsets --delete-local-data`
- Uncordon: `kubectl uncordon <node>`
- Take etcd snapshot: (see Lab C)
- Restore etcd snapshot: (see Lab C)
- Show kubeadm tokens: `kubeadm token list`
- Create join token: `kubeadm token create --print-join-command`
- Check component status: `kubectl get cs` (deprecated in newer clusters; use pod checks)
- Describe node: `kubectl describe node <node>`

---

## PART 4 — Safety Checklist & Tips

- Always backup etcd before upgrades or major changes.
- Test upgrade in staging with similar topology.
- Use HA control plane in production.
- Use PodDisruptionBudgets to protect apps during maintenance.
- Keep kubeadm/kubelet/kubectl versions consistent.
- Store etcd snapshots off-node (S3, NFS) and rotate snapshots.
- Automate token rotation and certificate renewal as part of ops.

---




