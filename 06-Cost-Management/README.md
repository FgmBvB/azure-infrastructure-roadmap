# Cost Management

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Cost Management, Azure Advisor, Reservations, Savings Plans, and Azure Hybrid Benefit, providing the knowledge required to monitor, optimize, govern, and reduce Azure operational costs.

---

# Overview

Cost optimization is one of the core responsibilities of an Azure Administrator.

Azure provides several services that help organizations understand cloud spending, identify optimization opportunities, and reduce long-term operational costs without compromising performance, reliability, or security.

This module explores Microsoft's native financial governance tools and pricing models used to manage Azure environments efficiently.

---

# Learning Objectives

After completing this module you should be able to:

- Understand Azure Cost Management.
- Analyze Azure spending.
- Configure Budgets and Cost Alerts.
- Understand Forecasting.
- Interpret Actual Cost and Amortized Cost.
- Understand Billing Scopes and Azure RBAC.
- Use Azure Advisor recommendations.
- Understand Advisor Score.
- Configure Advisor Alerts.
- Query recommendations with Azure Resource Graph.
- Understand Azure Reservations.
- Understand Azure Savings Plans.
- Configure Reservation Scopes.
- Understand Instance Size Flexibility (ISF).
- Optimize Reservation Utilization.
- Understand Azure Hybrid Benefit.
- Apply Microsoft's cost optimization best practices.

---

# Module Structure

| Section | Description |
|---------|-------------|
| **01 - Cost Management** | Azure Cost Management fundamentals, Cost Analysis, Budgets, Forecasting, Billing Scopes, Actual vs. Amortized Cost, Azure RBAC, budgeting, automation, and financial governance. |
| **02 - Azure Advisor** | Azure Advisor architecture, recommendation categories, Advisor Score, Azure Monitor integration, Advisor Alerts, Azure Resource Graph, RBAC, optimization workflows, and governance best practices. |
| **03 - Reservations and Savings** | Azure Reservations, Azure Savings Plans, Azure Hybrid Benefit, Reservation Scopes, Instance Size Flexibility (ISF), reservation utilization, pricing commitments, and long-term cost optimization strategies. |

---

# Module Architecture

```text
Azure Resources

↓

Resource Consumption

↓

Azure Billing Platform

↓

Financial Governance

├── Azure Cost Management
├── Azure Advisor
├── Reservations
├── Savings Plans
└── Azure Hybrid Benefit

↓

Optimization

↓

Continuous Cost Control
```

---

# Core Technologies

This module covers the primary Azure cost optimization services.

## Azure Cost Management

Provides visibility into Azure spending.

Main capabilities:

- Cost Analysis
- Budgets
- Forecasting
- Cost Allocation
- Exports
- Cost Alerts

---

## Azure Advisor

Continuously analyzes Azure resources and recommends improvements.

Recommendation categories:

- Cost
- Reliability
- Security
- Performance
- Operational Excellence

---

## Azure Reservations

Provide discounted pricing through one-year or three-year commitments for predictable workloads.

Key concepts:

- Reservation Scopes
- Automatic Matching
- Reservation Utilization
- Instance Size Flexibility

---

## Azure Savings Plans

Provide flexible pricing discounts for compute workloads based on a committed hourly spend rather than specific resource types.

Ideal for:

- Dynamic environments
- Autoscaling applications
- Frequently resized Virtual Machines

---

## Azure Hybrid Benefit

Allows organizations to reuse eligible Windows Server and SQL Server licenses in Azure.

Benefits include:

- Lower licensing costs
- Reduced Virtual Machine costs
- Additional savings when combined with Reservations or Savings Plans (where supported)

---

# Cost Optimization Workflow

```text
Deploy Resources

↓

Monitor Costs

↓

Analyze Spending

↓

Advisor Recommendations

↓

Reservations
Savings Plans
Hybrid Benefit

↓

Optimization

↓

Continuous Review
```

Cost optimization is an ongoing operational process rather than a one-time activity.

---

# Design Principles

Microsoft recommends following these principles:

- Monitor Azure spending continuously.
- Configure budgets before large deployments.
- Apply consistent resource tagging.
- Review Azure Advisor regularly.
- Use Reservations for predictable workloads.
- Use Savings Plans for dynamic compute.
- Enable Azure Hybrid Benefit when eligible.
- Track Reservation Utilization.
- Balance cost optimization with reliability, security, and performance.
- Review financial governance as workloads evolve.

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Azure Cost Management
- Cost Analysis
- Budgets
- Forecasting
- Cost Alerts
- Billing Scopes
- Azure RBAC
- Azure Advisor
- Advisor Score
- Advisor Alerts
- Azure Resource Graph
- Azure Reservations
- Azure Savings Plans
- Azure Hybrid Benefit
- Reservation Scopes
- Reservation Matching
- Instance Size Flexibility (ISF)
- Reservation Utilization
- Discount Application Order
- Cost Optimization Best Practices

---

# Key Takeaways

- Azure Cost Management provides the financial visibility required to monitor, forecast, and govern Azure spending.
- Azure Advisor continuously analyzes deployed resources and recommends improvements across cost, security, reliability, performance, and operational excellence.
- Azure Reservations, Savings Plans, and Azure Hybrid Benefit work together to reduce long-term Azure infrastructure costs through automated billing discounts.
- Effective cost optimization depends on understanding workload characteristics, selecting the appropriate pricing model, and continuously monitoring utilization and spending.
- Successful Azure administrators treat cost management as a continuous governance process that balances financial efficiency with business, security, and operational requirements.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cost Management | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Reservations | https://learn.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations |
| Azure Savings Plans | https://learn.microsoft.com/azure/cost-management-billing/savings-plan/savings-plan-compute-overview |
| Azure Hybrid Benefit | https://learn.microsoft.com/azure/azure-hybrid-benefit/ |
| Azure Well-Architected Framework – Cost Optimization | https://learn.microsoft.com/azure/well-architected/cost-optimization/ |
| Microsoft Learn – Control and optimize Azure costs | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
