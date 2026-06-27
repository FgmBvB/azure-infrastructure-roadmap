# Subscriptions

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

## Azure Subscription Hierarchy

```text
                 Microsoft Entra ID
                        │
               Azure Subscription
                        │
        ┌───────────────┼───────────────┐
        │               │               │
 Resource Group   Resource Group   Resource Group
        │               │               │
     Resources       Resources      Resources
```

---

> [!TIP]
> **Key Concepts**
>
> - A subscription is the billing and management boundary in Azure.
> - Every Azure resource belongs to a subscription.
> - A subscription can contain multiple Resource Groups.
> - Access is controlled through Azure RBAC.
> - Subscriptions define quotas and service limits.

---

## Overview

An Azure Subscription is a logical container used to provision and manage Azure resources.

Every resource deployed in Azure belongs to a single subscription, which defines billing, access control, quotas, and resource organization.

Organizations commonly use multiple subscriptions to separate environments, departments, projects, or billing requirements.

---

## Purpose

Subscriptions help organizations organize cloud resources while providing clear boundaries for billing, governance, and administration.

They also simplify cost management, improve security by isolating workloads, and allow administrators to apply different governance policies to different environments.

Using multiple subscriptions is a common strategy for managing enterprise-scale Azure environments.

---

## Architecture

Each Azure Subscription is associated with a Microsoft Entra ID tenant.

Within a subscription, administrators create Resource Groups that contain Azure resources such as Virtual Machines, Storage Accounts, Virtual Networks, and Databases.

Permissions are assigned through Azure Role-Based Access Control (RBAC), while spending and service consumption are tracked independently for each subscription.

---

## Enterprise Scenario

A company has separate Development, Testing, and Production environments.

Instead of placing every resource inside a single subscription, the organization creates three subscriptions:

- Development Subscription
- Testing Subscription
- Production Subscription

This approach improves security, simplifies billing, and prevents development workloads from affecting production resources.

---

## Best Practices

- Use separate subscriptions for different environments when appropriate.
- Assign permissions using Azure RBAC.
- Monitor costs for each subscription.
- Apply governance policies consistently.
- Use meaningful subscription names.

---

## Common Pitfalls

- Deploying every workload into a single subscription.
- Confusing subscriptions with Resource Groups.
- Granting excessive permissions.
- Ignoring subscription quotas and limits.
- Not monitoring subscription costs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Subscriptions
> - Billing boundaries
> - Management boundaries
> - Resource organization
> - Subscription limits and quotas

---

## Key Takeaways

- Every Azure resource belongs to one subscription.
- A subscription is the billing boundary.
- Subscriptions provide administrative isolation.
- Multiple subscriptions improve governance.
- RBAC controls access within subscriptions.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/initial-subscriptions | Subscription design recommendations |
| https://learn.microsoft.com/azure/cost-management-billing/manage/ | Billing and cost management |
| https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/ | Azure subscription fundamentals |
