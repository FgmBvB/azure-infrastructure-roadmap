# Azure Advisor Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Advisor, Microsoft's personalized cloud consultant that analyzes Azure resources and provides recommendations to improve reliability, security, performance, operational excellence, and cost optimization.

---

# Overview

Azure Advisor is a free Azure service that continuously analyzes deployed resources and compares them against Microsoft's recommended best practices.

Based on telemetry collected from Azure Resource Manager and platform services, Advisor generates personalized recommendations that help administrators:

- Reduce Azure costs
- Improve security
- Increase reliability
- Optimize performance
- Improve operational excellence

Unlike Azure Monitor, which focuses on operational health and monitoring, Azure Advisor focuses on **improving the configuration and efficiency** of Azure resources.

---

# Azure Advisor Architecture

```text
Azure Resources

↓

Azure Platform Telemetry

↓

Azure Advisor Analysis Engine

↓

Personalized Recommendations

↓

Administrator Review

↓

Optimization

↓

Improved Azure Environment
```

Advisor continuously evaluates Azure resources and updates recommendations automatically as the environment changes.

---

# Recommendation Categories

Azure Advisor organizes recommendations into five categories.

---

## Reliability

Recommendations that improve service availability and business continuity.

Examples include:

- Configure Azure Backup.
- Enable Azure Site Recovery.
- Use Availability Zones.
- Deploy redundant resources.
- Improve resiliency.

---

## Security

Recommendations that strengthen resource security.

Examples include:

- Enable Microsoft Defender for Cloud.
- Secure exposed resources.
- Apply security recommendations.
- Improve identity protection.
- Reduce security risks.

---

## Performance

Recommendations that improve workload efficiency.

Examples include:

- Resize Virtual Machines.
- Optimize storage performance.
- Reduce resource bottlenecks.
- Improve application responsiveness.

---

## Operational Excellence

Recommendations that improve administration and governance.

Examples include:

- Improve monitoring.
- Configure diagnostics.
- Apply governance recommendations.
- Increase operational visibility.

---

## Cost

Recommendations that reduce Azure spending.

Examples include:

- Right-size Virtual Machines.
- Remove idle resources.
- Purchase Reservations.
- Evaluate Savings Plans.
- Optimize storage costs.

Cost recommendations are among the most frequently tested Azure Advisor capabilities in the AZ-104 exam.

---

# Advisor Recommendation Workflow

```text
Azure Resources

↓

Platform Analysis

↓

Recommendation Generated

↓

Administrator Review

↓

Implement Recommendation

↓

Environment Optimized
```

Recommendations should be reviewed regularly as workloads evolve.

---

# Recommendation Severity

Recommendations are prioritized according to their expected operational impact.

Typical factors include:

- Potential cost savings
- Security exposure
- Availability improvements
- Performance gains
- Operational impact

This prioritization helps administrators address the most valuable recommendations first.

---

# Advisor Score

Azure Advisor includes an **Advisor Score** that helps organizations measure how closely their Azure environment aligns with Microsoft's recommended best practices.

Scores are presented:

- Overall Advisor Score
- Individual scores for each recommendation category

Categories include:

- Reliability
- Security
- Performance
- Operational Excellence
- Cost

Applying recommendations generally improves the corresponding score, while unresolved recommendations may reduce it.

The Advisor Score helps administrators:

- Measure governance maturity.
- Track operational improvements.
- Monitor optimization progress over time.
- Report cloud health to management.

> [!TIP]
> Advisor Score is intended as a governance indicator rather than a formal compliance metric.

---

# Azure Advisor and Cost Optimization

Azure Advisor plays a key role in Azure cost optimization.

Typical recommendations include:

- Resize oversized Virtual Machines.
- Delete unused Public IP Addresses.
- Remove unattached managed disks.
- Purchase Azure Reservations.
- Evaluate Azure Savings Plans.
- Optimize storage tiers.

Advisor should be reviewed regularly as part of operational cost management.

---

# Azure Advisor and Azure Monitor

Although both services analyze Azure resources, they serve different purposes.

