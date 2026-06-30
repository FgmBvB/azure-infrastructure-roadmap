# Azure Monitoring Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Monitor and the core monitoring services used to observe, analyze, troubleshoot, and optimize Azure resources in production environments.

---

# Overview

Monitoring is a fundamental operational responsibility in Azure.

Without proper monitoring, administrators cannot effectively detect failures, diagnose performance issues, respond to security events, or maintain service availability.

Azure Monitor is Microsoft's centralized monitoring platform that collects telemetry from Azure resources, operating systems, applications, and networking components.

It provides a unified solution for:

- Collecting telemetry
- Visualizing performance
- Generating alerts
- Investigating incidents
- Supporting troubleshooting
- Improving operational health

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
        ├──────── Events
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
Automation Analysis Insights
```

Azure Monitor serves as the central monitoring platform for Azure services.

---

# Core Components

Azure Monitor is composed of several integrated services.

## Metrics

Metrics are:

- Numerical values
- Lightweight
- Near real-time
- Optimized for performance monitoring

Examples:

- CPU Percentage
- Available Memory
- Network Throughput
- Disk IOPS
- Requests per Second

Metrics are stored in a time-series database.

---

## Logs

Logs contain detailed operational information.

Unlike metrics, logs provide rich diagnostic data that can be queried using Kusto Query Language (KQL).

Typical log sources include:

- Virtual Machines
- Azure Firewall
- NSGs
- Storage Accounts
- Application Gateway
- Activity Log
- Microsoft Entra ID

Logs are stored inside a **Log Analytics Workspace**.

---

## Log Analytics Workspace

A Log Analytics Workspace is the central repository for Azure Monitor logs.

It enables:

- Centralized log storage
- Cross-resource queries
- KQL searches
- Dashboards
- Alert rules
- Long-term retention

Multiple Azure resources can send telemetry to the same workspace.

---

## Log Analytics Retention and Data Lifecycle

Log Analytics supports configurable data retention policies to balance operational requirements and storage costs.

Two storage stages are available:

### Interactive Retention

Interactive data can be queried immediately using Kusto Query Language (KQL).

Retention can be configured according to organizational requirements and Microsoft-supported limits.

---

### Archived Logs

Older data can be moved to the Archive tier for long-term retention.

Archived data:

- Costs less to store.
- Is not immediately queryable.
- Can be restored temporarily or searched using Search Jobs.

Archive is commonly used to satisfy long-term compliance requirements.

---

### Data Purge

Log Analytics is designed as an append-only platform.

Individual records cannot be deleted through normal queries.

To satisfy legal or regulatory requirements (such as GDPR), Azure provides a dedicated **Workspace Purge** operation through the Azure REST API.

> [!IMPORTANT]
> Retention policies reduce storage costs, while Archive and Purge address compliance and regulatory requirements.

---

## Activity Log

The Activity Log records management operations performed on Azure resources.

Examples:

- Resource creation
- Resource deletion
- RBAC changes
- Azure Policy assignments
- Virtual Machine start/stop
- Network configuration changes

The Activity Log operates at the Azure subscription level.

---

## Activity Log Retention

Azure Activity Log records subscription-level management operations.

By default:

- Activity Log is retained by Azure for a limited period.
- Long-term auditing requires exporting the data.

Organizations requiring extended audit history should configure **Diagnostic Settings** to continuously export Activity Log data to:

- Log Analytics Workspace
- Azure Storage Account
- Event Hubs

This enables long-term retention, centralized analysis, and compliance reporting.

> [!TIP]
> Diagnostic Settings should be configured early in the deployment lifecycle to avoid losing historical management events.

---

## Diagnostic Settings

Diagnostic Settings define which resource logs and metrics are exported.

Supported destinations include:

- Log Analytics Workspace
- Azure Storage Account
- Event Hubs

Without Diagnostic Settings enabled, many resource-specific logs are not collected.

---

## Alerts

Azure Monitor Alerts automatically notify administrators when predefined conditions occur.

Alert sources include:

- Metrics
- Logs
- Activity Log
- Service Health
- Resource Health

Alerts trigger **Action Groups**.

---

## Metric Alerts vs Log Alerts

Azure Monitor supports two primary alert types.

| Feature | Metric Alerts | Log Alerts |
|----------|---------------|------------|
| Data Source | Azure Metrics | Log Analytics queries |
| Response Time | Near real-time | Depends on log ingestion |
| Query Language | Not required | KQL |
| Typical Use Cases | CPU, Memory, Network | Security, auditing, complex conditions |
| Cost | Lower | Depends on log ingestion and query execution |

### Metric Alerts

Metric Alerts evaluate platform metrics at frequent intervals.

Typical scenarios include:

- High CPU utilization
- Memory pressure
- Network throughput
- Disk performance

They provide the fastest response for infrastructure monitoring.

---

### Log Alerts

Log Alerts evaluate Kusto Query Language (KQL) queries against Log Analytics data.

Typical scenarios include:

- Security events
- Azure Firewall activity
- Failed sign-in attempts
- Administrative operations
- Compliance monitoring

Because Log Alerts depend on data ingestion into Log Analytics, they typically have higher latency than Metric Alerts.

> [!IMPORTANT]
> Use Metric Alerts for infrastructure health and Log Alerts for operational, security, and compliance scenarios.

---

## Action Groups

Action Groups define what happens when an alert is triggered.

Common actions include:

- Email
- SMS
- Push notification
- Voice call
- Azure Function
- Logic App
- Automation Runbook
- Webhook

One Action Group can be reused across multiple alerts.

---

## Azure Monitor Agent (AMA)

Azure Monitor Agent (AMA) is Microsoft's modern monitoring agent.

AMA replaces the legacy:

- Log Analytics Agent (MMA)
- Diagnostics Extension

Benefits include:

- Simplified management
- Better performance
- Data Collection Rules support
- Improved security

Microsoft recommends AMA for all new deployments.

---

## Data Collection Rules (DCR)

Data Collection Rules determine:

- What data is collected
- Where data is sent
- Which machines collect telemetry

Benefits:

- Centralized configuration
- Flexible filtering
- Reduced ingestion costs
- Consistent monitoring policies

DCRs work together with Azure Monitor Agent.

---

# Azure Monitor Data Flow

```text
Azure Resources

