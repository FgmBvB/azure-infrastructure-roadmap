# Azure Reservations and Savings Plans Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Reservations and Azure Savings Plans, Microsoft's primary long-term pricing options for reducing Azure costs on predictable workloads.

---

# Overview

Azure provides several pricing models to help organizations optimize cloud spending.

While the default **Pay-As-You-Go** model offers maximum flexibility, organizations running stable workloads can significantly reduce costs by committing to longer usage periods.

The two primary discount mechanisms are:

- **Azure Reservations**
- **Azure Savings Plans for Compute**

Both reduce Azure costs, but they operate differently and are designed for different workload patterns.

---

# Azure Pricing Models

Azure commonly offers four pricing approaches.

| Pricing Model | Best For |
|---------------|----------|
| Pay-As-You-Go | Variable or unpredictable workloads |
| Azure Reservations | Stable, predictable workloads |
| Azure Savings Plans | Variable compute workloads |
| Azure Hybrid Benefit | Existing eligible Microsoft licenses |

Choosing the appropriate pricing model is an important part of Azure cost optimization.

---

# Azure Reservations

Azure Reservations provide discounted pricing by committing to resource usage for either:

- 1 year
- 3 years

Reservations are available for several Azure services, including:

- Virtual Machines
- Azure SQL Database
- Azure SQL Managed Instance
- Azure Cosmos DB
- App Service
- Azure Files
- Managed Disks (selected scenarios)

Reservations apply automatically to eligible resources without requiring manual assignment.

---

# Reservation Architecture

```text
Reservation Purchased

↓

Billing Platform

↓

Matching Azure Resources

↓

Automatic Discount Applied

↓

Reduced Monthly Cost
```

Reservations are billing benefits rather than configuration changes applied directly to resources.

---

# Reservation Scope

Reservations can be assigned to different scopes.

Supported scopes include:

- Shared Scope
- Management Group
- Subscription
- Resource Group (supported services)

---

## Shared Scope

The reservation discount can be applied to matching resources across all eligible subscriptions within the billing context.

---

## Management Group Scope

Reservations can be shared across subscriptions within a Management Group where supported.

---

## Subscription Scope

The discount is limited to a single subscription.

---

## Resource Group Scope

Some reservation types support restricting benefits to a specific Resource Group.

Choosing the correct scope improves reservation utilization.

---

# Reservation Matching

Azure continuously evaluates deployed resources.

Reservation discounts are automatically applied whenever matching resources are running.

Matching considers factors such as:

- Resource type
- Azure region
- VM family
- VM size flexibility (when supported)
- Reservation scope

Administrators do not manually assign reservations to individual resources.

---

# Instance Size Flexibility

Virtual Machine Reservations support **Instance Size Flexibility (ISF)** for many VM series.

Instead of matching only a single VM size, Azure can automatically apply a reservation to different VM sizes within the same supported family.

Example:

```text
Reservation

↓

Standard_E4s_v3

↓

Automatically matches

• 1 × Standard_E4s_v3

or

• 2 × Standard_E2s_v3

(if supported by the flexibility ratio)
```

Azure uses an internal flexibility ratio to determine how reservation capacity is distributed across eligible VM sizes.

Benefits include:

- Better reservation utilization.
- Greater operational flexibility.
- Reduced waste when resizing Virtual Machines.

> [!TIP]
> Instance Size Flexibility allows reservations to continue providing savings even when Virtual Machines are resized within the same supported VM family.

---

# Azure Savings Plans

Azure Savings Plans provide pricing discounts for compute workloads without requiring commitment to a specific VM family.

Instead of reserving a particular resource, organizations commit to a fixed hourly spending amount for either:

- 1 year
- 3 years

Azure automatically applies discounts to eligible compute services until the committed hourly amount is reached.

---

# Savings Plan Architecture

```text
Hourly Spend Commitment

↓

Eligible Compute Resources

↓

Automatic Discount

↓

Reduced Compute Cost
```

Savings Plans provide greater flexibility than Reservations while still reducing long-term costs.

---

# Reservations vs Savings Plans

| Feature | Reservations | Savings Plans |
|----------|--------------|---------------|
| Commitment | Specific resources | Hourly spend |
| Flexibility | Lower | Higher |
| Discount | Typically higher | Typically lower |
| Best For | Stable workloads | Dynamic workloads |
| Automatic matching | Yes | Yes |

Organizations often combine both approaches.

---

# Discount Application Order

Azure applies available pricing benefits automatically following a defined order.

```text
Eligible Compute Resource

↓

Azure Reservation

↓

Azure Savings Plan

↓

Pay-As-You-Go
```

