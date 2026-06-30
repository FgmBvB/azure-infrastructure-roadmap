# Azure Advisor Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for using Azure Advisor to continuously optimize Azure environments, reduce costs, improve reliability, strengthen security, and support operational excellence.

---

# Overview

Azure Advisor should not be viewed as a one-time assessment tool.

Microsoft recommends incorporating Advisor into regular operational processes to continuously improve Azure environments as workloads evolve.

Advisor is most effective when combined with:

- Azure Monitor
- Microsoft Defender for Cloud
- Azure Cost Management
- Azure Policy
- Azure Well-Architected Framework

Continuous optimization leads to more reliable, secure, and cost-efficient Azure deployments.

---

# Review Advisor Regularly

Recommendations change as resources change.

Microsoft recommends reviewing Azure Advisor on a scheduled basis.

Typical review frequency:

- Weekly for production environments.
- Monthly for smaller environments.
- After major infrastructure deployments.
- After architectural changes.

Regular reviews prevent optimization opportunities from accumulating.

---

# Prioritize High-Impact Recommendations

Not every recommendation has the same operational value.

Prioritize recommendations that provide:

- High cost savings.
- Critical security improvements.
- Reliability enhancements.
- Performance gains.

Review the expected business impact before implementation.

---

# Use Advisor Score

Azure Advisor provides an **Advisor Score** that reflects how closely the environment aligns with Microsoft's recommended best practices.

Monitor both:

- Overall Advisor Score.
- Individual category scores.

Categories include:

- Reliability
- Security
- Performance
- Operational Excellence
- Cost

Improving recommendations over time increases the Advisor Score and provides a measurable indicator of governance maturity.

---

# Validate Recommendations Before Applying

Advisor recommendations should always be reviewed before implementation.

Consider:

- Business requirements.
- Application architecture.
- Service Level Agreements (SLAs).
- Compliance requirements.
- Operational impact.

Recommendations are guidance, not mandatory configuration changes.

---

# Integrate Advisor into Cost Optimization

Advisor is one of Microsoft's primary optimization tools.

Review recommendations related to:

- Virtual Machine rightsizing.
- Idle resources.
- Storage optimization.
- Reservations.
- Savings Plans.

Cost optimization should become part of regular operational reviews.

---

# Combine Advisor with Azure Monitor

Advisor identifies optimization opportunities.

Azure Monitor validates operational behavior.

Recommended workflow:

```text
Azure Monitor

↓

Operational Metrics

↓

Azure Advisor

↓

Optimization Recommendation

↓

Administrator Review

↓

Implementation

↓

Continuous Monitoring
```

Together they provide operational visibility and continuous improvement.

---

# Combine Advisor with Microsoft Defender for Cloud

Advisor and Microsoft Defender for Cloud provide complementary recommendations.

Advisor focuses on:

- Optimization
- Cost
- Reliability
- Performance

Defender focuses on:

- Security posture
- Threat protection
- Regulatory compliance
- Vulnerability assessment

Both services should be reviewed together.

---

# Manage Recommendations

Azure Advisor provides tools for reducing dashboard noise.

---

## Snooze

Use **Snooze** when a recommendation is temporarily not applicable.

Examples include:

- Planned maintenance.
- Seasonal workload increases.
- Temporary business exceptions.

The recommendation reappears automatically after the selected period.

---

## Dismiss

Use **Dismiss** only when a recommendation is permanently not applicable.

Examples include:

- Approved architectural decisions.
- Accepted business risks.
- Unsupported optimization scenarios.

Dismissing inappropriate recommendations keeps the dashboard focused on actionable improvements.

---

# Filter Recommendations by Scope

Large Azure environments may contain hundreds of recommendations.

Use Azure scopes to focus analysis.

Supported scopes include:

- Management Group
- Subscription
- Resource Group

Filtering helps administrators:

- Separate Production and Development.
- Review individual business units.
- Focus on critical workloads.
- Reduce operational noise.

---

# Track Advisor Trends

Advisor should be reviewed over time rather than as isolated snapshots.

Track:

- Advisor Score improvements.
- Cost savings achieved.
- Recommendation trends.
- Remaining optimization opportunities.
- Previously implemented recommendations.

Trend analysis supports continuous improvement.

---

# Implement Governance

Advisor recommendations should complement organizational governance.

Recommendations include:

- Apply Azure Policy.
- Standardize resource deployment.
- Review Azure RBAC assignments.
- Monitor compliance.
- Maintain documentation.

Governance reduces recurring configuration issues.

---

# Automate Operational Reviews

Although Azure Advisor recommendations require administrator review, operational processes can be automated.

Examples include:

- Scheduled review meetings.
- Automated reporting.
- Dashboard integration.
- Cost review workflows.
- Governance reporting.

Automation improves consistency across large environments.

---

# Do Not Optimize Cost Alone

Cost should never be the only optimization objective.

Always balance:

- Cost
- Reliability
- Security
- Performance
- Operational Excellence

Reducing costs should never compromise business requirements.

---

# Enterprise Scenario

A multinational organization operates hundreds of Azure subscriptions.

The cloud operations team:

- Reviews Advisor weekly.
- Tracks Advisor Score.
- Filters recommendations by Management Group.
- Prioritizes high-impact recommendations.
- Reviews Cost recommendations with Finance.
- Reviews Security recommendations with the Security team.
- Documents implemented improvements.

This structured process enables continuous optimization while maintaining governance and operational stability.

---

# Best Practices Checklist

- Review Advisor regularly.
- Track Advisor Score.
- Prioritize high-impact recommendations.
- Validate recommendations before implementation.
- Integrate Advisor with Azure Monitor.
- Review Microsoft Defender for Cloud recommendations.
- Review Cost recommendations frequently.
- Filter recommendations by scope.
- Use Snooze for temporary exceptions.
- Use Dismiss only for justified permanent exceptions.
- Apply Azure Policy where appropriate.
- Track optimization trends.
- Balance cost with reliability, security, and performance.

---

# Common Pitfalls

- Ignoring Advisor recommendations.
- Applying every recommendation without validation.
- Focusing only on Cost recommendations.
- Never reviewing Advisor Score.
- Leaving outdated recommendations unresolved.
- Using Dismiss instead of Snooze for temporary situations.
- Optimizing costs at the expense of reliability.
- Reviewing Advisor only during incidents.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Advisor recommendation categories
> - Advisor Score
> - Recommendation prioritization
> - Snooze vs Dismiss
> - Scope filtering
> - Advisor with Azure Monitor
> - Advisor with Microsoft Defender for Cloud
> - Cost optimization recommendations
> - Governance best practices

---

# Key Takeaways

- Azure Advisor should be integrated into regular operational reviews rather than used only during troubleshooting or cost reduction initiatives.
- Recommendations should be validated against business, security, and architectural requirements before implementation.
- Advisor Score, recommendation trends, and scope filtering help administrators measure optimization progress and focus on the most important workloads.
- Azure Advisor complements Azure Monitor, Microsoft Defender for Cloud, Azure Policy, and Cost Management to provide continuous improvement across the Azure environment.
- Successful Azure administration requires balancing cost optimization with reliability, security, performance, and operational excellence.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Advisor documentation | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Advisor recommendations | https://learn.microsoft.com/azure/advisor/advisor-reference |
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Cost Management | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/defender-for-cloud-introduction |
| Azure Policy | https://learn.microsoft.com/azure/governance/policy/overview |
| Microsoft Learn – Optimize Azure resources with Azure Advisor | https://learn.microsoft.com/training/modules/optimize-costs-azure-advisor/ |
