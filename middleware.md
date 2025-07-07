# 🔍 Redis Middleware Monitoring – Key Performance Metrics & Requirements

| Author  | Created on | Version   | Last Edited On | Comment  | Reviewer |
|---------|------------|-----------|----------------|-------------------|---------------|
| Shubham | 07-07-25   |  version1| 07-07-25       | Internal Review    |Siddhath |
| Shubham | 07-07-25  |  version1|-   | L0  Review  | Gaurav Singla |
| Shubham | 07-07-25  |  version1| -     | L1  Review | Rahul Gupta |
| Shubham | 07-07-25   |  version1| -      | L2  Review  | Mahesh Kumar|

This document outlines essential Redis performance metrics, their definitions, thresholds, and how to monitor them effectively using tools like **Prometheus**, **Grafana**, and **Redis Exporter**.

---

## 📚 Table of Contents

- [Introduction](#-introduction)
- [Key Redis Performance Metrics](#-key-redis-performance-metrics)
- [Monitoring Requirements](#-monitoring-requirements)
- [Best Practices](#-best-practices)
- [Conclusion](#-conclusion)
- [Contact Information](#-contact-information)

---

## 🚀 Introduction

Redis is a high-performance, in-memory key-value store often used as a **cache**, **session store**, or **message broker**. Monitoring Redis helps ensure **low latency**, **data durability**, and **resource optimization**.

---

## 📊 Key Redis Performance Metrics

| **Metric**                  | **Definition**                                                | **Recommended Threshold**           | **Monitoring Tools**                     |
|-----------------------------|---------------------------------------------------------------|--------------------------------------|------------------------------------------|
| **used_memory**             | Total memory used by Redis                                   | < 75–80% of total system memory      | Redis Exporter, INFO command             |
| **connected_clients**       | Number of active client connections                          | Depends on `maxclients` config       | Redis Exporter, INFO                     |
| **instantaneous_ops_per_sec** | Number of operations per second                              | Track baseline for anomalies         | Redis Exporter                           |
| **keyspace_hits / misses**  | Cache efficiency (hits vs misses)                            | Hit rate > 90% preferred             | Redis INFO command                       |
| **evicted_keys**            | Number of keys evicted due to memory limit                   | Should be zero in optimal config     | Redis Exporter                           |
| **blocked_clients**         | Number of clients waiting on blocking operations             | Should be close to 0                 | Redis Exporter                           |
| **expired_keys**            | Number of keys expired due to TTL                            | Track for trends                     | INFO stats                               |
| **used_cpu_sys / used_cpu_user** | CPU usage by Redis in system/user mode                     | < 70% CPU utilization                 | Redis Exporter                           |
| **rdb_last_bgsave_status**  | Status of last background RDB save                           | Should be "ok"                       | Redis INFO, Alertmanager                 |
| **aof_last_write_status**   | Status of last AOF write                                     | Should be "ok"                       | Redis INFO                               |
| **replication_lag**         | Lag between master and replica in seconds                    | < 1s preferred                       | Redis INFO replication metrics           |
| **uptime_in_seconds**       | Redis server uptime                                          | N/A (used to detect restarts)        | Redis Exporter, Alert on restart         |
| **connected_slaves**        | Number of connected replicas                                 | Should match expected count          | Redis INFO                               |

---

## ✅ Monitoring Requirements

| **Component**         | **Tool / Source**                        |
|-----------------------|------------------------------------------|
| **Metrics Collector** | Redis Exporter + Prometheus              |
| **Visualization**     | Grafana Redis Dashboard                  |
| **Alerting**          | Alertmanager, PagerDuty/Opsgenie         |
| **Logging**           | Redis logs, syslog integration           |
| **Health Check**      | TCP ping on port `6379`, or sentinel API |
| **Failover Detection**| Sentinel metrics or Redis cluster state  |

---

## 🧠 Best Practices

- 🔒 Enable **authentication (AUTH)** and **TLS** for production use
- ⚖️ Monitor **key eviction** to tune max memory policies
- 📈 Set **alerts on increasing memory/cpu/latency trends**
- 🧪 Regularly test **backup (RDB/AOF) restore** procedures
- 🛑 Use **persistence mode (AOF/RDB)** suitable for your data criticality

---

## 🔚 Conclusion

Monitoring Redis ensures high availability and fast response times in middleware-heavy environments. Combining **metrics, logs, and alerting** builds a full picture of Redis health.

---
##  Contact Information

| Name | Email Address |
|------|---------------|
| Shubham Prasad | [shubham.prasad.snaatak@mygurukulam.co](mailto:shubham.prasad.snaatak@mygurukulam.co) |
