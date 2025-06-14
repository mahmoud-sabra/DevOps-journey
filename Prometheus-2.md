## **📌 1. Metrics**

**Definition:**  
Metrics are numerical values collected over time that describe the state and performance of a system. They help in tracking resource utilization, errors, request rates, and other key performance indicators (KPIs).

**🔹 Examples:**

- **CPU Usage** 
- **Memory Usage** 
- **HTTP Requests** 
- **Disk I/O Operations** 


---

## **📌 2. Events**

**Definition:**  
Events are discrete occurrences that happen at specific points in time. Unlike metrics, which are continuous and numerical, events capture **what happened and when**.

**🔹 Examples:**

- **Server Restarted** at `2025-03-12 12:30:00`
- **Application Crashed** due to an `OutOfMemory` error
- **User Login** event
- **Database Backup Completed** at a certain timestamp

**🔹 Prometheus and Events:**

- Prometheus is **not event-driven**; it primarily collects **time-series metrics**.
- If you need event-based monitoring, you should integrate **logs or event-driven tools like Loki, Elasticsearch, or Kafka**.

---

## **📌 3. Logs**

**Definition:**  
Logs are **detailed textual records** of system activity. They capture what’s happening in an application or system **at a granular level**.

**🔹 Examples:**

- `2025-03-12 12:31:45 ERROR: Database Connection Failed`
- `INFO: User 'admin' logged in from IP 192.168.1.100`
- `DEBUG: Request received at /api/orders`

**🔹 Difference Between Logs & Metrics:**

| Aspect        | Logs                 | Metrics                     |
| ------------- | -------------------- | --------------------------- |
| **Data Type** | Textual              | Numerical                   |
| **Storage**   | Log files, databases | Time-series database (TSDB) |
| **Use Case**  | Debugging & tracing  | Performance monitoring      |

🔹 **Prometheus doesn’t store logs** → Use **Grafana Loki** for logs alongside Prometheus.

---

## **📌 4. Dashboards**

**Definition:**  
Dashboards are **visual representations** of collected metrics. They help in analyzing trends, detecting anomalies, and making data-driven decisions.

**🔹 Examples:**

- **Grafana Dashboards** showing CPU usage over time.
- **Prometheus Web UI** displaying real-time HTTP request rates.
- **Kibana Dashboards** for log analysis.

**🔹 Common Tools for Dashboards:**

- **Grafana** (best for Prometheus visualization)
- **Kibana** (for logs with Elasticsearch)
- **Thanos UI** (for large-scale Prometheus setups)

---

## **📌 5. Job in Prometheus**

**Definition:**  
A **job** in Prometheus is a **logical grouping of targets (instances) that need to be monitored**.

**🔹 Example:**

```
scrape_configs:
  - job_name: "node_exporter"
    static_configs:
      - targets: ["192.168.1.10:9100", "192.168.1.11:9100"]

```

- Here, `"node_exporter"` is the **job name**.
- It includes **multiple instances (targets)** that provide system metrics.

**🔹 Types of Jobs:**

1. **Node Exporter Job** → Collects system metrics from Linux servers.
2. **Kubernetes Job** → Monitors Kubernetes components.
3. **Application Job** → Scrapes metrics from a web app.

---

## **📌 6. Instance in Prometheus**

**Definition:**  
An **instance** is a single **target (server, application, or service)** that Prometheus scrapes metrics from.

**🔹 Example:**  
If you have **two servers** running `node_exporter`:

```
scrape_configs:
  - job_name: "node_exporter"
    static_configs:
      - targets: ["192.168.1.10:9100", "192.168.1.11:9100"]

```

## PromQL (Prometheus Query Language)
**PromQL (Prometheus Query Language)** is a powerful language used in **Prometheus** to query, filter, and aggregate time-series data. It enables users to extract insights from collected metrics and visualize them in dashboards like **Grafana**.
```
# Instant Vector Example (Current CPU usage per instance)
node_cpu_seconds_total

# Range Vector Example (CPU usage over the last 5 minutes)
node_cpu_seconds_total[5m]

# Scalar Example (Dividing two metric values)
up / 2

```