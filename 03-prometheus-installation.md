# Module 3 – Installing Prometheus & Grafana

In this module, we'll install a complete Kubernetes monitoring stack using the official `kube-prometheus-stack` Helm chart.

## Topics Covered

- Why use Helm for Prometheus?
- kube-prometheus-stack
- Add Helm Repository
- Update Repository
- Search Available Charts
- Explore Chart Metadata
- Explore Default Values
- Create Namespace
- Install Monitoring Stack
- Verify Installation

---

# Why Use Helm?

Installing Prometheus manually requires creating many Kubernetes resources such as:

- Prometheus
- Grafana
- Alertmanager
- Node Exporter
- kube-state-metrics
- RBAC
- ConfigMaps
- Secrets
- Services
- Deployments
- StatefulSets
- CRDs

Instead of creating all these resources manually, we can install them using a single Helm chart.

---

# What is kube-prometheus-stack?

`kube-prometheus-stack` is the official Helm chart for deploying a complete Kubernetes monitoring solution.

It installs:

- Prometheus
- Grafana
- Alertmanager
- Node Exporter
- kube-state-metrics
- Prometheus Operator
- Custom Resource Definitions (CRDs)

---

# Step 1 – Verify Helm

```bash
helm version
```

---

# Step 2 – Check Existing Helm Repositories

```bash
helm repo list
```

---

# Step 3 – Add Prometheus Community Repository

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

Verify:

```bash
helm repo list
```

---

# Step 4 – Update Helm Repository

```bash
helm repo update
```

---

# Step 5 – Search Available Charts

```bash
helm search repo prometheus-community
```

This lists all charts available in the Prometheus Community repository.

---

# Step 6 – Inspect the Chart

View chart metadata:

```bash
helm show chart prometheus-community/kube-prometheus-stack
```

Important fields:

- Chart Name
- Chart Version
- App Version
- Dependencies

---

# Chart Dependencies

The chart automatically installs several components.

| Component | Purpose |
|-----------|---------|
| Prometheus Operator | Manages Prometheus resources |
| Prometheus | Collects and stores metrics |
| Alertmanager | Sends alerts |
| Grafana | Visualizes metrics |
| Node Exporter | Collects Linux node metrics |
| kube-state-metrics | Collects Kubernetes object metrics |
| CRDs | Required by Prometheus Operator |

---

# Step 7 – Explore Default Values

Export default values:

```bash
helm show values prometheus-community/kube-prometheus-stack > values.yaml
```

The generated file contains more than **5600 lines**, showing that almost every aspect of the monitoring stack is configurable.

After exploring the file, it can be removed because it is generated content.

```bash
rm values.yaml
```

---

# Step 8 – Create Monitoring Namespace

```bash
kubectl create namespace monitoring
```

Verify:

```bash
kubectl get ns
```

---

# Step 9 – Install kube-prometheus-stack

```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
--namespace monitoring
```

---

# Verify Helm Release

```bash
helm list -n monitoring
```

Expected Status:

```text
STATUS: deployed
```

---

# Verify Pods

```bash
kubectl get pods -n monitoring
```

Expected components:

- Grafana
- Prometheus
- Alertmanager
- Prometheus Operator
- Node Exporter
- kube-state-metrics

---

# Verify Services

```bash
kubectl get svc -n monitoring
```

---

# Verify Deployments

```bash
kubectl get deployments -n monitoring
```

Expected:

- Grafana
- Prometheus Operator
- kube-state-metrics

---

# Verify StatefulSets

```bash
kubectl get statefulsets -n monitoring
```

Expected:

- Prometheus
- Alertmanager

StatefulSets are used because these components store persistent data.

---

# Verify DaemonSets

```bash
kubectl get daemonsets -n monitoring
```

Expected:

- Prometheus Node Exporter

Node Exporter runs as a DaemonSet so that one Pod is deployed on every Kubernetes node.

---

# Architecture After Installation

```text
                   Kubernetes Cluster
                           │
        ┌──────────────────┴──────────────────┐
        │                                     │
        ▼                                     ▼
 Node Exporter                    kube-state-metrics
        │                                     │
        └──────────────────┬──────────────────┘
                           ▼
                 Prometheus Server
                           │
              ┌────────────┴────────────┐
              ▼                         ▼
      Alertmanager                 Time Series DB
                                          │
                                          ▼
                                      Grafana
```

---

# Summary

After completing this module, you should understand:

- ✅ Why Helm is used
- ✅ What kube-prometheus-stack installs
- ✅ Helm repository management
- ✅ Chart inspection
- ✅ Chart dependencies
- ✅ Installing the monitoring stack
- ✅ Verifying Kubernetes resources
- ✅ Understanding why Deployments, StatefulSets, and DaemonSets are used

---

# Next Module

## Module 4 – Exploring Prometheus & Grafana

Topics:

- Access Prometheus UI
- Access Grafana UI
- Prometheus Targets
- Service Discovery
- Default Dashboards
- First PromQL Query