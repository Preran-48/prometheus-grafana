# Module 1 – Monitoring Fundamentals

In this module, we'll understand the fundamental concepts of monitoring before installing Prometheus and Grafana.

## Topics Covered

- What is Monitoring?
- Why is Monitoring Needed?
- Monitoring vs Logging
- What are Metrics?
- What is a Time Series?
- What is a Time Series Database (TSDB)?
- Why Prometheus?
- Why Grafana?

> **Note:** Once these concepts are clear, learning Prometheus and Grafana becomes much easier.

---

## 1. What is Monitoring?

Monitoring is the process of continuously collecting and observing the health and performance of systems, applications, and infrastructure.

### Simple Definition

> Monitoring is continuously checking whether a system is healthy and performing as expected.

---

## Real-Life Example

Imagine you're riding your **Bike**.

While riding, you continuously monitor:

- Speed
- Fuel Level
- Engine Temperature
- Battery Indicator
- Check Engine Light

These indicators continuously tell you how your bike is performing.

This is called **Monitoring**.

Similarly, in Kubernetes we continuously monitor:

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic
- Running Pods
- Failed Pods
- Pod Restart Count

---

## 2. Why is Monitoring Needed?

Imagine you have deployed an e-commerce application on Kubernetes.

Without monitoring:

```text
Customer
    │
    ▼
Application
```

One day the application becomes slow.

You don't know:

- Is CPU usage high?
- Is Memory exhausted?
- Is the Node full?
- Is the Database slow?
- Are Pods restarting?

You're simply guessing.

---

With monitoring:

```text
Customer
      │
      ▼
Application
      │
      ▼
Metrics
      │
      ▼
Prometheus
      │
      ▼
Grafana Dashboard
```

Now you immediately know:

- CPU Usage = 95%
- Memory Usage = 90%
- Pod Restart Count = 10
- Node Disk Usage = 95%

Instead of guessing, you diagnose problems using actual data.

---

## 3. Monitoring vs Logging

This is one of the most frequently asked interview questions.

| Monitoring | Logging |
|------------|---------|
| Collects numerical metrics | Collects detailed logs and events |
| Answers **"What is happening?"** | Answers **"Why did it happen?"** |
| CPU, Memory, Network, Requests/sec | Stack traces, Errors, Application Logs |
| Prometheus | Elasticsearch, Loki, Splunk, CloudWatch Logs |

### Example

Monitoring tells you:

```text
CPU Usage = 95%
```

Logging tells you:

```text
OutOfMemoryError occurred while processing order #12345
```

Both Monitoring and Logging are important and are usually used together.

---

## 4. What are Metrics?

A **Metric** is a measurable value representing the current state or performance of a system at a specific point in time.

### Examples

| Metric | Value |
|--------|------:|
| CPU Usage | 35% |
| Memory Usage | 2.5 GB |
| Running Pods | 18 |
| HTTP Requests/sec | 250 |
| Disk Usage | 60% |

Prometheus continuously collects these metrics.

---

## 5. What is a Time Series?

Metrics continuously change over time.

Example:

| Time | CPU Usage |
|------|----------:|
| 10:00 | 20% |
| 10:01 | 24% |
| 10:02 | 31% |
| 10:03 | 45% |
| 10:04 | 38% |

Every metric contains:

- A Timestamp
- A Value

This combination is called **Time-Series Data**.

---

## 6. What is a Time Series Database (TSDB)?

A **Time Series Database (TSDB)** is a database specifically designed to store timestamped data efficiently.

Example:

| Timestamp | CPU |
|-----------|----:|
| 10:00 | 20 |
| 10:01 | 24 |
| 10:02 | 31 |

Prometheus comes with its own built-in **Time Series Database (TSDB)**.

Because of this, Prometheus does **not** require databases like:

- MySQL
- PostgreSQL
- Oracle

to store monitoring metrics.

---

## 7. Why Prometheus?

Prometheus is responsible for:

- Collecting Metrics
- Storing Metrics
- Querying Metrics using PromQL
- Triggering Alerts

Think of Prometheus as the **Monitoring Engine**.

---

## 8. Why Grafana?

Prometheus stores numerical data.

Example:

```text
CPU = 35%
Memory = 62%
Pods = 18
```

Although useful, raw numbers are difficult to analyze.

Grafana connects to Prometheus and converts those numbers into visual dashboards.

Grafana provides:

- Line Charts
- Bar Charts
- Gauges
- Tables
- Dashboards

Think of Grafana as the **Visualization Layer**.

---

## High-Level Architecture

```text
                  Kubernetes Cluster
                 ┌──────────────────┐
                 │                  │
                 │      Nodes       │
                 │       Pods       │
                 │    Containers    │
                 └────────┬─────────┘
                          │
                        Metrics
                          │
                          ▼
                 ┌──────────────────┐
                 │    Prometheus    │
                 │                  │
                 │ Collects Metrics │
                 │  Stores Metrics  │
                 └────────┬─────────┘
                          │
                     PromQL Queries
                          │
                          ▼
                 ┌──────────────────┐
                 │     Grafana      │
                 │                  │
                 │    Dashboards    │
                 │      Charts      │
                 └──────────────────┘
```

---

## Summary

After completing this module, you should understand:

- ✅ What Monitoring is
- ✅ Why Monitoring is Needed
- ✅ Monitoring vs Logging
- ✅ What Metrics are
- ✅ What a Time Series is
- ✅ What a Time Series Database (TSDB) is
- ✅ Why Prometheus is Used
- ✅ Why Grafana is Used

---

## Next Module

**Module 2 – Prometheus Architecture**

Topics:

- Prometheus Components
- Exporters
- Node Exporter
- kube-state-metrics
- Service Discovery
- Targets
- Pull vs Push Model
- Alertmanager