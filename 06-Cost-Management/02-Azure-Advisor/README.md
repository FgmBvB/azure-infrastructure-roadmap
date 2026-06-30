# Azure Advisor

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Advisor, Microsoft's built-in recommendation service that continuously analyzes Azure resources and provides personalized guidance to improve cost efficiency, reliability, security, performance, and operational excellence.

---

# Overview

Azure Advisor is a free Azure service that evaluates deployed resources against Microsoft's best practices.

It continuously analyzes the Azure environment and generates recommendations that help administrators optimize infrastructure without manually auditing every resource.

Azure Advisor complements services such as:

- Azure Monitor
- Azure Cost Management
- Microsoft Defender for Cloud
- Azure Policy
- Azure Well-Architected Framework

Rather than monitoring operational health, Azure Advisor focuses on improving the overall quality, efficiency, and governance of Azure deployments.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Advisor architecture.
- Understand recommendation categories.
- Interpret Advisor Score.
- Prioritize recommendations.
- Understand Cost, Reliability, Security, Performance, and Operational Excellence recommendations.
- Configure Advisor Alerts.
- Understand Snooze and Dismiss actions.
- Filter recommendations by scope.
- Understand Azure RBAC permissions for Advisor.
- Query recommendations using Azure Resource Graph.
- Apply Microsoft's operational best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure Advisor architecture, recommendation categories, Advisor Score, recommendation lifecycle, Azure Monitor integration, Microsoft Defender for Cloud integration, scope filtering, Azure Resource Graph, RBAC, and core AZ-104 concepts. |
| **02 - Best Practices** | Operational reviews, recommendation prioritization, Advisor Alerts, governance, Azure Monitor integration, Azure Policy, Resource Graph reporting, automation, cost optimization, and Microsoft's production recommendations. |

---

# Azure Advisor Architecture

```text
Azure Resources

↓

Azure Platform Telemetry

↓

Azure Advisor Analysis Engine

↓

Recommendations

├── Cost
├── Reliability
├── Security
├── Performance
└── Operational Excellence

↓

Administrator Review

↓

Continuous Optimization
```

Azure Advisor continuously evaluates deployed resources and updates recommendations as the environment evolves.

---

# Core Capabilities

This section covers the primary capabilities of Azure Advisor.

## Optimization

- Cost optimization
- Performance improvements
- Reliability recommendations
- Security guidance
- Operational Excellence recommendations

---

## Governance

- Advisor Score
- Recommendation prioritization
- Scope filtering
- Azure RBAC integration
- Recommendation lifecycle

---

## Automation

- Azure Monitor Alerts
- Action Groups
- Advisor Alerts
- Automation workflows
- ITSM integration

---

## Enterprise Visibility

- Azure Resource Graph
- Multi-subscription analysis
- Management Group reporting
- Organizational governance

---

# Recommendation Lifecycle

```text
Azure Resources

↓

Platform Analysis

↓

Recommendation Generated

↓

Administrator Review

↓

Implement
Snooze
Dismiss

↓

Environment Optimized

↓

Continuous Reassessment
```

Recommendations evolve automatically as Azure resources change.

---

# Design Principles

Microsoft recommends following these principles:

- Review Advisor regularly.
- Prioritize recommendations by business impact.
- Validate recommendations before implementation.
- Integrate Advisor with Azure Monitor.
- Review Advisor Score over time.
- Filter recommendations by scope.
- Automate operational notifications.
- Track optimization trends.
- Balance cost, security, reliability, and performance.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Advisor
- Advisor recommendation categories
- Advisor Score
- Recommendation prioritization
- Cost optimization
- Azure Monitor integration
- Microsoft Defender for Cloud integration
- Advisor Alerts
- Azure Resource Graph
- Azure RBAC
- Snooze vs Dismiss
- Scope filtering
- Operational best practices

---

# Key Takeaways

- Azure Advisor continuously analyzes Azure resources and provides personalized recommendations based on Microsoft's best practices.
- Recommendations span Cost, Reliability, Security, Performance, and Operational Excellence, helping administrators optimize every aspect of their Azure environment.
- Advisor Score, Azure Resource Graph, and scope filtering provide valuable governance capabilities for large-scale environments.
- Integration with Azure Monitor, Action Groups, and automation services enables proactive operational workflows.
- Regular review of Advisor recommendations supports continuous improvement, better governance, and more efficient Azure administration.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Advisor documentation | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Advisor recommendations | https://learn.microsoft.com/azure/advisor/advisor-reference |
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Cost Management | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/defender-for-cloud-introduction |
| Azure Resource Graph | https://learn.microsoft.com/azure/governance/resource-graph/overview |
| Azure Monitor | https://learn.microsoft.com/azure/azure-monitor/overview |
| Microsoft Learn – Optimize Azure resources with Azure Advisor | https://learn.microsoft.com/training/modules/optimize-costs-azure-advisor/ |
