# Azure Resource Locks Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Resource Locks, explains how they protect Azure resources from accidental changes, and describes their role within Azure governance.

---

## Overview

Azure Resource Locks protect Azure resources from accidental modification or deletion.

Unlike Azure RBAC, which controls **who** can perform actions, or Azure Policy, which governs **how** resources should be configured, Resource Locks protect existing resources regardless of the user's permissions.

Resource Locks provide an additional layer of protection for critical Azure infrastructure.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Resource Locks.
- Differentiate the available lock types.
- Understand scope inheritance.
- Explain how Resource Locks interact with Azure RBAC and Azure Policy.
- Apply Resource Locks to protect critical resources.

---

## Governance Evaluation

Azure Resource Manager evaluates several governance mechanisms during resource operations.

```text
Authentication
      │
      ▼
Azure RBAC
(Authorization)
      │
      ▼
Azure Policy
(Compliance)
      │
      ▼
Resource Locks
      │
      ▼
Resource Operation
```

Resource Locks are evaluated after authorization and policy evaluation but before the requested operation is completed.

---

## Lock Types

Azure supports two lock types.

| Lock | Description |
|------|-------------|
| **CanNotDelete** | Prevents resource deletion while allowing modifications. |
| **ReadOnly** | Prevents modifications and deletions. Only read operations are allowed. |

Both lock types apply regardless of the user's Azure RBAC permissions.

---

## Scope Hierarchy

Resource Locks can be applied at different Azure scopes.

```text
Subscription
      │
      ▼
Resource Group
      │
      ▼
Resource
```

Locks assigned at a higher scope are inherited automatically by child resources.

---

## Lock Inheritance

If a lock is applied to a Resource Group:

- Existing resources inherit the lock.
- Newly created resources inherit the lock.
- Individual resources cannot remove or override the inherited lock.

To remove protection, the inherited lock must first be removed from the parent scope.

---

## Resource Locks and Azure RBAC

Azure RBAC and Resource Locks provide different types of protection.

| Azure RBAC | Resource Locks |
|------------|----------------|
| Controls who can perform operations. | Protects resources from accidental changes. |
| Permissions are assigned through roles. | Protection applies regardless of assigned roles. |
| Authorization mechanism. | Resource protection mechanism. |

A user with the **Owner** role can still be prevented from deleting a resource if a Resource Lock applies.

---

## Enterprise Scenario

An organization protects its Production Resource Group with a **CanNotDelete** lock.

Infrastructure administrators continue updating Virtual Machines and networking resources, but accidental deletion of the Resource Group or any child resources is prevented until the lock is removed.

Critical networking components receive **ReadOnly** locks during migration projects to prevent configuration changes.

---

## Best Practices

- Apply locks only to critical resources.
- Prefer Resource Group locks for related resources.
- Use **CanNotDelete** for production workloads.
- Use **ReadOnly** only when configuration changes must be completely prevented.
- Combine Resource Locks with Azure RBAC and Azure Policy.
- Review locks periodically.

---

## Common Pitfalls

- Forgetting inherited locks.
- Applying **ReadOnly** to resources that require frequent updates.
- Assuming Azure RBAC overrides Resource Locks.
- Applying locks too broadly.
- Forgetting to remove temporary locks after maintenance.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Resource Lock types
> - CanNotDelete vs ReadOnly
> - Scope inheritance
> - Azure RBAC vs Resource Locks
> - Governance evaluation order

---

## Key Takeaways

- Resource Locks protect Azure resources from accidental modification and deletion.
- Azure supports **CanNotDelete** and **ReadOnly** locks.
- Locks inherit from parent scopes to child resources.
- Resource Locks complement Azure RBAC and Azure Policy as part of Azure governance.
- Applying Resource Locks to critical resources improves operational security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Lock your Azure resources to protect your infrastructure](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource Lock concepts and management |
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager architecture |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy governance |
| [Microsoft Learn – Protect your Azure resources with resource locks](https://learn.microsoft.com/training/modules/protect-resource-manager-resources/) | Microsoft Learn module |
