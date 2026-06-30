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