### Azure Reservations

Reservations are evaluated first because they apply to specific eligible resources.

---

### Azure Savings Plans

If no Reservation applies, Azure evaluates any available Savings Plan commitment.

---

### Pay-As-You-Go

Any remaining eligible usage that is not covered by Reservations or Savings Plans is billed at standard Pay-As-You-Go rates.

> [!IMPORTANT]
> Administrators do not manually select which discount is applied. Azure Billing automatically applies the pricing benefit that best matches the eligible resource usage.

---

# Azure Hybrid Benefit

Azure Hybrid Benefit allows organizations to reuse eligible Windows Server and SQL Server licenses in Azure.

Benefits include:

- Lower licensing costs.
- Reduced Virtual Machine costs.
- Better utilization of existing Microsoft licenses.

Azure Hybrid Benefit can be combined with Reservations or Savings Plans where supported.

---

# Reservation Lifecycle

```text
Purchase Reservation

↓

Azure Billing Platform

↓

Automatic Matching

↓

Discount Applied

↓

Monitor Utilization

↓

Renew or Modify Strategy
```

Administrators should periodically review reservation utilization to maximize savings.

---

# Reservation Exchanges and Cancellations

Business requirements may change during the reservation term.

Azure supports options for modifying reservation commitments.

---

## Reservation Exchanges

Where supported, eligible reservations can be exchanged for different reservations.

Typical scenarios include:

- Changing VM families.
- Moving to different regions.
- Increasing reservation value.

The replacement reservation must satisfy Microsoft's exchange requirements.

---

## Reservation Cancellations

Microsoft also supports reservation cancellations in eligible scenarios.

Cancellation policies, refund eligibility, and financial limits are governed by Microsoft's current reservation terms and billing agreement.

Administrators should always verify the current Microsoft documentation before planning reservation cancellations.

> [!IMPORTANT]
> Reservation exchanges and cancellations are subject to Microsoft's current policies, which may change over time depending on the billing agreement and reservation type.

---

# Reservation Utilization

A reservation only generates savings while matching eligible running resources.

Low utilization may occur when:

- Resources are deleted.
- Workloads move to another region.
- VM sizes change.
- Reservation scope is too restrictive.

Microsoft recommends monitoring utilization regularly.

---

# Enterprise Scenario

A company operates:

- Stable production Virtual Machines.
- Dynamic development environments.
- Existing Windows Server licenses.

Recommended strategy:

- Reservations for production workloads.
- Savings Plans for development workloads.
- Azure Hybrid Benefit for eligible Windows Server licenses.
- Regular utilization reviews.

This approach balances flexibility with maximum cost savings.

---

# Common Pitfalls

- Purchasing Reservations for unstable workloads.
- Using Savings Plans for highly predictable workloads that would benefit more from Reservations.
- Choosing an incorrect reservation scope.
- Ignoring reservation utilization.
- Forgetting Azure Hybrid Benefit.
- Assuming Reservations require manual assignment.
- Leaving reservations underutilized.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Reservations
> - Azure Savings Plans
> - Azure Hybrid Benefit
> - Reservation scopes
> - Reservation matching
> - Reservation utilization
> - Reservations vs Savings Plans
> - Cost optimization strategies

---

# Key Takeaways

- Azure Reservations and Azure Savings Plans help reduce long-term Azure costs by applying automatic billing discounts to eligible workloads.
- Reservations are best suited for stable, predictable resources, while Savings Plans provide greater flexibility for changing compute workloads.
- Reservation discounts are applied automatically by the Azure billing platform based on matching criteria such as region, resource type, scope, and eligible compute resources.
- Azure Hybrid Benefit further reduces licensing costs by allowing eligible Windows Server and SQL Server licenses to be reused in Azure.
- Regularly reviewing reservation utilization and selecting the appropriate scope are essential to maximizing cost savings.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Reservations | https://learn.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations |
| Azure Savings Plans | https://learn.microsoft.com/azure/cost-management-billing/savings-plan/savings-plan-compute-overview |
| Azure Hybrid Benefit | https://learn.microsoft.com/azure/azure-hybrid-benefit/ |
| Reservation management | https://learn.microsoft.com/azure/cost-management-billing/reservations/manage-reserved-vm-instance |
| Azure pricing | https://azure.microsoft.com/pricing/ |
| Azure Cost Management | https://learn.microsoft.com/azure/cost-management-billing/cost-management-billing-overview |
| Microsoft Learn – Optimize Azure costs with Reservations and Savings Plans | https://learn.microsoft.com/training/modules/control-spending-manage-bills-azure/ |