| Azure Advisor | Azure Monitor |
|---------------|---------------|
| Best practice recommendations | Operational monitoring |
| Configuration optimization | Metrics and logs |
| Cost optimization | Alerting |
| Resource improvement | Incident detection |
| Governance recommendations | Operational visibility |

Both services complement each other and should be used together.

---

# Azure Advisor and Microsoft Defender for Cloud

Azure Advisor and Microsoft Defender for Cloud also complement each other.

| Azure Advisor | Microsoft Defender for Cloud |
|---------------|-----------------------------|
| Optimization recommendations | Security posture management |
| Performance improvements | Threat protection |
| Cost optimization | Vulnerability assessment |
| Reliability recommendations | Regulatory compliance |

Advisor focuses on optimization, while Defender focuses on security.

---

# Enterprise Scenario

A company operates hundreds of Azure resources.

Each month administrators review Azure Advisor to:

- Identify oversized Virtual Machines.
- Purchase Reservations.
- Remove idle resources.
- Improve monitoring.
- Increase workload resiliency.
- Apply security recommendations.

This continuous review improves both operational efficiency and financial governance.

---

# Scope and Resource Filtering

Azure Advisor supports filtering recommendations across different Azure scopes.

Recommendations can be reviewed at:

- Management Group
- Subscription
- Resource Group

Filtering allows administrators to focus on specific environments without affecting other workloads.

Typical scenarios include:

- Reviewing only production subscriptions.
- Analyzing a single business unit.
- Investigating one Resource Group.
- Separating development and production environments.

Using appropriate scopes simplifies operational reviews and improves governance in large Azure environments.

> [!TIP]
> Filtering recommendations helps administrators prioritize business-critical workloads while reducing operational noise.

---

# Managing Recommendations

Not every recommendation requires immediate implementation.

Azure Advisor provides two mechanisms for managing recommendations.

---

## Snooze

Snoozing temporarily hides a recommendation.

Typical use cases include:

- Planned maintenance windows.
- Seasonal workloads.
- Temporary operational exceptions.

After the selected period expires, the recommendation becomes visible again.

---

## Dismiss

Dismiss permanently hides a recommendation that is not applicable to the environment.

Typical examples include:

- Business-approved architectural decisions.
- Unsupported optimization scenarios.
- Accepted operational risks.

This helps administrators keep the Advisor dashboard focused on actionable recommendations.

> [!IMPORTANT]
> Recommendations should only be dismissed after confirming they are not appropriate for the workload.

---

# Common Pitfalls

- Ignoring Advisor recommendations.
- Assuming every recommendation should be implemented automatically.
- Reviewing Advisor only after cost problems appear.
- Focusing only on Cost recommendations.
- Ignoring Reliability recommendations.
- Forgetting to reassess recommendations after infrastructure changes.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Advisor purpose
> - Recommendation categories
> - Cost optimization recommendations
> - Reliability recommendations
> - Security recommendations
> - Performance recommendations
> - Operational Excellence recommendations
> - Advisor vs Azure Monitor
> - Advisor vs Microsoft Defender for Cloud

---

# Key Takeaways

- Azure Advisor continuously analyzes Azure resources and provides personalized recommendations based on Microsoft's best practices.
- Recommendations are grouped into Reliability, Security, Performance, Operational Excellence, and Cost categories.
- Azure Advisor complements Azure Monitor by focusing on resource optimization rather than operational monitoring.
- Reviewing Advisor regularly helps reduce costs, improve resilience, strengthen security, and optimize Azure workloads.
- Azure Advisor should be part of every administrator's routine operational review process.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Advisor documentation | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Advisor recommendations | https://learn.microsoft.com/azure/advisor/advisor-reference |
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Cost Optimization | https://learn.microsoft.com/azure/well-architected/cost-optimization/ |
| Reliability | https://learn.microsoft.com/azure/well-architected/reliability/ |
| Microsoft Learn – Optimize Azure resources with Azure Advisor | https://learn.microsoft.com/training/modules/optimize-costs-azure-advisor/ |
