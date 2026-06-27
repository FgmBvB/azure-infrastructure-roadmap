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
> - A Resource Group belongs to one Azure Subscription.
> - Resources inside a Resource Group can be managed together.
> - RBAC, Azure Policy, Resource Locks, and Tags can be applied at the Resource Group scope.
> - Moving resources between Resource Groups or subscriptions has governance and dependency implications.

---

## Overview

An Azure Resource Group is a logical container used to manage related Azure resources.

Resources such as Virtual Machines, Storage Accounts, Virtual Networks, Databases, and Key Vaults are deployed inside Resource Groups.

Resource Groups simplify administration by allowing related resources to be organized, monitored, secured, automated, and managed together.

---

## Purpose

Resource Groups help administrators organize cloud resources according to applications, environments, projects, or business units.

They provide a management scope where permissions, policies, locks, monitoring, automation, and lifecycle operations can be applied collectively.

Using Resource Groups correctly improves operational efficiency, governance, security, cost tracking, and infrastructure lifecycle management.

---

## Architecture

Every Azure resource must belong to exactly one Resource Group.

A Resource Group belongs to a single Azure Subscription, but it can contain resources located in different Azure Regions, depending on the service.

When a Resource Group is created, Azure requires a region. This location stores the metadata for the Resource Group, not the resources themselves.

If the Resource Group's metadata region becomes unavailable, resources running in other Azure Regions continue operating. However, management operations such as creating, updating, or deleting resources within that Resource Group may be temporarily unavailable.

Resource Groups are managed through Azure Resource Manager (ARM), which provides the management layer used to deploy, update, organize, and control Azure resources.

Resource Groups work together with Azure RBAC, Azure Policy, Resource Locks, and Tags to provide governance and resource management.

---

## Resource Movement

Azure resources can be moved between Resource Groups or between subscriptions, but not every resource type supports move operations.

Before moving resources, administrators should validate whether the resource type supports movement and check any dependencies.

During a move operation, both the source and destination Resource Groups are temporarily locked for write and delete operations.

Moving a resource changes its management scope and may affect automation, scripts, monitoring, dependencies, RBAC inheritance, Azure Policy assignments, and other governance configurations.

---

## Resource Locks

Resource Locks can be applied at the subscription, Resource Group, or resource scope to help prevent accidental deletion or modification.

When a lock is applied at the Resource Group level, resources inside that Resource Group inherit the lock.

There are two lock types:

- **CanNotDelete**: resources can be modified but cannot be deleted.
- **ReadOnly**: resources become read-only and update operations are blocked.

Many Azure operations that appear to be read actions actually require write operations through Azure Resource Manager. As a result, a ReadOnly lock can prevent operations such as starting or stopping a Virtual Machine.

Resource Locks take precedence over RBAC permissions. Even users with high-level roles may be prevented from modifying or deleting locked resources.

---

## ARM and Bicep Deployments

Resource Groups are the most common deployment scope for ARM templates and Bicep files.

Azure Resource Manager supports two deployment modes:

- **Incremental mode** adds or updates resources without deleting resources that are not included in the template.
- **Complete mode** removes resources from the Resource Group if they are not defined in the deployment template.

Because Complete mode can delete existing resources, it should only be used when the desired state of the Resource Group is fully defined.

---

## Limits and Quotas

Azure applies limits and quotas to Resource Groups, subscriptions, deployments, and individual services.

Deployment history is also maintained for each Resource Group. When the deployment history reaches the supported platform limit, older deployment records should be removed before creating new deployments.

Because Azure limits may change over time, administrators should always verify current values in the official Microsoft documentation before designing large-scale environments.

---

## Enterprise Scenario

A company deploys a production web application composed of multiple Azure services.

To simplify administration, the organization creates a Resource Group named **RG-WebApp-Production** containing:

- Virtual Machine
- Virtual Network
- Storage Account
- Key Vault
- Network Security Group

Managing these resources together simplifies administration, monitoring, automation, access control, cost tracking, and lifecycle management.

---

## Best Practices

- Group resources with the same lifecycle.
- Use consistent naming conventions.
- Apply Azure RBAC at the Resource Group level when appropriate.
- Use Tags for resource classification and cost management.
- Protect critical Resource Groups with Resource Locks.
- Avoid placing unrelated workloads in the same Resource Group.
- Validate dependencies before moving resources.
- Review limits and quotas when designing large environments.

---

## Common Pitfalls

- Creating one large Resource Group for every resource.
- Organizing Resource Groups by resource type instead of workload lifecycle.
- Ignoring naming conventions.
- Applying excessive permissions.
- Forgetting to use Tags and Resource Locks.
- Deleting a Resource Group without understanding that all contained resources are also deleted.
- Moving resources without checking supported resource types and dependencies.
- Using Complete deployment mode without understanding its impact.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Resource Groups
> - Azure Resource Manager
> - Resource organization
> - Resource lifecycle
> - Resource movement
> - Resource Locks
> - RBAC inheritance
> - Azure Policy integration
> - Tags
> - ARM and Bicep deployment modes
> - Resource Group metadata location
> - Limits and quotas

---

## Key Takeaways

- Every Azure resource belongs to one Resource Group.
- Resource Groups belong to a single Azure Subscription.
- Resource Groups are logical management containers.
- Resource Groups store metadata in a specific Azure Region.
- Governance features such as RBAC, Policy, Locks, and Tags integrate with Resource Groups.
- Resource movement requires planning and validation.
- Resource Locks help protect critical resources.
- ARM and Bicep deployments commonly target Resource Groups.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager and Resource Groups |
| [Manage Azure Resource Groups](https://learn.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal) | Resource Group management |
| [Move resources to a new Resource Group or subscription](https://learn.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription) | Resource movement |
| [Lock your Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource Locks |
| [ARM deployment modes](https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes) | Incremental and Complete deployment modes |
| [Azure subscription and service limits](https://learn.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) | Azure limits and quotas |
| [Azure naming rules and restrictions](https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules) | Naming conventions |
