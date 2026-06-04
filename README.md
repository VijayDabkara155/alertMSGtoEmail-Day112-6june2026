# Day 112 - Prometheus Alertmanager Email & Slack Notifications

## 📌 Project Overview

This project demonstrates how to configure **Prometheus Alertmanager** to send alerts through:

* 📧 Email Notifications (Gmail SMTP)
* 💬 Slack Notifications (Incoming Webhook)

The monitoring stack is deployed on Kubernetes and includes custom Prometheus alert rules that trigger notifications when alerts fire.

---

## 🚀 Technologies Used

* Kubernetes
* Prometheus
* Alertmanager
* Slack Incoming Webhooks
* Gmail SMTP
* YAML Configuration

---

## 📂 Project Structure

```bash
.
├── alertmanager-config.yaml
├── alertmanager-deployment.yaml
├── alertmanager-service.yaml
├── prometheus-config.yaml
├── prometheus-deployment.yaml
├── prometheus-service.yaml
├── alerts.yml
└── README.md
```

---

## ⚙️ Features

### Email Notifications

Alertmanager sends email alerts using Gmail SMTP whenever an alert is triggered.

Example alert:

* High CPU Usage
* High Memory Usage
* AlwaysFiring Test Alert

---

### Slack Notifications

Alertmanager integrates with Slack using Incoming Webhooks and posts alerts directly to a Slack channel.

Example Slack message:

```text
[FIRING] AlwaysFiring
Severity: Critical
Description: Slack integration test
```

---

## 🔔 Custom Alert Rules

### AlwaysFiring Test Alert

```yaml
- alert: AlwaysFiring
  expr: vector(1)
  for: 1m
```

### High CPU Usage

```yaml
- alert: HighCPUUsage
  expr: 100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100) > 80
  for: 1m
```

### High Memory Usage

```yaml
- alert: HighMemoryUsage
  expr: |
    (1 - (node_memory_Mem_Available_bytes / node_memory_MemTotal_bytes)) * 100 > 80
  for: 1m
```

---

## 🛠️ Deployment

Apply all manifests:

```bash
kubectl apply -f .
```

Verify resources:

```bash
kubectl get pods -n monitoring
kubectl get svc -n monitoring
```

---

## 🔍 Verify Alertmanager

Port-forward Alertmanager:

```bash
kubectl port-forward svc/alertmanager 19093:9093 -n monitoring
```

Check status:

```bash
curl http://localhost:19093/api/v2/status
```

View active alerts:

```bash
curl http://localhost:19093/api/v2/alerts
```

---

## 📸 Expected Outcome

When an alert is triggered:

✅ Alert appears in Prometheus

✅ Alert is routed to Alertmanager

✅ Slack notification is delivered

✅ Email notification is sent

---

## 🔒 Security Note

Secrets such as:

* Gmail App Passwords
* Slack Webhook URLs

should never be committed to Git repositories.

Use:

* Kubernetes Secrets
* Environment Variables
* External Secret Managers

for production deployments.

---

## 📚 Learning Outcomes

Through this project, I learned:

* Prometheus Alerting Rules
* Alertmanager Configuration
* Slack Integration
* Gmail SMTP Configuration
* Kubernetes Monitoring
* Troubleshooting Alert Delivery
* Notification Routing

---

## 👨‍💻 Author

**Vijay Dabkara**

DevOps Engineer | AWS | Docker | Kubernetes | Terraform | Linux

GitHub: https://github.com/VijayDabkara155

---

### Day 112 of My DevOps Journey 🚀

Building production-style monitoring and alerting systems using Prometheus and Alertmanager.
