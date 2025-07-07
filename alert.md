# 🚨 Alerting Rules & Process for App Monitoring using Alertmanager
| Author  | Created on | Version   | Last Edited On | Comment  | Reviewer |
|---------|------------|-----------|----------------|-------------------|---------------|
| Shubham | 07-07-25   |  version1| 07-07-25       | Internal Review    |Siddhath |
| Shubham | 07-07-25  |  version1|-   | L0  Review  | Gaurav Singla |
| Shubham | 07-07-25  |  version1| -     | L1  Review | Rahul Gupta |
| Shubham | 07-07-25   |  version1| -      | L2  Review  | Mahesh Kumar|

This document outlines the standard **alerting strategy** for application monitoring using **Prometheus + Alertmanager**. It includes defined **alert rules**, **severity levels**, **notification channels**, and the **escalation process**.

---

## 📚 Table of Contents

- [Objectives](#-objectives)
- [Alert Rules](#️-alert-rules)
- [Severity Levels](#-severity-levels)
- [Notification Channels](#-notification-channels)
- [Alert Routing & Grouping](#-alert-routing--grouping)
- [Escalation Process](#-escalation-process)
- [Best Practices](#-best-practices)
- [Contact Information](#-contact-information)

---

## 🎯 Objectives

- Detect issues in the application stack proactively
- Classify and prioritize alerts by **severity**
- Notify appropriate **stakeholders or on-call teams**
- Automate **escalation** for unresolved critical issues

---

## ⚠️ Alert Rules

| **Alert Name**              | **Expression (PromQL)**                                      | **Severity** | **Description**                         |
|----------------------------|--------------------------------------------------------------|--------------|-----------------------------------------|
| High CPU Usage             | `avg(node_cpu_seconds_total{mode="user"}) > 0.8`             | warning      | CPU usage over 80%                      |
| App Down                   | `up{job="app"} == 0`                                          | critical     | Application instance not responding     |
| High Memory Usage          | `node_memory_Active_bytes / node_memory_MemTotal_bytes > 0.85` | warning      | Memory usage > 85%                      |
| High Error Rate            | `rate(http_requests_total{status=~"5.."}[5m]) > 0.05`         | critical     | 5xx errors exceed 5%                    |
| DB Latency High            | `avg(db_query_duration_seconds{job="db"}) > 0.2`              | warning      | Query time > 200ms                      |
| Pod CrashLoopBackOff       | `kube_pod_container_status_waiting_reason{reason="CrashLoopBackOff"} > 0` | critical | Pod is in CrashLoopBackOff             |
| Disk Space Low             | `(node_filesystem_avail_bytes / node_filesystem_size_bytes) < 0.15` | warning | Disk space available < 15%             |

---

## 🛑 Severity Levels

| **Severity** | **Definition**                                           | **Action Required**                  |
|--------------|----------------------------------------------------------|--------------------------------------|
| `critical`   | Immediate threat to availability or stability            | Page on-call engineer                |
| `warning`    | Performance degradation or approaching threshold         | Monitor and investigate              |
| `info`       | Informational alerts for awareness                       | Log only or notify via low-priority  |

---

## 📨 Notification Channels

| **Channel**      | **Purpose**                    | **Used For Severities** | **Tools**                    |
|------------------|--------------------------------|---------------------------|------------------------------|
| Email            | General notification           | warning, info             | SMTP, Mailgun, SES           |
| Slack/Teams      | Team alerts & collaboration    | info, warning, critical   | Slack Webhooks, MS Teams     |
| PagerDuty        | Critical issue paging          | critical                  | PagerDuty integration        |
| Opsgenie         | Escalation & on-call management| critical                  | Opsgenie API/Webhook         |
| Webhooks         | Integration with ticketing tools| all                       | JIRA, ServiceNow, custom API |

---

## 📈 Alert Routing & Grouping

### 📦 **Grouping Rules**
Alerts are grouped by:
- `alertname`
- `severity`
- `job` or `service`

This avoids alert storms during outages and provides context-aware notifications.

### 🔀 **Routing Example (in `alertmanager.yml`)**

```yaml
route:
  group_by: ['alertname', 'job']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 4h
  receiver: 'default-notification'

  routes:
    - match:
        severity: 'critical'
      receiver: 'pagerduty-team'

    - match:
        severity: 'warning'
      receiver: 'slack-dev-team'

##  Contact Information

| Name | Email Address |
|------|---------------|
| Shubham Prasad | [shubham.prasad.snaatak@mygurukulam.co](mailto:shubham.prasad.snaatak@mygurukulam.co) |
