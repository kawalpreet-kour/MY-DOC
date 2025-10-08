# Documentation on Alerting Rules, Severity Levels, Notification Channels & Escalation Process for App Monitoring using Alertmanager

<img width="295" height="171" alt="download" src="https://github.com/user-attachments/assets/55453275-9b9e-4c78-a401-d0906df0960f" />

---

## Author Information

| Last Updated On | Version | Author          | Level           | Reviewer       |
| --------------- | ------- | --------------- | --------------- | -------------- |
| 08-10-2025      | V1.2    | Kawalpreet Kour | Internal Review | Sharvari       |
|                 |         | Kawalpreet Kour | L0              | Shreya         |
|                 |         | Kawalpreet Kour | L1              | Abhishek V     |
|                 |         | Kawalpreet Kour | L2              | Abhishek Dubey |

---

<details>
  <summary><h2><strong>Table of Contents</strong></h2></summary>

1. [Introduction](#introduction)
2. [What Are Alerting Rules?](#what-are-alerting-rules)
3. [Severity Levels](#severity-levels)
4. [Notification Channels](#notification-channels)
5. [Escalation Process](#escalation-process)
6. [Process of App Monitoring using Alertmanager](#process-of-app-monitoring-using-alertmanager)
7. [Common Alert Rules for Applications](#common-alert-rules-for-applications)
8. [Advantages of Alerting](#advantages-of-alerting)
9. [Limitations and Challenges](#limitations-and-challenges)
10. [Best Practices for Alerting](#best-practices-for-alerting)
11. [Conclusion](#conclusion)
12. [FAQs](#faqs)
13. [Contact Information](#contact-information)
14. [References](#references)

</details>

---

## Introduction

Application monitoring ensures the health, performance, and availability of services.
**Alerting rules** act like an early warning system—detecting anomalies and notifying responsible teams before users are affected.
**Alertmanager**, integrated with **Prometheus**, automates alert routing, grouping, and escalation through defined notification channels and severity levels.

---

## What is Alert Manager?

**Alertmanager** is a component of the Prometheus monitoring stack that manages alerts by grouping, deduplicating, silencing, and routing them. It ensures that notifications reach the right teams through channels like Email, Slack, PagerDuty, or Webhooks, making alerts actionable and reducing noise.

---
## Process of App Monitoring using Alertmanager

| Step  | Stage                        | Description                                                                 |
| ----- | ---------------------------- | --------------------------------------------------------------------------- |
| **1** | **Metrics Collection**       | Prometheus scrapes metrics from app and infra (CPU, memory, response time). |
| **2** | **Rule Evaluation**          | Alerting rules are evaluated periodically (defined in YAML).                |
| **3** | **Alert Triggering**         | If threshold is breached, Prometheus triggers an alert.                     |
| **4** | **Alert Grouping & Routing** | Alertmanager groups and routes alerts based on labels (e.g., severity).     |
| **5** | **Notification Dispatch**    | Alerts sent to Slack, Email, or PagerDuty as per configuration.             |
| **6** | **Escalation Handling**      | If not acknowledged, alerts are auto-escalated per escalation policy.       |
| **7** | **Resolution & Review**      | Once resolved, alerts auto-close and RCA is performed.                      |

---
## What Are Alerting Rules?

Alerting rules are predefined conditions in Prometheus that continuously evaluate metrics.
When a defined threshold is breached, an alert is generated and sent to **Alertmanager**, which processes and routes it to appropriate channels.

---

## Common Alert Rules for Applications

| Alert Rule                 | Condition / Threshold Example | Severity | Notification Channel | Escalation        |
| -------------------------- | ----------------------------- | -------- | -------------------- | ----------------- |
| **High CPU Usage**         | CPU > 80% for 5 min           | High     | Slack / PagerDuty    | L1 → L2 after 15m |
| **Memory Utilization**     | Memory > 90%                  | Critical | PagerDuty / SMS      | Immediate to L2   |
| **Service Down**           | Health check fail for 1 min   | Critical | Email + Slack        | L1 → L2 instantly |
| **High Error Rate**        | HTTP 5xx > 5%                 | Critical | Slack / Email        | L1 → L2 (10m)     |
| **High Latency**           | Response time > 2s            | Medium   | Slack                | L1 only           |
| **Disk Space Low**         | Disk usage > 85%              | High     | Email                | L1 → L2 (20m)     |
| **DB Connection Failures** | > 50 errors/min               | Critical | PagerDuty            | Immediate         |
| **Queue Lag**              | Queue length > threshold      | Medium   | Slack                | L1 only           |
| **App Restart Detected**   | Restart count > 3/hr          | Low      | Email                | L1 review daily   |

---



---


## Advantages of Alerting

| Advantage                    | Description                                  |
| ---------------------------- | -------------------------------------------- |
| **Faster Incident Response** | Alerts reach the right team instantly.       |
| **Reduced Downtime**         | Quick detection = quicker recovery.          |
| **Improved Visibility**      | Real-time health view of apps.               |
| **Automated Escalations**    | No manual tracking for unresolved alerts.    |
| **Actionable Insights**      | Alerts include details for immediate action. |

---



## Best Practices for Alerting

 Use **severity labels** consistently.
 Define **realistic thresholds** using historical data.
 Configure **grouping and inhibition rules** in Alertmanager.
 Integrate with **Slack/PagerDuty** for immediate visibility.
 Regularly review **false alerts** and refine rules.
 Perform **RCA** after each critical incident.

---

## Conclusion

**Prometheus + Alertmanager** together enable intelligent, automated, and structured alerting.
With clearly defined **alert rules**, **severity levels**, **notification channels**, and **escalation policies**, teams can ensure proactive monitoring, faster response, and minimal downtime.

---
