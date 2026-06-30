# Azure Reservations and Savings Plans Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for maximizing savings with Azure Reservations, Azure Savings Plans, and Azure Hybrid Benefit while maintaining operational flexibility.

---

# Overview

Reservations and Savings Plans can significantly reduce Azure costs when applied correctly.

However, selecting the wrong pricing model or purchasing commitments without understanding workload behavior may reduce flexibility and decrease overall savings.

Microsoft recommends evaluating workload characteristics before committing to long-term pricing options.

---

# Understand Your Workloads

Before purchasing any commitment, analyze workload behavior.

Consider:

- Resource utilization
- Runtime patterns
- Seasonal demand
- Scaling behavior
- Regional deployment
- Future growth

Stable workloads benefit from Reservations, while dynamic workloads often benefit from Savings Plans.

---

# Use Reservations for Predictable Workloads

Reservations provide the greatest savings when workloads remain consistent.

Typical candidates include:

- Production Virtual Machines
- SQL databases
- Long-running App Services
- Persistent storage workloads

Avoid purchasing Reservations for resources that are frequently created and deleted.

---

# Use Savings Plans for Flexible Compute

Savings Plans are designed for organizations whose compute usage changes over time.

Ideal scenarios include:

- Development environments
- Test environments
- Autoscaling applications
- Mixed compute services
- Frequently resized Virtual Machines

Savings Plans provide greater flexibility than Reservations while still reducing compute costs.

---

# Maximize Reservation Utilization

Reservations only generate savings while matching resources are running.

Recommendations:

- Review utilization regularly.
- Choose the appropriate reservation scope.
- Avoid purchasing excessive capacity.
- Resize Virtual Machines carefully.
- Monitor workload changes.

Unused reservations reduce overall cost efficiency.

---

# Understand Instance Size Flexibility

Many Virtual Machine Reservations support **Instance Size Flexibility (ISF)**.

Benefits include:

- Resize VMs within the same supported VM family.
- Maintain reservation utilization.
- Reduce unused reservation capacity.
- Increase operational flexibility.

Review VM families before purchasing Reservations.

---

# Select the Correct Scope

Reservation scope directly affects utilization.

Available scopes include:

- Shared
- Management Group
- Subscription
- Resource Group (supported services)

Recommendations:

- Use Shared scope for centralized environments.
- Use Subscription scope for dedicated workloads.
- Periodically review scope assignments.

Choose the broadest scope that aligns with governance requirements.

---

# Combine Reservations with Azure Hybrid Benefit

Organizations with eligible Windows Server or SQL Server licenses should enable Azure Hybrid Benefit.

Benefits include:

- Lower licensing costs.
- Additional savings beyond Reservations.
- Better return on existing Microsoft investments.

Azure Hybrid Benefit and Reservations complement each other.

---

# Understand Discount Application Order

Azure automatically applies pricing benefits.

Order of evaluation:

```text
Eligible Compute Resource

↓

Azure Reservation

↓

Azure Savings Plan

↓

Pay-As-You-Go
```

Administrators do not manually assign discounts.

Azure Billing automatically applies the best available pricing benefit.

---

# Monitor Reservation Utilization

Regularly review:

- Utilization percentage
- Expiration dates
- Reservation scope
- Matching resources
- Savings achieved

Low utilization indicates that reservations should be reviewed or adjusted.

---

# Review Reservation Expiration

Reservations expire automatically at the end of their commitment.

Recommendations:

- Review upcoming expirations.
- Evaluate future workload demand.
- Compare Reservations with Savings Plans.
- Renew only when workloads remain predictable.

Do not automatically renew every Reservation.

---

# Evaluate Exchanges Carefully

Business requirements change over time.

Where supported, Reservation exchanges can help:

- Move to another VM family.
- Change Azure regions.
- Adapt to infrastructure evolution.

Review Microsoft's current exchange policies before making changes.

---

# Review Cancellation Policies

Reservation cancellations are governed by Microsoft's billing policies.

