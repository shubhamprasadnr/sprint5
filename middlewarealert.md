# 🚨 Alerting Rules & Process for Redis Monitoring
| Author  | Created on | Version   | Last Edited On | Comment  | Reviewer |
|---------|------------|-----------|----------------|-------------------|---------------|
| Shubham | 07-07-25   |  version1| 07-07-25       | Internal Review    |Siddhath |
| Shubham | 07-07-25  |  version1|-   | L0  Review  | Gaurav Singla |
| Shubham | 07-07-25  |  version1| -     | L1  Review | Rahul Gupta |
| Shubham | 07-07-25   |  version1| -      | L2  Review  | Mahesh Kumar|


This document defines Redis-specific **alert rules**, **severity levels**, **notification channels**, and the **escalation process** used to monitor and respond to issues in a Redis-based middleware environment.

---

## 📚 Table of Contents

- [Objectives](#-objectives)
- [Redis Alert Rules](#️-redis-alert-rules)
- [Severity Levels](#-severity-levels)
- [Notification Channels](#-notification-channels)
- [Alert Routing Example](#-alert-routing-example)
- [Escalation Process](#-escalation-process)
- [Best Practices](#-best-practices)
- [Escalation Process](#-escalation-process)
- [Contact Information](#-contact-information)


---

## 🎯 Objectives

- Detect Redis performance and availability issues early
- Define actionable alerts with severity
- Notify responsible teams and ensure quick resolution
- Document clear escalation paths

---

## ⚠️ Redis Alert Rules

| **Alert Name**             | **Condition (PromQL or Description)**                             | **Severity** | **Description**                                 |
|----------------------------|--------------------------------------------------------------------|--------------|-------------------------------------------------|
| `RedisInstanceDown`        | `up{job="redis"} == 0`                                             | critical     | Redis server is unreachable                     |
| `RedisMemoryUsageHigh`     | `redis_memory_used_bytes / redis_total_system_memory_bytes > 0.85`| warning      | Redis memory usage exceeds 85%                  |
| `RedisEvictedKeys`         | `increase(redis_evicted_keys_total[5m]) > 0`                       | warning      | Keys are being evicted due to memory pressure   |
| `RedisBlockedClients`      | `redis_blocked_clients > 0`                                        | warning      | Blocking operations detected                    |
| `RedisReplicationLagHigh`  | `redis_replication_lag_seconds > 2`                                | critical     | Replica is lagging behind master                |
| `RedisAOFWriteError`       | `redis_aof_last_write_status != "ok"`                              | critical     | Append-only file (AOF) write issue              |
| `RedisRDBSaveFailure`      | `redis_rdb_last_bgsave_status != "ok"`                             | critical     | Snapshot save failed                            |
| `RedisKeyspaceMissRate`    | `rate(redis_keyspace_misses_total[5m]) / rate(redis_keyspace_hits_total[5m]) > 0.1` | warning | Cache miss rate is higher than 10%             |
| `RedisConnectionsHigh`     | `redis_connected_clients > 500` (example threshold)                | warning      | High number of client connections               |
| `RedisUptimeReset`         | `increase(redis_uptime_in_seconds[1h]) < 60`                       | critical     | Redis server restarted                          |

---

## 🛑 Severity Levels

| **Severity** | **Definition**                                         | **Action Required**         |
|--------------|--------------------------------------------------------|-----------------------------|
| `critical`   | Redis is down or data durability is at risk            | Immediate paging of on-call |
| `warning`    | Redis performance degraded or nearing limit            | Notify DevOps/Infra team    |
| `info`       | Informational alert, trends or minor issues            | Optional alert/logging      |

---

## 📨 Notification Channels

| **Channel**        | **Used For Severities** | **Tool/Platform**         | **Purpose**                      |
|--------------------|--------------------------|-----------------------------|----------------------------------|
| Email              | info, warning            | SES, Gmail, Mailgun         | Low-severity awareness           |
| Slack/Teams        | warning, critical        | Slack Webhook, MS Teams Bot | Fast team communication          |
| PagerDuty/Opsgenie | critical                 | PagerDuty/Opsgenie API      | On-call escalation               |
| Webhook/API        | all                      | JIRA, ServiceNow, Custom API| Auto-ticket creation             |

---

## 📈 Alert Routing Example (Alertmanager)

```yaml
route:
  group_by: ['alertname', 'severity']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 3h
  receiver: 'default-receiver'

  routes:
    - match:
        severity: 'critical'
      receiver: 'pagerduty-team'

    - match:
        severity: 'warning'
      receiver: 'slack-redis-monitoring'

    - match:
        severity: 'info'
      receiver: 'email-infra-team'
```
## 🆘 Escalation Process

| **Time Elapsed** | **Action**                        | **Responsible**         |
|------------------|-----------------------------------|--------------------------|
| Immediate        | Alert triggered via Alertmanager  | Redis on-call engineer  |
| +10 min          | Escalate to Infra Lead            | L2 / Redis SME           |
| +30 min          | Escalate to SRE Manager           | Infra/SRE Manager        |
| +1 hr            | Trigger incident call             | All stakeholders         |

##  Contact Information

| Name | Email Address |
|------|---------------|
| Shubham Prasad | [shubham.prasad.snaatak@mygurukulam.co](mailto:shubham.prasad.snaatak@mygurukulam.co) |
