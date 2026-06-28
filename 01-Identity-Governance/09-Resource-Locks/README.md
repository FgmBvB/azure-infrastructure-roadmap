# Azure Resource Locks

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Resource Locks, including lock types, inheritance, governance integration, and Microsoft's recommended practices for protecting critical Azure resources.

---

## Overview

Azure Resource Locks provide an additional layer of protection against accidental modification or deletion of Azure resources.

Unlike Azure RBAC, which determines **who** can perform actions, or Azure Policy, which defines **how** resources should be configured, Resource Locks protect deployed resources regardless of user permissions.

Resource Locks are a key component of Azure governance, helping organizations safeguard production environments from unintended changes.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Resource Locks.
- Differentiate **CanNotDelete** and **ReadOnly** locks.
- Understand scope inheritance.
- Explain how Resource Locks interact with Azure RBAC and Azure Policy.
- Apply Microsoft's best practices for protecting Azure resources.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Resource Lock architecture, lock types, scope inheritance, governance evaluation, and Azure RBAC integration. |
| **02 - Best Practices** | Lock strategy, governance recommendations, operational guidance, and common implementation pitfalls. |

---

## Architecture

```text
          Authentication
                 │
                 ▼
        Azure RBAC (Authorization)
                 │
                 ▼
      Azure Policy (Compliance)
                 │
                 ▼
        Resource Locks Check
                 │
                 ▼
      Resource Operation
```

---

## Skills Covered

This section includes:

- Azure Resource Locks
- CanNotDelete Lock
- ReadOnly Lock
- Scope Inheritance
- Governance Evaluation
- Azure RBAC Integration
- Azure Policy Integration
- Operational Protection
- Governance Best Practices

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure Resource Locks.
- Protect Azure resources from accidental deletion.
- Understand lock inheritance.
- Differentiate Azure RBAC, Azure Policy, and Resource Locks.
- Apply governance controls to Azure resources.

---

## Key Takeaways

- Azure Resource Locks protect existing Azure resources from accidental modification or deletion.
- **CanNotDelete** prevents deletion while allowing resource management.
- **ReadOnly** blocks both modifications and deletions.
- Locks inherit through the Azure resource hierarchy.
- Resource Locks complement Azure RBAC and Azure Policy as part of a layered Azure governance strategy.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Lock your Azure resources to protect your infrastructure](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource Lock concepts and implementation |
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager architecture |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy governance |
| [Microsoft Learn – Protect your Azure resources with resource locks](https://learn.microsoft.com/training/modules/protect-resource-manager-resources/) | Microsoft Learn module |
