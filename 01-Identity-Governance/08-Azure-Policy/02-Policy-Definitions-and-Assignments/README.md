# Policy Definitions and Assignments

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure Policy Definitions and Assignments work, including policy parameters, scopes, effects, exclusions, exemptions, and remediation tasks.

---

## Overview

Azure Policy enforces governance by evaluating resources against defined rules.

A policy becomes active only after it is **assigned** to a scope. During assignment, administrators can customize policy behavior using parameters, exclusions, and enforcement settings.

Understanding the relationship between Policy Definitions and Policy Assignments is essential for designing scalable governance solutions.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Policy Definitions.
- Create Policy Assignments.
- Configure policy parameters.
- Apply policies at different scopes.
- Understand policy effects.
- Configure exclusions and exemptions.
- Launch remediation tasks.

---

## Policy Workflow

```text
Policy Definition
        │
        ▼
Policy Assignment
        │
 ┌──────┼─────────┐
 │      │         │
 ▼      ▼         ▼
Scope Parameters Effect
        │
        ▼
 Policy Evaluation
        │
        ▼
Compliance Results
```

---

## Policy Definitions

A **Policy Definition** contains the rule that Azure Policy evaluates.

It specifies:

- Conditions to evaluate.
- Resource types.
- Policy effect.
- Parameters (optional).

Azure provides both **Built-in Policies** and **Custom Policies**.

---

## Policy Assignments

A **Policy Assignment** applies a Policy Definition to a specific scope.

Assignments determine:

- Where the policy applies.
- Parameter values.
- Excluded scopes.
- Enforcement mode.

A policy has no effect until it is assigned.

---

## Parameters

Parameters allow administrators to reuse the same Policy Definition in different environments.

Examples include:

- Allowed locations.
- Required resource tags.
- Approved SKU sizes.
- Allowed resource types.

Parameters improve flexibility without modifying the original policy definition.

---

## Assignment Scope

Policies can be assigned at multiple levels.

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

Assignments inherit automatically to child resources unless explicitly excluded or exempted.

---

## Policy Effects

Azure Policy supports several built-in effects.

| Effect | Description |
|---------|-------------|
| **Audit** | Reports non-compliant resources. |
| **Deny** | Blocks non-compliant deployments. |
| **Append** | Adds properties during deployment. |
| **Modify** | Updates resource properties during deployment or remediation. |
| **DeployIfNotExists** | Deploys missing dependent resources after deployment. |
| **AuditIfNotExists** | Audits when related resources are missing. |
| **Disabled** | Disables policy evaluation. |

---

## Exclusions and Exemptions

Azure Policy provides two ways to exclude resources from policy enforcement.

| Feature | Description |
|---------|-------------|
| **Exclusion** | Removes an entire scope from policy evaluation during assignment. |
| **Exemption** | Excludes specific resources while keeping the policy assignment active. Exemptions can include an expiration date and justification. |

Exclusions are commonly used for development or testing environments, while Exemptions are intended for approved governance exceptions.

---

## Enforcement Mode

Policy assignments support two enforcement modes.

| Mode | Behavior |
|------|----------|
| **Enabled** | The policy effect is enforced normally. |
| **DoNotEnforce** | The policy is evaluated for compliance but its effect is not enforced. |

**DoNotEnforce** is useful when testing new policies before applying enforcement in production.

---

## Remediation Tasks

Some policy effects support automatic remediation.

For example:

- Add missing tags.
- Enable diagnostic settings.
- Deploy monitoring agents.
- Configure supported resource settings.

Remediation tasks use a managed identity to perform corrective actions on existing non-compliant resources.

---

## Enterprise Scenario

An organization creates a policy requiring all Storage Accounts to use secure transfer.

The policy is assigned at the Subscription scope.

Production Resource Groups are evaluated normally, while a development Resource Group is excluded from the assignment.

Existing Storage Accounts that do not meet the policy requirements are corrected using a remediation task.

---

## Best Practices

- Reuse built-in policies whenever possible.
- Assign policies at the highest appropriate scope.
- Use parameters instead of creating duplicate policies.
- Test policies using **DoNotEnforce** before enabling enforcement.
- Use Exemptions instead of removing assignments when governance exceptions are required.
- Monitor compliance after every policy deployment.

---

## Common Pitfalls

- Creating policies without assigning them.
- Applying **Deny** policies without testing.
- Creating duplicate policies instead of using parameters.
- Confusing Exclusions with Exemptions.
- Forgetting to run remediation tasks for existing resources.
- Assigning policies at an unnecessarily broad scope.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Policy Definitions
> - Policy Assignments
> - Parameters
> - Policy Effects
> - Scope inheritance
> - Exclusions vs Exemptions
> - Enforcement Mode
> - Remediation Tasks

---

## Key Takeaways

- Policy Definitions describe governance rules.
- Policy Assignments activate policies by applying them to a scope.
- Parameters make policies reusable across environments.
- Exclusions and Exemptions serve different governance purposes.
- Remediation Tasks help bring existing resources into compliance.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Policy definition structure](https://learn.microsoft.com/azure/governance/policy/concepts/definition-structure) | Policy definition schema |
| [Azure Policy assignments](https://learn.microsoft.com/azure/governance/policy/concepts/assignment-structure) | Policy assignment configuration |
| [Azure Policy effects](https://learn.microsoft.com/azure/governance/policy/concepts/effect-basics) | Built-in policy effects |
| [Remediate non-compliant resources](https://learn.microsoft.com/azure/governance/policy/how-to/remediate-resources) | Remediation tasks |
| [Microsoft Learn – Configure Azure Policy](https://learn.microsoft.com/training/modules/configure-azure-policy/) | Microsoft Learn module |