↓

Azure Monitor Agent

↓

Data Collection Rules

↓

Azure Monitor

↓

Metrics
Logs
Activity Log

↓

Alerts
Dashboards
Workbooks
Analysis
```

---

# Azure Monitor Insights

Azure Monitor includes built-in monitoring solutions called **Insights**.

Examples include:

- VM Insights
- Container Insights
- Network Insights
- Application Insights

Insights provide:

- Performance dashboards
- Dependency maps
- Health information
- Performance recommendations

---

# Service Health

Azure Service Health reports issues affecting Microsoft Azure services.

Categories include:

- Service Issues
- Planned Maintenance
- Health Advisories
- Security Advisories

Service Health helps determine whether an incident originates from Azure itself.

---

# Resource Health

Resource Health reports the health of individual Azure resources.

Typical states include:

- Available
- Unavailable
- Unknown
- Degraded

Resource Health is useful when diagnosing infrastructure problems affecting specific resources.

---

# Azure Advisor

Azure Advisor analyzes Azure deployments and recommends improvements.

Categories include:

- Reliability
- Security
- Performance
- Operational Excellence
- Cost Optimization

Although Advisor is not a monitoring platform itself, it complements Azure Monitor by identifying optimization opportunities.

---

# Monitoring Workflow

A typical operational workflow follows these steps:

```text
Resource

↓

Telemetry Collection

↓

Azure Monitor

↓

Metrics & Logs

↓

Alert

↓

Action Group

↓

Administrator

↓

Investigation

↓

Resolution
```

---

# Monitoring Hierarchy

```text
Azure Monitor

├── Metrics

├── Logs
│     └── Log Analytics Workspace

├── Alerts
│     └── Action Groups

├── Activity Log

├── Diagnostic Settings

├── Azure Monitor Agent

├── Data Collection Rules

├── Service Health

├── Resource Health

└── Insights
```

---

# Enterprise Scenario

A production environment contains:

- Virtual Machines
- Azure Firewall
- Application Gateway
- Azure SQL Database
- Storage Accounts

Azure Monitor collects telemetry using Azure Monitor Agent.

Logs are stored in a shared Log Analytics Workspace.

Metric Alerts detect:

- High CPU utilization
- Low disk space
- Gateway failures

Action Groups notify administrators by email and trigger Automation Runbooks.

Azure Advisor periodically recommends optimization opportunities.

---

# Common Pitfalls

- Not configuring Diagnostic Settings.
- Using multiple unnecessary Log Analytics Workspaces.
- Forgetting to configure Action Groups.
- Ignoring Service Health notifications.
- Collecting excessive log data.
- Not using Data Collection Rules.
- Continuing to deploy legacy monitoring agents.
- Creating alerts without meaningful thresholds.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Monitor
> - Metrics vs Logs
> - Log Analytics Workspace
> - Azure Monitor Agent (AMA)
> - Data Collection Rules (DCR)
> - Activity Log
> - Diagnostic Settings
> - Alerts
> - Action Groups
> - Service Health
> - Resource Health
> - Azure Advisor
> - Monitoring architecture

---

# Key Takeaways

- Azure Monitor is Microsoft's centralized platform for collecting, analyzing, and acting on telemetry from Azure resources.
- Metrics provide lightweight, near real-time performance data, while logs offer detailed operational information stored in Log Analytics Workspaces.
- Azure Monitor Agent and Data Collection Rules represent the modern approach to telemetry collection and configuration.
- Alerts, Action Groups, Service Health, and Resource Health enable rapid detection and response to operational issues.
- A well-designed monitoring strategy improves reliability, accelerates troubleshooting, and supports proactive management of Azure environments.

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
