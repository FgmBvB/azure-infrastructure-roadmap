# Azure Reservations and Savings Plans

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Reservations, Azure Savings Plans, and Azure Hybrid Benefit, Microsoft's primary mechanisms for reducing long-term Azure infrastructure costs through pricing commitments and licensing optimization.

---

# Overview

Azure Reservations and Azure Savings Plans help organizations reduce cloud costs by committing to future resource consumption.

Unlike Pay-As-You-Go pricing, these purchasing models reward predictable usage with discounted pricing while maintaining automatic billing management through the Azure platform.

Understanding when to use Reservations versus Savings Plans is an important skill for both the AZ-104 exam and real-world Azure administration.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Reservations.
- Understand Azure Savings Plans.
- Compare Reservations and Savings Plans.
- Understand Azure Hybrid Benefit.
- Configure reservation scopes.
- Understand reservation matching.
- Understand Instance Size Flexibility (ISF).
- Understand reservation utilization.
- Understand the discount application order.
- Monitor reservation effectiveness.
- Apply Microsoft's cost optimization best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure Reservations, Savings Plans, Azure Hybrid Benefit, reservation scopes, automatic matching, Instance Size Flexibility (ISF), reservation utilization, pricing models, discount application order, and AZ-104 concepts. |
| **02 - Best Practices** | Workload analysis, scope selection, reservation optimization, Savings Plan strategy, Azure Hybrid Benefit, utilization monitoring, exchanges, cancellation considerations, Cost Management integration, and Microsoft's production recommendations. |

---

# Pricing Commitment Architecture

```text
Azure Resources

↓

Resource Consumption

↓

Pricing Evaluation

├── Reservations
├── Savings Plans
├── Azure Hybrid Benefit
└── Pay-As-You-Go

↓

Automatic Discount

↓

Reduced Azure Costs
```

Azure automatically evaluates eligible pricing benefits without requiring manual assignment.

---

# Core Components

This section covers the primary Azure pricing commitment mechanisms.

## Azure Reservations

- One-year or three-year commitments
- Resource-specific discounts
- Automatic matching
- Reservation scopes
- Highest savings for predictable workloads

---

## Azure Savings Plans

- One-year or three-year commitments
- Hourly spending commitment
- Flexible compute coverage
- Automatic discount application
- Ideal for changing workloads

---

## Azure Hybrid Benefit

- Reuse eligible Windows Server licenses
- Reuse eligible SQL Server licenses
- Lower licensing costs
- Can be combined with Reservations or Savings Plans where supported

---

## Cost Optimization

- Reservation utilization
- Instance Size Flexibility
- Reservation scope optimization
- Azure Advisor recommendations
- Azure Cost Management reporting

---

# Discount Application Flow

```text
Eligible Azure Resource

↓

Azure Reservations

↓

Azure Savings Plan

↓

Pay-As-You-Go
```

Azure Billing automatically applies the most beneficial eligible pricing option according to Microsoft's billing rules.

---

# Design Principles

Microsoft recommends following these principles:

- Analyze workloads before purchasing commitments.
- Use Reservations for stable workloads.
- Use Savings Plans for dynamic compute.
- Enable Azure Hybrid Benefit where eligible.
- Select the appropriate reservation scope.
- Monitor reservation utilization regularly.
- Review Azure Advisor recommendations.
- Track costs using Azure Cost Management.
- Reassess commitments as business requirements evolve.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Reservations
- Azure Savings Plans
- Azure Hybrid Benefit
- Reservation scopes
- Reservation matching
- Instance Size Flexibility
- Reservation utilization
- Discount application order
- Reservation exchanges
- Reservation lifecycle
- Cost optimization strategies

---

# Key Takeaways

- Azure Reservations provide the highest savings for predictable workloads by applying automatic discounts to eligible resources over one- or three-year commitments.
- Azure Savings Plans offer greater flexibility by applying discounts to eligible compute services based on a committed hourly spend rather than specific resource types.
- Azure Hybrid Benefit further reduces licensing costs by allowing eligible Windows Server and SQL Server licenses to be reused in Azure.
- Reservation utilization, Instance Size Flexibility, and appropriate scope selection are essential for maximizing long-term savings.
- Continuous monitoring with Azure Cost Management and Azure Advisor ensures pricing commitments remain aligned with changing business and infrastructure requirements.

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
| Microsoft Learn – Optimize Azure costs | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
