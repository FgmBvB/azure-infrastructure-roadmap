# Azure Policy Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Policy, explains how policy evaluation works, and describes its role in Azure governance and compliance.

---

## Overview

Azure Policy is Azure's governance service for enforcing organizational standards and assessing compliance across Azure resources.

Unlike Azure RBAC, which controls **who** can perform actions, Azure Policy controls **how** Azure resources should be configured and whether they comply with organizational requirements.

Azure Policy helps organizations maintain consistent, secure, and compliant environments at scale.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Policy architecture.
- Differentiate Azure Policy from Azure RBAC.
- Understand the policy evaluation process.
- Identify policy scopes.
- Understand policy effects.
- Monitor compliance across Azure resources.

---

## Azure Policy Architecture

```text
Azure Resource Manager (ARM)
            │
            ▼
      Azure Policy
            │
    Policy Evaluation
            │
            ▼
   Compliance Assessment
            │
     ┌──────┴──────┐
     │             │
     ▼             ▼
 Compliant   Non-Compliant
```

---

## Azure Policy vs Azure RBAC

Although both services are part of Azure governance, they solve different problems.

| Azure Policy | Azure RBAC |
|---------------|------------|
| Evaluates resource compliance | Controls authorization |
| Governs resource configuration | Governs user permissions |
| Applies organizational standards | Grants administrative access |
| Prevents or audits non-compliant resources | Controls who can manage resources |

Azure RBAC answers **Who can perform an action?**

Azure Policy answers **Should this resource comply with organizational standards?**

---

## Policy Components

Every Azure Policy implementation consists of several components.

| Component | Purpose |
|-----------|---------|
| **Policy Definition** | Defines the rule to evaluate. |
| **Assignment** | Applies the policy to a specific scope. |
| **Parameters** | Customize policy behavior. |
| **Policy Effect** | Defines the action taken when the policy evaluates a resource. |

---

## Scope Hierarchy

Azure Policy can be assigned at different scopes.

```text
Management Group
        │
        ▼
 Subscription
        │
        ▼
 Resource Group
        │
        ▼
    Resource
```

Policies assigned at higher scopes are inherited by child resources unless excluded or exempted.

---

## Policy Evaluation

Azure Policy evaluates resources during several events:

- Resource creation.
- Resource updates.
- Periodic compliance scans.
- Manual compliance evaluation.

Resources are marked as either **Compliant** or **Non-compliant** based on the assigned policies.

---

### Resource Manager Evaluation

During resource deployment, Azure Resource Manager evaluates several governance services before completing the operation.

A simplified evaluation sequence is:

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
Resource Deployment
```

In general:

- Azure RBAC verifies whether the identity is authorized to perform the requested operation.
- Azure Policy evaluates whether the resource configuration complies with organizational standards.
- Resource Locks protect existing resources from accidental modification or deletion.

If a policy with the **Deny** effect applies, Azure Resource Manager stops the deployment before the resource is created.

---

## Policy Effects

Azure Policy supports multiple effects.

Common effects include:

- Audit
- Deny
- Append
- Modify
- DeployIfNotExists
- AuditIfNotExists
- Disabled

Each effect determines how Azure responds when a resource does not satisfy the policy rule.

---

## Exclusions and Exemptions

Azure Policy provides two mechanisms for excluding resources from policy enforcement.

| Feature | Description |
|---------|-------------|
| **Exclusion** | Excludes a scope from a policy assignment so resources within that scope are not evaluated. |
| **Exemption** | Excludes specific resources from compliance while keeping the policy assignment in place. Exemptions can optionally include an expiration date and justification. |

Exclusions are configured during policy assignment, whereas Exemptions are intended for approved governance exceptions without removing the policy itself.

---

## Compliance

Azure Policy continuously tracks compliance across assigned scopes.

Administrators can:

- View compliance reports.
- Identify non-compliant resources.
- Investigate policy violations.
- Launch remediation tasks for supported policies.

Compliance results are available in the Azure portal and can also be queried programmatically.

---

## Policy Initiatives

A **Policy Initiative** (also called a **Policy Set Definition**) is a collection of multiple Policy Definitions managed as a single unit.

Instead of assigning many individual policies, administrators can assign one Initiative that represents a common governance objective.

Benefits include:

- Simplified policy management.
- Centralized compliance reporting.
- Consistent governance across subscriptions.
- Easier implementation of regulatory standards.

Policy Initiatives are covered in detail in the next section of this roadmap.

---

## Enterprise Scenario

A company requires all Storage Accounts to use secure transfer and all Virtual Machines to include mandatory resource tags.

Azure Policy evaluates every deployment and prevents non-compliant resources from being created while continuously monitoring existing resources for compliance.

---

## Best Practices

- Assign policies at the highest appropriate scope.
- Start with **Audit** before using **Deny**.
- Reuse built-in policies whenever possible.
- Use Initiatives to organize related policies.
- Review compliance regularly.
- Use remediation tasks to correct non-compliant resources.

---

## Common Pitfalls

- Applying Deny policies without prior testing.
- Assigning policies at an unnecessarily broad scope.
- Ignoring compliance reports.
- Creating duplicate custom policies.
- Confusing Azure Policy with Azure RBAC.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Policy architecture
> - Policy evaluation
> - Scope hierarchy
> - Policy effects
> - Compliance assessment
> - Azure Policy vs Azure RBAC

---

## Key Takeaways

- Azure Policy enforces organizational standards across Azure resources.
- Azure Policy governs resource compliance, while Azure RBAC governs authorization.
- Policies are evaluated automatically throughout the resource lifecycle.
- Policy effects determine how Azure responds to non-compliant resources.
- Compliance reporting helps organizations maintain secure and consistent Azure environments.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy concepts and architecture |
| [Azure Policy definition structure](https://learn.microsoft.com/azure/governance/policy/concepts/definition-structure) | Policy definition components |
| [Azure Policy effects](https://learn.microsoft.com/azure/governance/policy/concepts/effect-basics) | Built-in policy effects |
| [Azure Policy compliance](https://learn.microsoft.com/azure/governance/policy/how-to/get-compliance-data) | Compliance evaluation and reporting |
| [Microsoft Learn – Configure Azure Policy](https://learn.microsoft.com/training/modules/configure-azure-policy/) | Microsoft Learn module |
