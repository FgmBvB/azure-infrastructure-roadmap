# Azure Monitoring Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for designing, operating, securing, and optimizing Azure Monitor in production environments.

---

# Overview

Monitoring is not simply about collecting data—it is about collecting the **right data**, generating actionable alerts, and reducing the time required to detect and resolve incidents.

A successful monitoring strategy should provide:

- Visibility
- Reliability
- Security
- Operational efficiency
- Cost control

Microsoft recommends designing monitoring from the beginning of every Azure deployment rather than adding it after production.

---

# Design a Centralized Monitoring Strategy

Avoid isolated monitoring configurations.

Recommendations:

- Use centralized Log Analytics Workspaces.
- Standardize monitoring across subscriptions.
- Collect telemetry consistently.
- Reuse Alert Rules whenever possible.
- Share Action Groups across workloads.

Centralized monitoring simplifies administration and troubleshooting.

---

# Use Azure Monitor Agent

Microsoft recommends using **Azure Monitor Agent (AMA)** for all new deployments.

Benefits include:

- Better performance.
- Simplified configuration.
- Support for Data Collection Rules.
- Centralized management.
- Improved security.

Avoid deploying legacy Log Analytics Agent (MMA).

---

# Configure Data Collection Rules

Use **Data Collection Rules (DCRs)** instead of configuring monitoring individually on each resource.

Recommendations:

- Collect only required data.
- Filter unnecessary logs.
- Reuse DCRs across similar workloads.
- Separate production and development configurations.
- Review DCRs periodically.

Proper DCR configuration reduces ingestion costs.

---

# Configure Diagnostic Settings

Many Azure resources do not send logs automatically.

Always configure Diagnostic Settings for production resources.

Recommended destinations:

- Log Analytics Workspace
- Storage Account
- Event Hubs

Without Diagnostic Settings, important operational data may never be collected.

---

# Configure Meaningful Alerts

Alerts should detect real operational problems.

Recommendations:

- Alert only on actionable events.
- Avoid excessive alert noise.
- Review thresholds regularly.
- Test alert behavior.
- Group related alerts.

Poor alert design leads to alert fatigue.

---

# Choose the Correct Alert Type

Use the appropriate alert based on the workload.

| Scenario | Recommended Alert |
|----------|-------------------|
| CPU utilization | Metric Alert |
| Memory utilization | Metric Alert |
| Disk performance | Metric Alert |
| Security events | Log Alert |
| Azure Firewall logs | Log Alert |
| Failed sign-ins | Log Alert |
| Administrative changes | Activity Log Alert |

Metric Alerts provide faster response times.

Log Alerts support more advanced analysis through KQL.

---

# Use Action Groups Efficiently

Action Groups should be reusable.

Recommendations:

- Separate operational teams.
- Reuse existing Action Groups.
- Document notification policies.
- Automate incident response where possible.

Common actions include:

- Email
- SMS
- Webhook
- Logic Apps
- Azure Automation
- Azure Functions

---

# Optimize Log Collection

Collecting excessive telemetry increases costs.

Recommendations:

- Collect only required logs.
- Disable unnecessary diagnostic categories.
- Review ingestion volume regularly.
- Archive historical data when appropriate.
- Adjust retention policies according to business requirements.

Monitoring should provide value without generating unnecessary expenses.

---

# Manage Log Retention

Configure retention according to operational and compliance requirements.

Recommendations:

- Keep interactive data only as long as necessary.
- Use Archive for long-term retention.
- Review retention policies regularly.
- Configure different retention periods when appropriate.

Longer retention increases storage costs.

---

# Monitor Platform Health

Monitor both Microsoft services and customer resources.

Recommended services:

- Azure Service Health
- Azure Resource Health
- Azure Monitor
- Azure Advisor

These services complement one another and improve incident diagnosis.

---

# Use Dashboards and Workbooks

Visualization improves operational awareness.

Recommendations:

- Build shared dashboards.
- Use Azure Workbooks.
- Display key infrastructure metrics.
- Create operational views for support teams.
- Review dashboards regularly.

Dashboards should simplify decision making.

---

# Secure Monitoring Data

Monitoring data often contains sensitive operational information.

Recommendations:

- Restrict Log Analytics access using Azure RBAC.
- Apply least privilege.
- Protect Storage Accounts used for diagnostics.
- Encrypt exported data.
- Audit monitoring access regularly.

