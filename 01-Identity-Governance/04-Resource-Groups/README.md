# Resource Groups

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

## Azure Resource Organization

```text
            Azure Subscription
                    │
         ┌──────────┴──────────┐
         │                     │
   Resource Group A      Resource Group B
         │                     │
   ┌─────┼─────┐          ┌────┼────┐
   │     │     │          │    │    │
 VM   Storage  VNet      SQL  VM  Key Vault
```

---

> [!TIP]
> **Key Concepts**
>
> - A Resource Group is a logical container for Azure resources.
> - Every Azure resource belongs to one Resource Group.
> - Resource Groups simplify management and organization.
> - Resources in a Resource Group can be managed together.
> - Access control and governance can be applied at the Resource Group level.

---

## Overview

An Azure Resource Group is a logical container that holds related Azure resources.

Resources such as Virtual Machines, Storage Accounts, Virtual Networks, Databases, and Key Vaults are deployed inside a Resource Group.

Resource Groups simplify administration by allowing related resources to be managed, monitored, secured, and organized together.

---

## Purpose

Resource Groups help administrators organize cloud resources according to projects, applications, environments, or business units.

They also provide a management boundary where permissions, policies, monitoring, automation, and resource lifecycle operations can be applied collectively.

Using Resource Groups improves operational efficiency and simplifies infrastructure management.

---

## Architecture

Every Azure resource must belong to exactly one Resource Group.

A Resource Group belongs to a single Azure Subscription, but it can contain different types of Azure resources located in different Azure Regions, depending on the service.

Resource Groups work together with Azure RBAC, Azure Policy, Resource Locks, and Tags to provide governance and resource management.

---

## Enterprise Scenario

A company deploys a web application composed of multiple Azure services.

To simplify administration, the organization creates a Resource Group named **RG-WebApp-Production** containing:

- Virtual Machine
- Virtual Network
- Storage Account
- Key Vault
- Network Security Group

Managing these resources together simplifies administration, monitoring, automation, and lifecycle management.

---

## Best Practices

- Group resources with the same lifecycle.
- Use consistent naming conventions.
- Apply Azure RBAC at the Resource Group level whenever appropriate.
- Use Tags for resource classification.
- Protect critical Resource Groups with Resource Locks.
- Avoid placing unrelated workloads in the same Resource Group.

---

## Common Pitfalls

- Creating one large Resource Group for every resource.
- Organizing Resource Groups by resource type instead of workload.
- Ignoring naming conventions.
- Applying excessive permissions.
- Forgetting to use Tags and Resource Locks.
- Deleting a Resource Group without understanding that all contained resources are also deleted.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Resource Groups
> - Resource organization
> - Resource lifecycle
> - Azure RBAC integration
> - Azure Policy integration
> - Resource Locks
> - Tags

---

## Key Takeaways

- Every Azure resource belongs to one Resource Group.
- Resource Groups organize related Azure resources.
- Resource Groups belong to a single Azure Subscription.
- Governance features such as RBAC, Policy, Locks, and Tags integrate with Resource Groups.
- Resources inside a Resource Group can be managed together.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager and Resource Groups |
| [Manage Azure Resource Groups](https://learn.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal) | Resource Group management |
| [Azure naming rules and restrictions](https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules) | Naming conventions |
| [Microsoft Learn – Describe Azure architecture and services](https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/) | Azure architecture fundamentals |