Before cancelling:

- Review current refund policies.
- Evaluate financial impact.
- Consider exchanging instead.
- Validate workload requirements.

Cancellation should normally be the last option.

---

# Use Azure Advisor

Azure Advisor continuously analyzes reservation opportunities.

Review recommendations for:

- Reservations
- Savings Plans
- VM rightsizing
- Underutilized resources

Advisor helps maximize long-term savings.

---

# Monitor Costs with Cost Management

Use Azure Cost Management to monitor:

- Reservation utilization
- Actual Cost
- Amortized Cost
- Forecasts
- Department spending

Regular reviews ensure pricing commitments continue delivering value.

---

# Plan for Growth

Long-term commitments should align with business strategy.

Consider:

- Planned migrations
- New applications
- Regional expansion
- Scaling requirements
- Hardware lifecycle

Avoid purchasing Reservations without understanding future infrastructure plans.

---

# Enterprise Scenario

A multinational company operates:

- Stable production workloads
- Autoscaling web applications
- Development subscriptions
- Existing Windows Server licenses

Recommended strategy:

- Reservations for production Virtual Machines.
- Savings Plans for autoscaling workloads.
- Azure Hybrid Benefit for Windows workloads.
- Shared reservation scope where appropriate.
- Monthly utilization reviews.
- Azure Advisor recommendations reviewed regularly.

This combination maximizes savings while preserving operational flexibility.

---

# Best Practices Checklist

- Analyze workloads before purchasing commitments.
- Use Reservations for predictable workloads.
- Use Savings Plans for dynamic compute.
- Enable Azure Hybrid Benefit when eligible.
- Understand Instance Size Flexibility.
- Select the correct reservation scope.
- Monitor reservation utilization.
- Review reservation expiration dates.
- Understand discount application order.
- Review exchange and cancellation policies.
- Use Azure Advisor recommendations.
- Track Actual and Amortized Cost.
- Review Cost Management dashboards regularly.

---

# Common Pitfalls

- Purchasing Reservations for short-lived workloads.
- Ignoring Instance Size Flexibility.
- Selecting an overly restrictive reservation scope.
- Forgetting Azure Hybrid Benefit.
- Never reviewing reservation utilization.
- Assuming Reservations require manual assignment.
- Ignoring reservation expiration.
- Confusing Reservations with Savings Plans.
- Cancelling Reservations without evaluating exchanges.
- Purchasing commitments without understanding future growth.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Reservations
> - Azure Savings Plans
> - Azure Hybrid Benefit
> - Instance Size Flexibility
> - Reservation scopes
> - Reservation utilization
> - Discount application order
> - Reservation exchanges
> - Reservation cancellations
> - Azure Advisor recommendations
> - Cost Management integration
> - Best practices for long-term cost optimization

---

# Key Takeaways

- Reservations provide the greatest savings for stable workloads, while Savings Plans offer more flexibility for changing compute consumption.
- Reservation utilization, scope selection, and Instance Size Flexibility directly influence the effectiveness of long-term pricing commitments.
- Azure automatically applies Reservations, Savings Plans, and Azure Hybrid Benefit where eligible, simplifying cost optimization.
- Regular reviews using Azure Cost Management and Azure Advisor help ensure commitments remain aligned with business needs.
- Long-term cost optimization requires balancing financial savings with operational flexibility and future growth plans.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Reservations | https://learn.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations |
| Manage Azure Reservations | https://learn.microsoft.com/azure/cost-management-billing/reservations/manage-reserved-vm-instance |
| Azure Savings Plans | https://learn.microsoft.com/azure/cost-management-billing/savings-plan/savings-plan-compute-overview |
| Azure Hybrid Benefit | https://learn.microsoft.com/azure/azure-hybrid-benefit/ |
| Azure Cost Management | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Well-Architected Framework – Cost Optimization | https://learn.microsoft.com/azure/well-architected/cost-optimization/ |
| Microsoft Learn – Optimize Azure costs | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