Monitoring systems should follow the same security standards as production workloads.

---

# Monitor Costs

Azure Monitor generates costs based on data ingestion and retention.

Recommendations:

- Review ingestion trends.
- Remove unnecessary data sources.
- Optimize Diagnostic Settings.
- Archive historical logs.
- Monitor workspace usage.

Monitoring should remain operationally valuable while controlling costs.

---

# Enterprise Scenario

A company operates:

- Virtual Machines
- Azure Firewall
- Application Gateway
- Azure SQL Database
- Storage Accounts

Microsoft recommendations include:

- One centralized Log Analytics Workspace.
- Azure Monitor Agent on all Virtual Machines.
- Shared Data Collection Rules.
- Metric Alerts for infrastructure health.
- Log Alerts for security monitoring.
- Shared Action Groups.
- Azure Service Health notifications.
- Azure Advisor reviews.
- Archived logs for long-term compliance.

---

# Best Practices Checklist

- Use Azure Monitor Agent.
- Centralize Log Analytics Workspaces.
- Configure Diagnostic Settings.
- Use Data Collection Rules.
- Configure meaningful alerts.
- Select the correct alert type.
- Reuse Action Groups.
- Optimize log collection.
- Configure appropriate retention.
- Archive historical logs.
- Monitor Azure Service Health.
- Review Azure Advisor recommendations.
- Secure monitoring resources.
- Control monitoring costs.

---

# Common Pitfalls

- Continuing to deploy legacy monitoring agents.
- Creating multiple unnecessary Log Analytics Workspaces.
- Forgetting Diagnostic Settings.
- Collecting excessive telemetry.
- Creating too many alerts.
- Ignoring alert testing.
- Using Log Alerts for simple infrastructure metrics.
- Not reviewing retention policies.
- Leaving monitoring data unprotected.

---

# Advanced Troubleshooting

Azure provides several tools that work together during incident investigation.

| Tool | Purpose |
|------|----------|
| Azure Monitor | Central monitoring platform |
| Log Analytics | Query operational logs |
| Metrics Explorer | Analyze performance metrics |
| Activity Log | Audit management operations |
| Service Health | Microsoft platform incidents |
| Resource Health | Individual resource health |
| Azure Advisor | Optimization recommendations |

Using these services together significantly reduces troubleshooting time.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Monitor
> - Azure Monitor Agent (AMA)
> - Data Collection Rules (DCR)
> - Log Analytics Workspace
> - Diagnostic Settings
> - Metrics vs Logs
> - Metric Alerts
> - Log Alerts
> - Activity Log
> - Action Groups
> - Azure Service Health
> - Azure Resource Health
> - Azure Advisor
> - Monitoring best practices

---

# Key Takeaways

- A centralized monitoring strategy provides better visibility, operational consistency, and simplified troubleshooting across Azure environments.
- Azure Monitor Agent, Data Collection Rules, and Diagnostic Settings form the foundation of Microsoft's modern monitoring architecture.
- Selecting the appropriate alert type, optimizing log collection, and configuring retention policies improve both operational effectiveness and cost efficiency.
- Monitoring platform health, protecting monitoring data, and reviewing Azure Advisor recommendations help maintain secure and reliable Azure deployments.
- Following Microsoft's monitoring best practices enables proactive operations, faster incident response, and long-term operational excellence.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/overview |
| Azure Monitor Agent | https://learn.microsoft.com/azure/azure-monitor/agents/azure-monitor-agent-overview |
| Data Collection Rules | https://learn.microsoft.com/azure/azure-monitor/essentials/data-collection-rule-overview |
| Log Analytics Workspace | https://learn.microsoft.com/azure/azure-monitor/logs/log-analytics-workspace-overview |
| Azure Monitor Alerts | https://learn.microsoft.com/azure/azure-monitor/alerts/alerts-overview |
| Azure Monitor pricing | https://learn.microsoft.com/azure/azure-monitor/cost-usage |
| Azure Service Health | https://learn.microsoft.com/azure/service-health/overview |
| Azure Resource Health | https://learn.microsoft.com/azure/service-health/resource-health-overview |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Well-Architected Framework – Operational Excellence | https://learn.microsoft.com/azure/well-architected/operational-excellence/ |
