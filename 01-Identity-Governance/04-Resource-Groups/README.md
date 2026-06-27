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
> - Moving resources between Resource Groups or subscriptions has important governance and dependency implications.

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

Resource Groups are managed through Azure Resource Manager (ARM), which provides the management layer used to deploy, update, organize, and control Azure resources.

Resource Groups work together with Azure RBAC, Azure Policy, Resource Locks, and Tags to provide governance and resource management.

---

## Resource Movement

Azure resources can be moved between Resource Groups or between subscriptions, but not every resource type supports move operations.

Before moving resources, administrators should validate whether the resource type supports movement and check any dependencies.

During a move operation, both the source and destination Resource Groups are temporarily locked for write and delete operations.

Moving a resource can affect automation, scripts, monitoring, dependencies, RBAC inheritance, and governance because the resource is now managed under a different Resource Group or subscription scope.

---

## Resource Locks

Resource Locks can be applied at the subscription, Resource Group, or resource scope to help prevent accidental deletion or modification.

When a lock is applied at the Resource Group level, resources inside that Resource Group inherit the lock.

There are two main lock types:

- **CanNotDelete**: authorized users can read and modify resources, but they cannot delete them.
- **ReadOnly**: authorized users can read resources, but they cannot update or delete them.

Resource Locks override user permissions, so even users with high privileges can be blocked from deleting or modifying locked resources.

---

## ARM and Bicep Deployments

Resource Groups are commonly used as deployment scopes for ARM templates and Bicep files.

Azure Resource Manager supports different deployment modes:

- **Incremental mode**: adds or updates resources without deleting resources that are not included in the template.
- **Complete mode**: deletes resources in the Resource Group that are not defined in the template.

Complete mode must be used carefully because it can remove resources unintentionally if the template does not include the full desired state.

For most scenarios, incremental deployments are safer and more commonly used.

---

## Limits and Quotas

Azure applies limits and quotas to resources, deployments, subscriptions, and Resource Groups.

These limits can affect large environments and should be reviewed during architecture planning.

Because Azure limits can change over time and may vary by service, administrators should always verify the current limits in the official Microsoft documentation.

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
- Organizing Resource Groups only by resource type instead of workload or lifecycle.
- Ignoring naming conventions.
- Applying excessive permissions.
- Forgetting to use Tags and Resource Locks.
- Deleting a Resource Group without understanding that all contained resources are also deleted.
- Moving resources without checking dependencies and supported resource types.
- Using complete deployment mode without understanding its deletion behavior.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Resource Groups
> - Resource organization
> - Resource lifecycle
> - Azure Resource Manager
> - Moving resources between Resource Groups or subscriptions
> - RBAC inheritance at Resource Group scope
> - Azure Policy integration
> - Resource Locks
> - Tags
> - ARM and Bicep deployment behavior
> - Limits and quotas

---

## Key Takeaways

- Every Azure resource belongs to one Resource Group.
- Resource Groups belong to a single Azure Subscription.
- Resource Groups are logical management containers, not physical locations.
- Governance features such as RBAC, Policy, Locks, and Tags integrate with Resource Groups.
- Resource movement requires validation and can affect permissions, dependencies, and automation.
- Resource Locks help protect critical resources from accidental deletion or modification.
- ARM and Bicep deployments commonly target Resource Groups.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager and Resource Groups |
| [Manage Azure Resource Groups](https://learn.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal) | Resource Group management |
| [Move resources to a new Resource Group or subscription](https://learn.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription) | Resource movement behavior and restrictions |
| [Lock your Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource Locks |
| [Azure Resource Manager deployment modes](https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes) | Incremental and complete deployment modes |
| [Azure subscription and service limits](https://learn.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) | Azure limits, quotas, and constraints |
| [Azure naming rules and restrictions](https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules) | Naming conventions |
