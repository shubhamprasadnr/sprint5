
# 📈 Designing App Monitoring  
| Author  | Created on | Version   | Last Edited On | Comment  | Reviewer |
|---------|------------|-----------|----------------|-------------------|---------------|
| Shubham | 07-07-25   |  version1| 07-07-25       | Internal Review    |Siddhath |
| Shubham | 07-07-25  |  version1|-   | L0  Review  | Gaurav Singla |
| Shubham | 07-07-25  |  version1| -     | L1  Review | Rahul Gupta |
| Shubham | 07-07-25   |  version1| -      | L2  Review  | Mahesh Kumar|

## Identify Key Performance Metrics and Requirements

This document outlines **critical application performance metrics**, their **definitions**, **thresholds**, and **monitoring requirements** to design a robust application monitoring system.

---

## 📚 Table of Contents

- [🚀 Introduction](#-introduction)
- [📊 Key Application Performance Metrics](#-key-application-performance-metrics)
- [✅ Monitoring Requirements](#-monitoring-requirements)
- [🔍 Conclusion](#-conclusion)
- [🔍 Contact Information](#-contact-information)

---

## 🚀 Introduction

Application monitoring is crucial for ensuring system reliability, performance, and user satisfaction. This guide identifies the essential metrics every application should track, with thresholds and tool-specific guidance.

---

## 📊 Key Application Performance Metrics

| **Metric**                   | **Definition**                                                                 | **Recommended Threshold**                         | **Monitoring Requirement**                                             |
|-----------------------------|---------------------------------------------------------------------------------|--------------------------------------------------|------------------------------------------------------------------------|
| **Response Time (Latency)** | Time taken for the app to respond to a request                                | < 200ms for UI, < 500ms for APIs                  | Use APM tools (e.g., New Relic, Datadog) with alerting on spikes       |
| **Error Rate**              | % of failed requests over total requests                                       | < 1%                                             | Monitor via logs, APMs, and HTTP status codes                          |
| **Throughput (RPS/QPS)**    | Requests per second (or queries per second) handled by the application         | App-specific (baseline + 20%)                    | Monitor using Prometheus, CloudWatch, or App Insights                  |
| **CPU Usage**               | Percentage of CPU resources being utilized                                     | < 70% average                                   | Use system metrics monitoring (e.g., Grafana + Node Exporter)          |
| **Memory Usage**            | Percentage of memory consumed by the app                                       | < 75% average                                   | Enable memory profiling or use container metrics (cAdvisor, Prometheus)|
| **Disk I/O**                | Disk read/write speed or queue length                                           | < 80% disk utilization                          | Use cloud or OS-level monitoring tools                                 |
| **Database Query Time**     | Average execution time of DB queries                                           | < 200ms/query                                  | Enable slow query logs; monitor with DB-specific tools                 |
| **Request Count**           | Total number of requests received by the app                                   | N/A (used for scaling)                          | Track using access logs or built-in metrics of your web server         |
| **Availability/Uptime**     | Percentage of time the application is available                                | > 99.9% (three nines)                           | Use synthetic monitoring (e.g., Pingdom, UptimeRobot)                  |
| **Garbage Collection Time** | Time spent by the JVM/Runtime in memory cleanup                                | < 5% of CPU time                                | Use JVM/Node.js profilers depending on language                        |
| **Thread Count**            | Number of threads in use by the application                                    | Should not exceed max thread pool                | Use profilers or thread dump analysis tools                            |
| **Queue Length**            | Length of internal queues like job queues or message brokers                   | App-specific (should be close to 0 under normal load) | Monitor using messaging systems (Kafka, RabbitMQ, etc.)             |
| **Container Health**        | Status of containerized applications (crashes, restarts)                       | 0 restarts preferred                            | Use Docker metrics, Kubernetes probes (liveness/readiness)             |
| **Network Latency**         | Round-trip time between components/services                                     | < 100ms preferred                              | Use ping checks or service mesh observability                          |
| **Session Duration**        | Average time a user remains active on the application                          | Depends on app purpose                          | Useful for engagement analysis; captured via frontend tools            |

---

## ✅ Monitoring Requirements

| **Category**           | **Tool Recommendations**                                                                 |
|------------------------|-------------------------------------------------------------------------------------------|
| **Infrastructure**     | Prometheus + Grafana, Datadog Infrastructure, CloudWatch                                 |
| **Application Layer**  | New Relic, AppDynamics, Dynatrace, Elastic APM                                            |
| **Logs & Errors**      | ELK Stack, Graylog, Sentry, Splunk                                                        |
| **Synthetic Monitoring** | Pingdom, Uptime Robot, Grafana Synthetic Monitoring Plugin                              |
| **Container/K8s**      | cAdvisor, kube-state-metrics, Prometheus Operator, Lens, K9s                             |
| **Database**           | pg_stat_statements (PostgreSQL), Percona Toolkit, Cloud SQL Insights, APM DB tracing     |
| **Alerts & Notifications** | Grafana Alerting, PagerDuty, Opsgenie, VictorOps, Slack/Webhooks integrations       |

---

## 🔍 Conclusion

Designing a reliable monitoring system involves not just collecting data but setting meaningful **thresholds**, **visualizing trends**, and **triggering alerts**. Regular reviews and adjustments are necessary to adapt to changing app behaviors and usage patterns.

---


##  Contact Information

| Name | Email Address |
|------|---------------|
| Shubham Prasad | [shubham.prasad.snaatak@mygurukulam.co](mailto:shubham.prasad.snaatak@mygurukulam.co) |
