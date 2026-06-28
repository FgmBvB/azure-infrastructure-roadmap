# Azure Resource Locks Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for implementing Azure Resource Locks to protect critical Azure resources from accidental modification or deletion.

---

## Overview

Resource Locks provide an additional layer of protection for Azure resources by preventing accidental changes, regardless of Azure RBAC permissions.

Microsoft recommends using Resource Locks as part of a broader governance strategy together with Azure RBAC, Azure Policy, and proper operational procedures.

---

## Protection Lifecycle

```text
Identify Critical Resources
          │
          ▼
Select Lock Type
          │
          ▼
Apply Lock
          │
          ▼
Monitor Operations
          │
          ▼
Review Periodically
          │
          ▼
Remove Only When Required
```

---

> [!TIP]
> **Key Concepts**
>
> - Protect only critical resources.
> - Prefer **CanNotDelete** over **ReadOnly** when possible.
> - Apply locks at the lowest practical scope.
> - Combine Resource Locks with Azure RBAC and Azure Policy.
> - Review locks regularly.

---

## Choosing the Correct Lock

Microsoft recommends selecting the least restrictive lock that satisfies the business requirement.

| Requirement | Recommended Lock |
|------------|------------------|
| Prevent accidental deletion | **CanNotDelete** |
| Prevent all configuration changes | **ReadOnly** |

Whenever possible, use **CanNotDelete**, as it protects resources while still allowing administrators to perform maintenance.

---

## Scope Selection

When applying Resource Locks:

- Lock individual resources only when necessary.
- Use Resource Group locks to protect related resources.
- Apply Subscription-level locks only for exceptional governance scenarios.
- Always consider inherited locks before creating additional locks.

---

## Operational Recommendations

To reduce operational risk:

- Document every Resource Lock.
- Verify inherited locks before troubleshooting deployment failures.
- Remove temporary locks after maintenance activities.
- Review locks periodically to ensure they remain necessary.
- Test administrative procedures before applying **ReadOnly** locks in production.

---

## Security

Resource Locks should complement—not replace—other Azure security controls.

Microsoft recommends combining Resource Locks with:

- Azure RBAC for authorization.
- Azure Policy for governance and compliance.
- Multi-Factor Authentication (MFA) for privileged accounts.
- Microsoft Entra Privileged Identity Management (PIM) where available.

Together, these services provide layered protection for Azure resources.

---

## Governance

A mature governance strategy should include:

- Standardized lock naming conventions.
- Documentation of business justification.
- Regular governance reviews.
- Monitoring Activity Logs for lock changes.
- Approval procedures before removing production locks.

---

## Enterprise Scenario

A company protects all production Resource Groups with **CanNotDelete** locks.

Critical networking resources receive temporary **ReadOnly** locks during infrastructure migration to prevent configuration changes.

Azure RBAC controls administrative permissions, Azure Policy enforces deployment standards, and Resource Locks protect the deployed infrastructure from accidental modification or deletion.

---

## Best Practices Checklist

- Protect only critical resources.
- Prefer **CanNotDelete** when appropriate.
- Apply locks at the lowest practical scope.
- Review inherited locks before troubleshooting.
- Combine Resource Locks with Azure RBAC and Azure Policy.
- Document lock purpose and ownership.
- Monitor Activity Logs.
- Remove temporary locks after maintenance.
- Review production locks regularly.

---

## Common Pitfalls

- Applying **ReadOnly** unnecessarily.
- Forgetting inherited locks.
- Assuming Azure RBAC overrides Resource Locks.
- Applying locks at an unnecessarily broad scope.
- Leaving temporary locks in place after maintenance.
- Not documenting why locks were created.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - CanNotDelete vs ReadOnly
> - Scope inheritance
> - Resource Lock strategy
> - Azure RBAC vs Resource Locks
> - Azure Policy integration
> - Governance best practices

---

## Key Takeaways

- Resource Locks protect Azure resources from accidental changes.
- **CanNotDelete** is generally preferred because it allows normal administration while preventing accidental deletion.
- Locks inherit through the Azure resource hierarchy.
- Resource Locks should be combined with Azure RBAC and Azure Policy as part of a layered governance strategy.
- Regular reviews help ensure locks remain appropriate as environments evolve.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Lock your Azure resources to protect your infrastructure](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource Lock implementation and management |
| [Azure Resource Manager overview](https://learn.microsoft.com/azure/azure-resource-manager/management/overview) | Azure Resource Manager governance |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy governance |
| [Microsoft Learn – Protect your Azure resources with resource locks](https://learn.microsoft.com/training/modules/protect-resource-manager-resources/) | Microsoft Learn module |
