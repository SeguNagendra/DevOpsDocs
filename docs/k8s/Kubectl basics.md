---
sidebar_position: 5
---

#  `kubectl` Commands 

This document is a **practical `kubectl` command reference** for day‑to‑day Kubernetes work:
- Viewing resources
- Creating, updating, deleting objects
- Debugging & logs
- Scaling & rollouts
- Config, secrets, context, and more


---

## 1. Basic Command Structure

```bash
kubectl [command] [TYPE] [NAME] [flags]
```

- `TYPE` → Resource type (pod, deployment, service, etc.)
- `NAME` → Name of the resource (optional)
- `-n` / `--namespace` → Namespace (optional)

Example:
```bash
kubectl get pods -n dev
```

---

## 2. Cluster & Context Information

### 2.1 Cluster Info

```bash
kubectl cluster-info
kubectl cluster-info dump          # Debug info about the cluster
```

### 2.2 Get Current Context

```bash
kubectl config current-context
```

### 2.3 List Contexts

```bash
kubectl config get-contexts
```

### 2.4 Switch Context

```bash
kubectl config use-context <context-name>
```

---

## 3. Namespace Management

### 3.1 List Namespaces

```bash
kubectl get namespaces
kubectl get ns
```

### 3.2 Create Namespace

```bash
kubectl create namespace dev
```

### 3.3 Delete Namespace

```bash
kubectl delete namespace dev
```

---

## 4. Viewing Resources (`get`)

### 4.1 Generic Form

```bash
kubectl get <resource-type>
kubectl get <resource-type> -n <namespace>
kubectl get <resource-type> <name>
```

### 4.2 Common Examples

```bash
kubectl get pods
kubectl get pods -o wide
kubectl get deployments
kubectl get rs
kubectl get svc
kubectl get nodes
kubectl get configmaps
kubectl get secrets
kubectl get ingress
```

### 4.3 All Resources in a Namespace

```bash
kubectl get all -n dev
```

---

## 5. Detailed Resource Info (`describe`)

```bash
kubectl describe pod <pod-name>
kubectl describe deployment <deployment-name>
kubectl describe service <service-name>
kubectl describe node <node-name>
```

This shows:
- Events
- Labels
- Annotations
- Pod status & conditions
- Error messages (useful for debugging)

---

## 6. Creating & Applying Manifests

### 6.1 Apply YAML (Create or Update)

```bash
kubectl apply -f app.yaml
kubectl apply -f k8s-manifests/      # Entire folder
```

### 6.2 Create From Imperative Commands

```bash
kubectl create deployment nginx-deploy --image=nginx:1.25
kubectl expose deployment nginx-deploy --port=80 --type=ClusterIP
```

> Use `create` for one-time quick objects, `apply` for GitOps/YAML-driven.

---

## 7. Editing Resources

```bash
kubectl edit deployment nginx-deploy
kubectl edit svc nginx-service
```

This opens the resource in your default editor.

---

## 8. Deleting Resources

```bash
kubectl delete pod <pod-name>
kubectl delete deployment <deployment-name>
kubectl delete svc <service-name>
kubectl delete -f app.yaml
kubectl delete namespace dev
```

---

## 9. Working with Pods

### 9.1 List Pods

```bash
kubectl get pods
kubectl get pods -n dev
kubectl get pods -o wide
```

