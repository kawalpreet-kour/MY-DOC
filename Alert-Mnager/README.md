# Documentation on Alerting Rules Process for App Monitoring using Alertmanager

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
2. [What is Alertmanager?](#what-is-alertmanager)
3. [What Are Alerting Rules?](#what-are-alerting-rules)
4. [Common Alert Rules for Applications](#common-alert-rules-for-applications)
5. [Severity Levels](#severity-levels)
6. [Notification Channels](#notification-channels)
7. [Escalation Process](#escalation-process)
8. [Process of App Monitoring using Alertmanager](#process-of-app-monitoring-using-alertmanager)
9. [Advantages of Alerting](#advantages-of-alerting)
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

## What is Alertmanager?

**Alertmanager** is a component of the Prometheus monitoring stack that manages alerts by grouping, deduplicating, silencing, and routing them. It ensures that notifications reach the right teams through channels like Email, Slack, PagerDuty, or Webhooks, making alerts actionable and reducing noise.

---

## What Are Alerting Rules?

Alerting rules are predefined conditions in Prometheus that continuously evaluate metrics.  
When a defined threshold is breached, an alert is generated and sent to **Alertmanager**, which processes and routes it to appropriate channels.

---

## Common Alert Rules for Applications

| Alert Rule                 | Condition / Threshold Example | Purpose                          | Priority  | Escalation Time     |
|----------------------------|-------------------------------|---------------------------------|----------|------------------|
| High CPU Usage             | CPU > 80% for 5 min           | CPU overload affecting performance | High     | 15 minutes       |
| Memory Utilization         | Memory > 90%                  | Prevent app crashes due to memory | Critical | Immediate        |
| Service Down               | Health check fail for 1 min   | App/API unavailable             | Critical | Immediate        |
| High Error Rate            | HTTP 5xx > 5%                 | Too many errors affecting users | Critical | 10 minutes       |
| High Latency               | Response time > 2s            | Slow response impacting UX      | Medium   | 30 minutes       |
| Disk Space Low             | Disk usage > 85%              | Avoid storage-related failures  | High     | 20 minutes       |
| DB Connection Failures     | > 50 errors/min               | Database issues impacting app   | Critical | Immediate        |
| Queue Lag                  | Queue length > threshold      | Processing delays               | Medium   | 30 minutes       |
| App Restart Detected       | Restart count > 3/hr          | App instability                 | Low      | Review daily     |

---

## Severity Levels

Each alert should have a **severity label** defining its importance and response priority.

| Severity Level | Definition                                              | Example Scenarios                             | Action / Response Time               |
| -------------- | ------------------------------------------------------- | --------------------------------------------- | ------------------------------------ |
| **Critical**   | Major outage or service down affecting users            | App or API not responding, database failure   | Immediate escalation to L2/L3        |
| **High**       | Significant performance degradation or resource overuse | CPU > 90%, Memory > 85%, Error rate > 10%     | Response within 10–15 minutes        |
| **Medium**     | Non-critical but needs attention                        | High latency, disk usage > 80%, queue backlog | Response within 30–45 minutes        |
| **Low**        | Informational or minor issues                           | Service restart, config drift, warning events | Review in daily check or next sprint |

*Severity helps prioritize response and reduces alert fatigue.*

---

## Notification Channels

Alertmanager supports multiple notification integrations for quick incident response.

| Channel Type                | Purpose                           | Example / Tool         | Usage Scenario                                                   |
| --------------------------- | --------------------------------- | ---------------------- | ---------------------------------------------------------------- |
| **Email**                   | Default notification channel      | Gmail, Outlook         | For general system alerts                                        |
| **Slack / Microsoft Teams** | Instant team collaboration        | Slack Incoming Webhook | For on-call & ops team notifications                             |
| **PagerDuty / OpsGenie**    | Incident escalation management    | PagerDuty Integration  | For production-level critical alerts                             |
| **SMS / Phone Call**        | Urgent, high-impact alerts        | Twilio / PagerDuty     | For critical outage alerts                                       |
| **Webhook / Custom API**    | Integration with automation tools | REST endpoints         | For auto-remediation or ticket creation (e.g., ServiceNow, Jira) |

---

## Escalation Process

An escalation process ensures that unacknowledged alerts are automatically passed to higher levels.

| Escalation Level         | Responsible Team            | Trigger Condition                | Escalation Time |
| ------------------------ | --------------------------- | -------------------------------- | --------------- |
| **Level 1 (L1)**         | On-call Engineer            | Alert triggered                  | Immediate       |
| **Level 2 (L2)**         | Senior Engineer / App Owner | Alert unresolved > 15 mins       | 15 minutes      |
| **Level 3 (L3)**         | DevOps / SRE Lead           | Alert unresolved > 30 mins       | 30 minutes      |
| **Level 4 (Management)** | IT Manager / CTO            | Major outage continues > 60 mins | 1 hour          |

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

| Best Practice                          | Description / Action                                      |
|----------------------------------------|-----------------------------------------------------------|
| **Use severity labels consistently**    | Ensure all alerts have proper severity to prioritize response. |
| **Define realistic thresholds**        | Set thresholds based on historical metrics to avoid false alerts. |
| **Configure grouping & inhibition**    | Group similar alerts and suppress less important ones when critical alerts are active. |
| **Integrate with Slack/PagerDuty**     | Ensure immediate visibility and quick response for critical alerts. |
| **Regularly review false alerts**      | Identify recurring false positives and refine alert rules. |
| **Perform RCA after incidents**        | Conduct Root Cause Analysis to improve rules and prevent future issues. |

---

## Conclusion

**Prometheus** and **Alertmanager** together form a powerful alerting and monitoring solution for modern applications.  
Prometheus efficiently collects and evaluates metrics, while Alertmanager manages alerts — routing, silencing, and escalating them to ensure timely notifications and quick responses.  
Using these tools helps teams maintain **high availability**, **minimize downtime**, and strengthen **observability** across distributed systems.


---
## FAQs

**Q: What is the difference between an alert and a metric?**  
**A:** A metric is raw data about system performance (like CPU usage or request rate), whereas an alert is a notification triggered when that metric crosses a predefined threshold.

**Q: How do I avoid alert fatigue in my team?**  
**A:** Focus on monitoring only key metrics, set realistic thresholds, and ensure alerts are actionable. Suppress non-critical alerts during maintenance or low-impact events.

**Q: Can alerts be integrated with multiple notification channels?**  
**A:** Yes. Alerts can be sent to email, Slack, Teams, PagerDuty, SMS, or custom webhooks simultaneously, ensuring the right people are notified promptly.

---

## Contact Information

| Name | Email |
|------|------|
| **Kawalpreet Kour** | kawalpreet.kour.snaatak@mygurukulam.co |

---

## References

| Description                 | Link |
|-----------------------------|------|
| Alerting Rules              | [Prometheus with Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) |
| Alerting Best Practices     | [Monitoring and Alerting Guide](https://www.datadoghq.com/monitoring-alerting-guide/) |
 

