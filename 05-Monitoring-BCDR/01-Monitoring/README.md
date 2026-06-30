# Azure Monitoring

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Monitor and the services used to collect, analyze, visualize, and act upon operational data across Azure environments.

---

# Overview

Monitoring is essential for operating Azure environments efficiently.

Azure Monitor provides a centralized platform that collects telemetry from Azure resources, operating systems, applications, and networking services, enabling administrators to proactively detect issues, investigate incidents, and maintain service health.

Rather than focusing on a single monitoring tool, Azure combines multiple services that work together to provide complete operational visibility.

This section introduces those services and Microsoft's recommended operational practices.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Monitor architecture.
- Differentiate Metrics and Logs.
- Configure Log Analytics Workspaces.
- Understand Azure Monitor Agent (AMA).
- Configure Data Collection Rules (DCR).
- Configure Diagnostic Settings.
- Configure Azure Monitor Alerts.
- Configure Action Groups.
- Understand Activity Log.
- Monitor Azure Service Health and Resource Health.
- Understand Azure Advisor recommendations.
- Apply Microsoft's monitoring best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure Monitor architecture, Metrics, Logs, Log Analytics Workspace, Azure Monitor Agent (AMA), Data Collection Rules (DCR), Activity Log, Diagnostic Settings, Alerts, Action Groups, Service Health, Resource Health, Azure Advisor, and monitoring fundamentals. |
| **02 - Best Practices** | Centralized monitoring, alert strategy, log retention, cost optimization, security, monitoring architecture, troubleshooting, governance, and Microsoft's production recommendations. |

---

# Azure Monitor Architecture

```text
Azure Resources
        │
        ▼
Telemetry Collection
        │
        ├──────── Metrics
        ├──────── Logs
        ├──────── Activity Log
        │
        ▼
Azure Monitor
        │
 ┌──────┼──────────────┐
 │      │              │
 ▼      ▼              ▼
Alerts Logs      Dashboards
 │      │              │
 ▼      ▼              ▼
Action Groups   Workbooks
        │
        ▼
 Investigation & Response
```

Azure Monitor centralizes telemetry collection and operational analysis across Azure services.

---

# Core Services Covered

This section includes:

## Monitoring Platform

- Azure Monitor
- Azure Monitor Agent (AMA)
- Data Collection Rules (DCR)
- Diagnostic Settings

---

## Data Collection

- Metrics
- Logs
- Activity Log
- Resource Logs
- Log Analytics Workspace

---

## Alerting

- Metric Alerts
- Log Alerts
- Activity Log Alerts
- Action Groups
- Alert Processing Rules

---

## Health Monitoring

- Azure Service Health
- Azure Resource Health
- Azure Advisor

---

## Operations

- Dashboards
- Azure Workbooks
- Kusto Query Language (KQL) fundamentals
- Log retention
- Cost optimization
- Monitoring governance

---

# Monitoring Workflow

```text
Azure Resource

↓

Telemetry

↓

Azure Monitor

↓

Metrics & Logs

↓

Alert Rules

↓

Action Groups

↓

Operations Team

↓

Investigation

↓

Resolution
```

A well-designed monitoring workflow enables proactive operations and faster incident response.

---

# Design Principles

Microsoft recommends following these principles:

- Centralize monitoring whenever possible.
- Collect only required telemetry.
- Prefer Azure Monitor Agent over legacy agents.
- Use Data Collection Rules to standardize configurations.
- Configure Diagnostic Settings early.
- Design meaningful alerts that reduce operational noise.
- Protect monitoring data with Azure RBAC.
- Balance observability with storage costs.
- Continuously review monitoring effectiveness.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Monitor
- Log Analytics Workspace
- Azure Monitor Agent
- Data Collection Rules
- Metrics
- Logs
- Activity Log
- Diagnostic Settings
- Azure Monitor Alerts
- Action Groups
- Azure Service Health
- Azure Resource Health
- Azure Advisor

---

# Key Takeaways

- Azure Monitor is Microsoft's centralized monitoring platform for collecting, analyzing, and responding to telemetry across Azure resources.
- Metrics, Logs, Activity Log, and Diagnostic Settings work together to provide complete operational visibility.
- Azure Monitor Agent and Data Collection Rules form the foundation of Microsoft's modern monitoring architecture.
- Alerts, Action Groups, and Health services enable proactive monitoring and faster incident response.
- Applying Microsoft's monitoring best practices improves reliability, operational efficiency, and cost management in production Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/overview |
| Azure Monitor Agent | https://learn.microsoft.com/azure/azure-monitor/agents/azure-monitor-agent-overview |
| Data Collection Rules | https://learn.microsoft.com/azure/azure-monitor/essentials/data-collection-rule-overview |
| Log Analytics Workspace | https://learn.microsoft.com/azure/azure-monitor/logs/log-analytics-workspace-overview |
| Azure Monitor Alerts | https://learn.microsoft.com/azure/azure-monitor/alerts/alerts-overview |
| Azure Service Health | https://learn.microsoft.com/azure/service-health/overview |
| Azure Resource Health | https://learn.microsoft.com/azure/service-health/resource-health-overview |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Well-Architected Framework – Operational Excellence | https://learn.microsoft.com/azure/well-architected/operational-excellence/ |
| Microsoft Learn – Monitor Azure resources | https://learn.microsoft.com/training/modules/monitor-azure-resources-with-azure-monitor/ |