### 9.2 Pod Logs

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>
kubectl logs -f <pod-name>          # Follow logs (like tail -f)
```

### 9.3 Execute Command in Pod

```bash
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -- /bin/sh
kubectl exec -it <pod-name> -- env
```

### 9.4 Port Forward

```bash
kubectl port-forward pod/<pod-name> 8080:80
kubectl port-forward svc/<service-name> 8080:80
```

You can then access:
```text
http://localhost:8080
```

---

## 10. Workloads (Deployment, ReplicaSet, etc.)

### 10.1 Deployments

```bash
kubectl get deployments
kubectl describe deployment <name>
```

### 10.2 Create Deployment (Imperative)

```bash
kubectl create deployment nginx-deploy --image=nginx:1.25 --replicas=2
```

### 10.3 Scale Deployment

```bash
kubectl scale deployment nginx-deploy --replicas=4
```

### 10.4 Update Image

```bash
kubectl set image deployment/nginx-deploy nginx=nginx:1.26
```

### 10.5 Rollout Status

```bash
kubectl rollout status deployment/nginx-deploy
```

### 10.6 Rollback Deployment

```bash
kubectl rollout undo deployment/nginx-deploy
```

---

## 11. Services & Networking

### 11.1 List Services

```bash
kubectl get svc
kubectl get svc -n dev
```

### 11.2 Describe Service

```bash
kubectl describe svc <service-name>
```

### 11.3 Create Service (Imperative)

Expose a Deployment as a Service:

```bash
kubectl expose deployment nginx-deploy --name=nginx-svc --port=80 --target-port=80 --type=ClusterIP
```

For NodePort:
```bash
kubectl expose deployment nginx-deploy --name=nginx-nodeport --port=80 --type=NodePort
```

---

## 12. ConfigMaps & Secrets

### 12.1 ConfigMap Commands

Create from literals:
```bash
kubectl create configmap app-config   --from-literal=APP_ENV=prod   --from-literal=LOG_LEVEL=info
```

Create from file:
```bash
kubectl create configmap app-config --from-file=config.properties
```

View:
```bash
kubectl get configmaps
kubectl describe configmap app-config
```

### 12.2 Secret Commands

Create generic secret:
```bash
kubectl create secret generic db-secret   --from-literal=DB_USER=admin   --from-literal=DB_PASSWORD=passw0rd
```

View:
```bash
kubectl get secrets
kubectl describe secret db-secret
```

Decode secret (example):
```bash
kubectl get secret db-secret -o jsonpath='{.data.DB_USER}' | base64 -d
```

---

## 13. Events & Troubleshooting

### 13.1 View Events

```bash
kubectl get events
kubectl get events --sort-by='.lastTimestamp'
```

### 13.2 Describe Pod (Most Used)

```bash
kubectl describe pod <pod-name>
```

This shows:
- Reasons for CrashLoopBackOff
- Image pull errors
- Readiness/liveness failures

---

## 14. Resource Usage (Metrics)

> Requires Metrics Server installed.

```bash
kubectl top nodes
kubectl top pods
kubectl top pods -n dev
```

---

## 15. API Discovery Helpers

### 15.1 Get API Resources

```bash
kubectl api-resources
```

### 15.2 Get API Versions

```bash
kubectl api-versions
```

### 15.3 Explain Resource (Built-in Docs)

```bash
kubectl explain pod
kubectl explain deployment.spec
kubectl explain svc.spec.ports
```

---

## 16. Debugging Newer Pods (Optional if Enabled)

```bash
kubectl debug <pod-name> -it --image=busybox -- /bin/sh
```

---

## 17. Apply & Delete All in a Directory

```bash
kubectl apply -f k8s/
kubectl delete -f k8s/
```

---

## 18. Useful Shortcuts & Patterns

### 18.1 Short Names

```bash
kubectl get po        # pods
kubectl get deploy    # deployments
kubectl get svc       # services
kubectl get ns        # namespaces
kubectl get cm        # configmaps
kubectl get rs        # replicasets
```

### 18.2 Common -o Output Options

```bash
kubectl get pods -o wide
kubectl get pods -o yaml
kubectl get pods -o json
```

---

## 19. Suggested Practice Labs

1. **List & inspect resources**
   - `kubectl get`, `kubectl describe`
2. **Deploy an app**
   - `kubectl create deployment`, `kubectl expose`
3. **Scale & update**
   - `kubectl scale`, `kubectl set image`, `kubectl rollout`
4. **Debug**
   - `kubectl logs`, `kubectl exec`, `kubectl describe`, `kubectl get events`

---

# KIND (Kubernetes IN Docker) Commands – Complete Guide

This document provides a **comprehensive list of KIND commands**, going beyond basic cluster creation.
It is useful for **local Kubernetes learning, testing, CI/CD, and troubleshooting**.

---

## 1. What is KIND?

**KIND (Kubernetes IN Docker)** is a tool for running **local Kubernetes clusters using Docker containers as nodes**.

✅ Lightweight  
✅ Fast  
✅ No VM required  
✅ Ideal for learning & testing Kubernetes  

---

## 2. Basic Cluster Management Commands

### Create a Cluster (Default Name: kind)
```bash
kind create cluster
```

### Create a Cluster with Custom Name
```bash
kind create cluster --name mycluster
```

### List All KIND Clusters
```bash
kind get clusters
```

### Delete a Cluster
```bash
kind delete cluster --name mycluster
```

### Delete All Clusters
```bash
kind delete clusters --all
```

---

## 3. Kubernetes Version & Image Control

### Create Cluster with Specific Kubernetes Version
```bash
kind create cluster --image kindest/node:v1.29.0
```

### List Available Node Images (manual reference)
```bash
docker images | grep kindest
```

> KIND node images are published at `kindest/node`

---

## 4. Kubeconfig & Context Management

### Get kubeconfig for a Cluster
```bash
kind get kubeconfig --name mycluster
```

### Export kubeconfig to file
```bash
kind get kubeconfig --name mycluster > mycluster-kubeconfig.yaml
```

### Set kubeconfig explicitly
```bash
export KUBECONFIG=~/.kube/config
```

---

## 5. Load Images into KIND Cluster (Very Important)

### Load Local Docker Image into KIND
```bash
kind load docker-image myimage:latest --name mycluster
```

✅ Avoids pushing image to Docker Hub  
✅ Useful for local builds  

---

### Load Image Archive (tar file)
```bash
kind load image-archive image.tar --name mycluster
```

---

### Verify Image inside KIND Node
```bash
docker exec -it mycluster-control-plane crictl images
```

---

## 6. Cluster Logs & Debugging

### Export Cluster Logs
```bash
kind export logs ./cluster-logs
```

### Export Logs for Specific Cluster
```bash
kind export logs ./logs --name mycluster
```

Useful for:
- Control plane crashes
- Networking issues
- Node failures

---

## 7. Custom Cluster Configuration (Config File)

### Create Cluster with Config File
```bash
kind create cluster --config kind-config.yaml
```

---

### Example: Multi-node Cluster Config
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

---

### Example: Cluster with Port Mapping
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  extraPortMappings:
  - containerPort: 30007
    hostPort: 30007
    protocol: TCP
```

