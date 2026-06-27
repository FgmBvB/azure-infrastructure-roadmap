# Subscriptions

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

## Azure Resource Hierarchy

```text
          Root Management Group
                   │
         Management Group(s)
                   │
         Azure Subscription(s)
                   │
           Resource Group(s)
                   │
            Azure Resources
```

---

> [!TIP]
> **Key Concepts**
>
> * A subscription is the billing and management boundary in Azure.
> * Every Azure resource belongs to one subscription.
> * A subscription can contain multiple Resource Groups.
> * Access is controlled through Azure RBAC.
> * Subscriptions define quotas and service limits.
> * Multiple subscriptions can be organized using Management Groups.
> * Each subscription is associated with one Microsoft Entra ID tenant.

---

## Overview

An Azure Subscription is a logical container used to provision and manage Azure resources.

Every resource deployed in Azure belongs to a single subscription, which defines billing, access control, quotas, and resource organization.

Organizations commonly use multiple subscriptions to separate environments, departments, projects, or billing requirements.

---

## Purpose

Subscriptions help organizations organize cloud resources while providing clear boundaries for billing, governance, and administration.

They simplify cost management, improve security by isolating workloads, and allow administrators to apply different governance policies to different environments.

Using multiple subscriptions is a common strategy for managing enterprise-scale Azure environments.

---

## Architecture

Each Azure Subscription is associated with a single Microsoft Entra ID tenant.

A Microsoft Entra ID tenant can contain multiple Azure subscriptions, but each subscription is associated with only one tenant at a time.

Within a subscription, administrators create Resource Groups that contain Azure resources such as Virtual Machines, Storage Accounts, Virtual Networks, Databases, Key Vaults, and many other Azure services.

Permissions are assigned through Azure Role-Based Access Control (RBAC), while spending, governance, and service consumption are managed independently for each subscription.

Large organizations commonly organize multiple subscriptions using Management Groups, allowing Azure Policy, RBAC assignments, and governance settings to be inherited across subscriptions.

---

## Subscription Types

Microsoft offers several subscription types designed for different customers and business requirements.

Common subscription types include:

* Free Trial
* Pay-As-You-Go
* Enterprise Agreement (EA)
* Microsoft Customer Agreement (MCA)

Although billing models differ, Azure administration concepts remain the same across subscription types.

---

## Enterprise Scenario

A company has separate Development, Testing, and Production environments.

Instead of placing every workload into a single subscription, the organization creates three independent subscriptions:

* Development
* Testing
* Production

This approach improves security, simplifies billing, isolates workloads, and prevents development activities from affecting production resources.

Management Groups are then used to apply common governance policies across all subscriptions.

---

## Best Practices

* Use separate subscriptions for different environments when appropriate.
* Assign permissions using Azure RBAC.
* Monitor subscription costs regularly.
* Apply governance policies consistently.
* Use meaningful subscription names.
* Organize enterprise subscriptions using Management Groups.

---

## Common Pitfalls

* Deploying every workload into a single subscription.
* Confusing subscriptions with Resource Groups.
* Granting excessive permissions.
* Ignoring subscription quotas and limits.
* Failing to monitor subscription costs.
* Not planning the subscription hierarchy before deploying resources.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Azure Subscriptions
> * Billing boundaries
> * Management boundaries
> * Resource organization
> * Subscription limits and quotas
> * Microsoft Entra ID tenant relationship
> * Management Groups

---

## Key Takeaways

* Every Azure resource belongs to a single subscription.
* A subscription is the billing and management boundary in Azure.
* A Microsoft Entra ID tenant can contain multiple subscriptions.
* A subscription is associated with only one tenant at a time.
* Resource Groups organize resources within a subscription.
* Management Groups provide governance across multiple subscriptions.

---

## References

| Microsoft Documentation                                                                                                                                           | Purpose                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| [Organize your Azure resources effectively](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/initial-subscriptions)          | Subscription organization and enterprise design |
| [Azure Management Groups](https://learn.microsoft.com/azure/governance/management-groups/overview)                                                                | Management Groups hierarchy and governance      |
| [Azure Cost Management](https://learn.microsoft.com/azure/cost-management-billing/manage/)                                                                        | Billing and subscription management             |
| [Microsoft Learn – Describe Azure Architecture and Services](https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/) | Azure subscription fundamentals                 |
