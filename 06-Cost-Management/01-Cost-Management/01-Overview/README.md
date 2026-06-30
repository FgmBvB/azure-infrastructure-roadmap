# Azure Cost Management Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Cost Management, Microsoft's native solution for monitoring, analyzing, optimizing, and governing Azure spending across subscriptions and resources.

---

# Overview

Cloud computing changes the way organizations consume infrastructure.

Unlike traditional datacenters with fixed capital expenses (CapEx), Azure follows a **pay-as-you-go** pricing model where resources are billed according to actual consumption.

Azure Cost Management provides administrators with the tools needed to:

- Monitor Azure spending
- Analyze resource costs
- Forecast future expenses
- Create budgets
- Configure cost alerts
- Allocate costs across teams
- Optimize cloud spending

Cost Management is a key operational service that helps organizations maintain financial control while maximizing resource efficiency.

---

# Azure Cost Management Architecture

```text
Azure Resources

↓

Resource Consumption

↓

Azure Billing Platform

↓

Azure Cost Management

↓

Cost Analysis
Budgets
Alerts
Exports
Recommendations

↓

Optimization & Governance
```

Azure Cost Management continuously collects billing information and transforms it into actionable financial insights.

---

# Core Components

Azure Cost Management consists of several integrated capabilities.

---

## Cost Analysis

Cost Analysis provides interactive reports that allow administrators to understand Azure spending.

Typical analysis includes:

- Cost by Subscription
- Cost by Resource Group
- Cost by Resource
- Cost by Service
- Cost by Region
- Cost by Tag

Administrators can filter, group, and visualize spending trends over time.

---

## Budgets

Budgets define expected spending limits.

A budget itself **does not stop Azure resources**.

Instead, it monitors spending against predefined thresholds.

Budgets can be configured at:

- Management Group
- Subscription
- Resource Group

Typical thresholds include:

- 50%
- 80%
- 90%
- 100%

When thresholds are reached, Azure triggers notifications through Azure Monitor.

---

## Cost Alerts

Cost alerts notify administrators when spending reaches predefined conditions.

Alerts help organizations:

- Prevent unexpected invoices.
- Detect abnormal spending.
- Track departmental budgets.
- Improve financial governance.

Alerts are commonly associated with Azure Budgets.

---

## Cost Allocation

Organizations often share Azure subscriptions across multiple departments.

Cost allocation helps distribute expenses using:

- Resource Groups
- Tags
- Subscriptions
- Management Groups

Proper tagging enables accurate chargeback and showback reporting.

---

## Cost Exports

Cost data can be exported automatically.

Supported destinations include:

- Azure Storage
- Power BI
- External reporting tools

Exports allow organizations to build custom financial dashboards.

---

## Forecasting

Azure Cost Management predicts future spending based on historical consumption.

Forecasting helps administrators:

- Estimate monthly costs.
- Detect spending trends.
- Plan budgets.
- Evaluate growth scenarios.

Forecasts improve financial planning but remain estimates based on historical usage.

---

## Cost Optimization Recommendations

Azure Cost Management works together with **Azure Advisor**.

Recommendations may include:

- Resize Virtual Machines.
- Remove unused resources.
- Purchase Reservations.
- Optimize storage usage.
- Reduce idle resources.

Optimization recommendations help reduce unnecessary spending.

---

# Pricing Model

Azure resources are billed according to different pricing models.

Common examples include:

| Resource | Billing Model |
|----------|---------------|
| Virtual Machines | Per second while running |
| Managed Disks | Provisioned capacity |
| Storage Accounts | Capacity + transactions |
| Azure SQL Database | Selected pricing tier |
| Azure Backup | Protected instances + storage |
| Bandwidth | Outbound data transfer |
| Public IP Addresses | SKU and allocation model |

Understanding pricing models helps prevent unexpected costs.

---

# Cost Management Workflow

```text
Deploy Resources

↓

Consume Azure Services

↓

Billing Data Collection

↓

Azure Cost Management

↓

Analyze Costs

↓

Create Budgets

↓

Monitor Spending

↓

Optimize Resources
```

---

# Scope Hierarchy

Cost information can be viewed at multiple Azure scopes.

```text
Management Group

↓

Subscription

↓

Resource Group

↓

Individual Resource
```

Higher scopes provide consolidated financial visibility.

---

# Azure Cost Management + Azure Monitor

Although closely related, these services have different responsibilities.

| Azure Cost Management | Azure Monitor |
|-----------------------|---------------|
| Financial analysis | Operational monitoring |
| Budgets | Alerts |
| Forecasting | Metrics |
| Cost reports | Logs |
| Spending optimization | Infrastructure health |

Together they provide operational and financial visibility.

---

# Enterprise Scenario

A company operates:

- Three Azure subscriptions
- Multiple departments
- Production and Development environments

Administrators:

- Tag all resources.
- Create departmental budgets.
- Monitor monthly spending.
- Export cost reports.
- Review Azure Advisor recommendations.
- Forecast future costs.

This enables centralized financial governance while maintaining operational flexibility.

---

# Common Pitfalls

- Creating resources without tags.
- Ignoring Azure Budgets.
- Assuming budgets stop resource deployment.
- Forgetting to review Cost Analysis regularly.
- Leaving unused resources running.
- Ignoring Azure Advisor recommendations.
- Failing to export cost reports.
- Using incorrect scope when analyzing costs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Cost Management
> - Cost Analysis
> - Budgets
> - Cost Alerts
> - Forecasting
> - Cost Allocation
> - Cost Exports
> - Pricing models
> - Scope hierarchy
> - Cost optimization fundamentals

---

# Key Takeaways

- Azure Cost Management provides centralized visibility into Azure spending and helps organizations monitor, analyze, forecast, and optimize cloud costs.
- Cost Analysis, Budgets, Alerts, Forecasting, and Cost Allocation work together to improve financial governance.
- Budgets monitor spending and trigger notifications but do not automatically stop resource consumption.
- Proper tagging, regular cost reviews, and optimization recommendations help reduce unnecessary expenses.
- Effective cost management combines financial oversight with operational best practices to maximize the value of Azure resources.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cost Management documentation | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Cost Analysis | https://learn.microsoft.com/azure/cost-management-billing/costs/cost-analysis-common-uses |
| Create and manage budgets | https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets |
| Export cost data | https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data |
| Understand your Azure bill | https://learn.microsoft.com/azure/cost-management-billing/understand/review-individual-bill |
| Azure pricing | https://azure.microsoft.com/pricing/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Well-Architected Framework – Cost Optimization | https://learn.microsoft.com/azure/well-architected/cost-optimization/ |
| Microsoft Learn – Introduction to Cost Management | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
