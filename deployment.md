# 🚀 Deployment Strategies Comparison

| Author  | Created on | Version   | Last Edited On | Comment  | Reviewer |
|---------|------------|-----------|----------------|-------------------|---------------|
| Shubham | 07-07-25   |  version1| 07-07-25       | Internal Review    |Siddhath |
| Shubham | 07-07-25  |  version1|-   | L0  Review  | Gaurav Singla |
| Shubham | 07-07-25  |  version1| -     | L1  Review | Rahul Gupta |
| Shubham | 07-07-25   |  version1| -      | L2  Review  | Mahesh Kumar|


This document compares **Rolling**, **Blue/Green**, and **Canary** deployment strategies including definitions, pros, cons, and recommended use cases.

---

## 📚 Table of Contents
- [ Comparison Table](#-comparison-table)
- [ Pros and  Cons](#-pros-and--cons)
- [Recommendations](#-recommendations)
- [Contact Information](#-contact-information)

---

## 📊 Comparison Table

| **Criteria**               | **Rolling Deployment**                                      | **Blue/Green Deployment**                                     | **Canary Deployment**                                           |
|---------------------------|--------------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------|
| **Definition**             | Updates are applied incrementally across instances           | Switches traffic between two identical environments (blue & green) | Releases new version to a small subset of users first           |
| **Downtime**              | Minimal to none                                              | Zero (if done properly)                                        | Minimal to none                                                |
| **Risk of Failure**        | Medium (partial rollback may be tricky)                     | Low (easy rollback to previous version)                        | Low (affects only subset initially)                            |
| **Rollback Strategy**     | Gradual rollback per instance                                | Instant switch back to blue environment                        | Redirect traffic back to stable version                        |
| **Traffic Distribution**  | Uniform over time                                            | All traffic switched at once                                   | Small % of traffic, gradually increased                        |
| **Environment Requirement** | Single set of infrastructure                                 | Two complete environments required                             | One environment with traffic control mechanism                 |
| **Monitoring Required**   | Basic monitoring                                             | Basic (mostly during switch)                                   | Intensive monitoring and metrics                               |
| **Resource Usage**        | Efficient (no duplicate resources)                           | High (duplicate resources during deployment)                   | Moderate (extra resources for limited users)                   |
| **Deployment Speed**      | Slower                                                       | Faster (instant switch)                                        | Slower (depends on traffic ramp-up plan)                       |
| **Complexity**            | Low to medium                                                | Medium                                                         | High (requires automation and precise traffic control)         |
| **Best For**              | Large, distributed systems with many nodes                   | High availability systems needing zero-downtime and instant rollback | Risk-sensitive applications, A/B testing, phased rollouts      |
| **Example Tools**         | Kubernetes, Ansible                                          | AWS Elastic Beanstalk, NGINX, Route 53                         | Istio, Argo Rollouts, LaunchDarkly                             |

---

## ✅ Pros and ❌ Cons

| **Strategy**     | ✅ **Pros**                                                                 | ❌ **Cons**                                                                 |
|------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Rolling**      | - No need for duplicate infrastructure  <br> - Minimal downtime  <br> - Resource efficient  <br> - Works well with Kubernetes | - Rollback is complex  <br> - Slower deployment  <br> - Failures affect partial traffic |
| **Blue/Green**   | - Zero downtime  <br> - Easy rollback  <br> - Full staging before release  <br> - Safe for critical systems | - High infrastructure cost  <br> - Complex traffic switch setup |
| **Canary**       | - Limits exposure  <br> - Supports A/B testing  <br> - Detects issues early  <br> - Safer for new features | - Requires automation and monitoring  <br> - Slow rollout  <br> - Complex traffic management |

---

## 📝 Recommendations

| **Use Case Scenario**                                  | **Recommended Strategy** |
|--------------------------------------------------------|---------------------------|
| Quick fixes with minimal resources                     | Rolling                  |
| Business-critical apps with zero downtime needs        | Blue/Green               |
| Feature testing and phased rollouts                    | Canary                   |
| Budget constraints and single-environment apps         | Rolling                  |
| Instant rollback with separate prod/stage environments | Blue/Green               |
| Safe rollout with real user feedback                   | Canary                   |

##  Contact Information

| Name | Email Address |
|------|---------------|
| Shubham Prasad | [shubham.prasad.snaatak@mygurukulam.co](mailto:shubham.prasad.snaatak@mygurukulam.co) |
