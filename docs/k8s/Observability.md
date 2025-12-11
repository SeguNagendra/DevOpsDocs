---
sidebar_position: 18
---

# Kubernetes Observability 
### Metrics, Prometheus, Grafana, EFK/Loki, Tracing

This document provides a **clean, structured, and deeply explained guide** to core Kubernetes observability components:

- Metrics Server  
- Prometheus  
- Grafana  
- Logging with EFK (Elasticsearch, Fluentd, Kibana) / Loki  
- Tracing basics  

---

# 1. What Is Observability in Kubernetes?

**Observability** is the ability to understand *what is happening inside your cluster* by analyzing:

- **Metrics** (CPU, memory, network, latency)
- **Logs** (applications, system events)
- **Traces** (request flow through microservices)

Observability answers:
- Why is my application slow?
- Why did this Pod crash?
- How is resource usage trending?
- Which microservice call is failing?

---

# 2. Metrics Server (For Kubernetes Resource Metrics)

Metrics Server collects lightweight resource usage metrics:
- Pod CPU/memory  
- Node CPU/memory  

Used by:
- `kubectl top`  
- Horizontal Pod Autoscaler (HPA)  

---

## 2.1 Install Metrics Server (Example for clusters)

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

## 2.2 Check Metrics

### Node metrics:
```bash
kubectl top nodes
```

Expected output:
```
NAME      CPU(cores)   MEMORY(bytes)
node-1    120m         1024Mi
```

### Pod metrics:
```bash
kubectl top pods
```

Expected:
```
nginx-xyz   50m CPU   120Mi Memory
```

Metrics Server is *not* a historical monitoring system — only real-time metrics.

---

# 3. Prometheus – Full Metrics Monitoring

Prometheus is the **standard monitoring system** for Kubernetes.

### Key Features:
- Pull-based metrics scraping  
- PromQL query language  
- Time-series database  
- Alert manager support  
- Auto-discovery of Kubernetes targets  

---

## 3.1 Install Prometheus Using Helm

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prom prometheus-community/prometheus
```

---

## 3.2 Access Prometheus UI

```bash
kubectl port-forward svc/prom-prometheus-server 9090:80
```

Open:
```
http://localhost:9090
```

---

## 3.3 Example PromQL Queries

### CPU usage
```
rate(container_cpu_usage_seconds_total[5m])
```

### Memory usage
```
container_memory_usage_bytes
```

### Pod restarts
```
kube_pod_container_status_restarts_total
```

Prometheus provides **raw metrics** needed for alerts, dashboards, and autoscaling.

---

# 4. Grafana – Dashboards & Visualization

Grafana reads metrics from:
- Prometheus  
- Loki  
- ElasticSearch  
- Many more data sources  

---

## 4.1 Install Grafana

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm install graf grafana/grafana
```

---

## 4.2 Access Grafana

```bash
kubectl port-forward svc/graf-grafana 3000:80
```

Default login:
```
user: admin
password: prom-operator generated secret
```

---

## 4.3 Import Kubernetes Dashboards

Grafana provides ready-made dashboards:

- Node Exporter Full  
- Kubernetes Cluster Monitoring  
- Pod Resource Usage  

Dashboard IDs (Grafana Library):
- **6417** – Kubernetes Cluster  
- **8588** – Node Exporter  
- **315** – NGINX  

---

# 5. Logging – EFK Stack (Elasticsearch + Fluentd + Kibana)

## 5.1 EFK Architecture

```
Pods → Fluentd → Elasticsearch → Kibana UI
```

### Fluentd
- Collects logs from nodes  
- Parses and filters logs  
- Sends logs to Elasticsearch  

### Elasticsearch
- Stores and indexes log data  

### Kibana
- Visualization & search interface  

---

## 5.2 Example Fluentd DaemonSet Snippet

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
spec:
  template:
    spec:
      containers:
        - name: fluentd
          image: fluent/fluentd:v1
          volumeMounts:
            - name: varlog
              mountPath: /var/log
      volumes:
        - name: varlog
          hostPath:
            path: /var/log
```

---

## 5.3 Kibana Access
Once deployed:

```bash
kubectl port-forward svc/kibana 5601:5601
```

---

# 6. Logging – Loki (Grafana Alternative to Elasticsearch)

Loki is a **lightweight, cost-effective logging solution**.

### Why Loki?
- Stores logs in compressed chunks  
- Only indexes labels (much cheaper than Elasticsearch)  
- Best with Promtail + Grafana  

---

## 6.1 Install Loki + Promtail (Log Collector)

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm install loki grafana/loki-stack
```

---

## 6.2 Query Logs in Grafana

Example LogQL queries:

### Show logs:
```
{app="nginx"}
```

### Search in logs:
```
{app="nginx"} |= "error"
```

### Count error logs:
```
sum(count_over_time({app="api"} |= "500" [5m]))
```

Loki integrates natively with Grafana dashboards.

---

# 7. Tracing Basics (Distributed Tracing)

Tracing helps you observe the **path of a request** through microservices.

Without tracing:
- Hard to troubleshoot slow requests  
- Hard to detect where errors originate  

### Popular tracing tools:
- **Jaeger**
- **Zipkin**
- **OpenTelemetry**

---

## 7.1 Example Trace Flow

```
Client → API Gateway → User Service → DB Service → Response
```

Tracing captures:
- Span duration  
- Errors  
- Context propagation  

---

## 7.2 Install Jaeger (All-in-One)

```bash
kubectl apply -f https://github.com/jaegertracing/jaeger-operator/releases/latest/download/jaeger-operator.yaml
```

---

## 7.3 Access Jaeger UI
```bash
kubectl port-forward svc/jaeger-query 16686:16686
```

---

## 7.4 Example Instrumentation (OpenTelemetry)

```python
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

with tracer.start_as_current_span("user-login") as span:
    span.set_attribute("user.id", 123)
```

---

# 8. Combined Observability Architecture

```
Metrics:
    Metrics Server → Prometheus → Grafana

Logs:
    Promtail/Fluentd → Loki/Elasticsearch → Grafana/Kibana

Tracing:
    OpenTelemetry → Jaeger → Grafana
```

---

# 9. Summary

| Component | Purpose |
|-----------|----------|
| Metrics Server | Basic CPU/Memory metrics for HPA |
| Prometheus | Full metrics monitoring + alerts |
| Grafana | Visualization & dashboards |
| EFK | Reactive log storage & search |
| Loki | Lightweight log collection |
| Jaeger/Tracing | Understand request flow |

A complete observability stack is essential for:
- Debugging  
- Performance tuning  
- Autoscaling  
- Production reliability  

---