---

## 8. Networking & Docker Integration

### List KIND Docker Containers
```bash
docker ps
```

### Inspect KIND Network
```bash
docker network inspect kind
```

### Exec into Control Plane Node
```bash
docker exec -it mycluster-control-plane bash
```

---

## 9. Working with Nodes

### List Nodes
```bash
kubectl get nodes
```

### Describe a Node
```bash
kubectl describe node mycluster-control-plane
```

---

## 10. Reset & Recreate Cluster (Common Practice)

```bash
kind delete cluster --name mycluster
kind create cluster --name mycluster
```

✅ Clean state  
✅ Fast resets for labs  

---

## 11. KIND + Kubernetes Workflow (Typical)

```text
1. Create KIND cluster
2. Build Docker image locally
3. Load image into KIND
4. Apply Kubernetes manifests
5. Test application
6. Delete cluster
```

---

## 12. Best Practices When Using KIND

✅ Use custom cluster names  
✅ Load local images instead of pushing to registry  
✅ Use config files for multi-node setup  
✅ Delete clusters after use  
✅ Recreate clusters for clean testing  

---

## 13. Common Errors & Tips

### Error: ImagePullBackOff
✅ Solution:
```bash
kind load docker-image myimage:latest
```

### NodePort Not Accessible
✅ Ensure port mapping is configured in KIND config

---

## 14. Useful Combined Commands

```bash
kind create cluster --name dev --image kindest/node:v1.28.0
kubectl cluster-info
kubectl get nodes
```

---

## 15. Summary

- KIND runs Kubernetes inside Docker
- Ideal for local development and learning
- Supports multi-node clusters
- Easy image loading
- Simple cluster reset and cleanup

KIND is one of the **best tools to learn Kubernetes locally**.

---