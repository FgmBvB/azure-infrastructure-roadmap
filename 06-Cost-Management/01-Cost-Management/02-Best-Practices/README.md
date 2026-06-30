# Azure Cost Management Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for monitoring, controlling, optimizing, and governing Azure costs across subscriptions and enterprise environments.

---

# Overview

Effective cloud cost management is an ongoing operational process rather than a one-time activity.

Microsoft recommends combining financial governance, resource optimization, automation, and continuous monitoring to maintain predictable Azure spending while ensuring business requirements continue to be met.

A mature cost management strategy should focus on:

- Visibility
- Governance
- Automation
- Optimization
- Accountability

---

# Build a Cost Governance Strategy

Cost optimization starts before resources are deployed.

Recommendations:

- Define ownership for every workload.
- Apply consistent naming conventions.
- Standardize tagging.
- Separate Production and Development subscriptions.
- Review costs regularly.

Well-defined governance simplifies financial reporting and accountability.

---

# Organize Resources with Tags

Tags are essential for financial management.

Recommended tags include:

- Environment
- Department
- Cost Center
- Project
- Owner
- Application

Example:

| Tag | Value |
|------|-------|
| Environment | Production |
| CostCenter | Finance |
| Owner | Infrastructure Team |

Tags enable:

- Chargeback
- Showback
- Cost Analysis filtering
- Budget reporting

---

# Tag Inheritance

Tags are essential for governance and cost allocation.

However, Azure Resource Manager **does not automatically inherit tags** from a Resource Group to the resources it contains.

Example:

```text
Resource Group
CostCenter = Finance

↓

Virtual Machine

↓

No tags assigned automatically
```

This behavior can lead to incomplete Cost Analysis reports and inaccurate chargeback calculations.

---

## Automating Tag Inheritance

Microsoft recommends using **Azure Policy** to enforce organizational tagging standards.

Common built-in policies can:

- Copy tags from the Resource Group.
- Require mandatory tags.
- Append missing tags.
- Modify resources during deployment.

These policies help maintain consistent financial reporting without manual intervention.

> [!IMPORTANT]
> Resource Group tags are **not inherited automatically**. Azure Policy should be used whenever automatic tag inheritance is required.

---

# Create Budgets Early

Budgets should be created before significant workloads are deployed.

Recommendations:

- Create subscription budgets.
- Create department budgets.
- Define multiple notification thresholds.
- Review budgets monthly.

Budgets improve financial visibility but do not automatically stop Azure resources.

---

# Automate Cost Responses

Budgets become more powerful when combined with automation.

Typical workflow:

```text
Budget Threshold

↓

Azure Monitor Alert

↓

Action Group

↓

Automation Runbook
Azure Function
Logic App

↓

Automatic Remediation
```

Possible remediation actions include:

- Stop development Virtual Machines.
- Deallocate idle resources.
- Notify administrators.
- Create ITSM incidents.
- Trigger approval workflows.

Automation reduces unnecessary spending without requiring manual intervention.

---

# Monitor Spending Regularly

Review Azure spending frequently.

Recommendations:

- Analyze monthly trends.
- Compare departments.
- Identify abnormal spending.
- Review new resource deployments.
- Investigate unexpected cost increases.

Frequent reviews prevent billing surprises.

---

# Use Cost Analysis Effectively

Cost Analysis should become part of operational reviews.

Analyze costs by:

- Subscription
- Resource Group
- Resource
- Service
- Region
- Tags

Use filtering to identify expensive workloads and optimization opportunities.

---

# Understand Cost Views

Different reports serve different business purposes.

| View | Recommended Use |
|------|------------------|
| Actual Cost | Invoice reconciliation |
| Amortized Cost | Internal reporting and reservation analysis |

Actual Cost reflects invoice charges.

Amortized Cost distributes Reservation and Savings Plan costs across the resources consuming those benefits.

Choose the appropriate view depending on the reporting objective.

---

# Understand Billing Data Latency

Azure billing information is not updated in real time.

Resource usage must first be processed before appearing in Cost Management.

Implications include:

- Recent deployments may not appear immediately.
- Budgets evaluate processed billing data.
- Cost Analysis should not be used for real-time operational monitoring.

Allow sufficient time before investigating apparent discrepancies.

---

# Optimize Compute Resources

Virtual Machines often represent the largest Azure expense.

Recommendations:

- Right-size Virtual Machines.
- Stop unused development VMs.
- Deallocate VMs when not required.
- Remove obsolete disks.
- Remove unused Public IP Addresses.
- Review VM utilization regularly.

Use Azure Advisor recommendations whenever possible.

---

# Virtual Machine Power States and Cost

Stopping a Virtual Machine does not always stop billing.

Azure distinguishes between two important VM states.

| VM State | Compute Charges | Description |
|----------|-----------------|-------------|
| **Stopped** | Yes | The operating system has shut down, but Azure still reserves the underlying compute resources. |
| **Stopped (Deallocated)** | No | Azure releases the compute resources. Charges continue only for storage and other allocated resources such as managed disks or static public IP addresses. |

---

## Best Practice

Development and testing Virtual Machines should always be **Stopped (Deallocated)** when not in use.

This can be automated using:

- Azure Automation
- Azure CLI
- Azure PowerShell
- Azure Functions
- Logic Apps

> [!TIP]
> Shutting down a VM from inside the guest operating system does **not** stop compute billing.

---

# Optimize Storage Costs

Storage costs accumulate over time.

Recommendations:

- Use Lifecycle Management.
- Delete obsolete snapshots.
- Archive inactive data.
- Select appropriate redundancy.
- Choose the correct Access Tier.

Storage optimization should balance performance, availability, and cost.

---

# Review Azure Advisor Recommendations

Azure Advisor continuously analyzes Azure resources.

Typical recommendations include:

- Resize Virtual Machines.
- Purchase Reservations.
- Remove idle resources.
- Optimize storage.
- Improve resource utilization.

Advisor recommendations should be reviewed periodically.

---

# Use Reservations and Savings Plans

Predictable workloads should take advantage of long-term pricing benefits.

Recommendations:

- Purchase Azure Reservations for stable workloads.
- Evaluate Azure Savings Plans for variable compute usage.
- Monitor reservation utilization.
- Review recommendations from Azure Advisor.

Reservations significantly reduce long-term operational costs.

---

# Azure Hybrid Benefit and Reservation Matching

Microsoft provides additional cost-saving mechanisms beyond Reservations.

---

## Azure Hybrid Benefit

Azure Hybrid Benefit allows eligible Windows Server and SQL Server licenses with Software Assurance or qualifying subscription benefits to be reused in Azure.

Benefits include:

- Lower Virtual Machine licensing costs.
- Reduced SQL Server licensing costs.
- Better return on existing Microsoft licensing investments.

Azure Hybrid Benefit can be combined with Reservations or Savings Plans where supported.

---

## Reservation Matching

Reservations are billing discounts rather than resource assignments.

Azure automatically evaluates eligible running resources and applies Reservation discounts whenever a matching resource exists.

Matching considers factors such as:

- Region
- Resource type
- VM size or VM family
- Reservation scope

No manual assignment to individual Virtual Machines is required.

> [!IMPORTANT]
> Reservations reduce billing automatically only while matching resources are running within the selected reservation scope.

---

# Secure Cost Information

Financial information is sensitive.

Recommendations:

- Apply least privilege.
- Separate Azure RBAC from billing roles.
- Review billing permissions regularly.
- Protect financial reports.
- Audit access periodically.

Not every Azure administrator requires billing access.

---

# Understand Billing Scopes

Azure separates resource administration from billing administration.

Azure Resource Manager scopes include:

- Management Groups
- Subscriptions
- Resource Groups
- Resources

Billing scopes include:

- Billing Account
- Billing Profile
- Invoice Section

Depending on the organization's billing agreement, additional billing permissions may be required before users can view cost information.

This separation improves financial governance.

---

# Export Cost Data

Organizations often require external reporting.

Recommendations:

- Export cost data automatically.
- Store exports securely.
- Build Power BI dashboards.
- Integrate with financial systems.
- Archive historical reports.

Exports support enterprise reporting and auditing.

---

# Monitor Cost Trends

Do not focus only on monthly invoices.

Track:

- Daily spending
- Weekly trends
- Resource growth
- Reservation utilization
- Forecast accuracy

Trend analysis enables proactive optimization.

---

# Enterprise Scenario

A global company operates multiple Azure subscriptions.

Microsoft recommends:

- Standardized tagging.
- Department budgets.
- Monthly Cost Analysis reviews.
- Automated budget notifications.
- Azure Advisor optimization reviews.
- Reservation utilization monitoring.
- Automated shutdown of development Virtual Machines outside business hours.

The organization achieves predictable spending while maintaining operational flexibility.

---

# Best Practices Checklist

- Define cost governance.
- Apply standardized tags.
- Create budgets early.
- Configure multiple budget thresholds.
- Automate budget responses.
- Review Cost Analysis regularly.
- Understand billing data latency.
- Use the correct cost view.
- Optimize compute resources.
- Optimize storage costs.
- Review Azure Advisor recommendations.
- Use Reservations and Savings Plans.
- Export cost reports.
- Secure billing information.
- Review spending trends continuously.

---

# Common Pitfalls

- Assuming budgets stop resources automatically.
- Deploying resources without tags.
- Ignoring Azure Advisor recommendations.
- Leaving Virtual Machines running unnecessarily.
- Using Actual Cost when Amortized Cost is required.
- Forgetting billing data latency.
- Granting excessive billing permissions.
- Never reviewing reservation utilization.
- Ignoring daily spending trends.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Cost Analysis
> - Budgets
> - Cost Alerts
> - Action Groups
> - Cost Automation
> - Billing Scopes
> - Azure RBAC vs Billing Roles
> - Actual Cost vs Amortized Cost
> - Billing latency
> - Cost Allocation
> - Azure Advisor
> - Reservations
> - Savings Plans
> - Cost optimization best practices

---

# Key Takeaways

- Cost optimization should be integrated into everyday Azure operations rather than treated as a periodic financial review.
- Budgets, Cost Analysis, Azure Advisor, and automation work together to provide visibility, governance, and proactive cost control.
- Proper tagging, billing permissions, and resource organization improve financial reporting and accountability.
- Understanding billing scopes, cost views, and billing data latency helps administrators interpret Azure cost information correctly.
- Continuous optimization, automation, and governance enable organizations to reduce unnecessary spending while maintaining reliable cloud services.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cost Management documentation | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Cost Analysis | https://learn.microsoft.com/azure/cost-management-billing/costs/cost-analysis-common-uses |
| Budgets | https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets |
| Cost exports | https://learn.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data |
| Azure pricing | https://azure.microsoft.com/pricing/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Well-Architected Framework – Cost Optimization | https://learn.microsoft.com/azure/well-architected/cost-optimization/ |
| Microsoft Learn – Control and organize Azure costs | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
