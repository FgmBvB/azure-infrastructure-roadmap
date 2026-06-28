# Azure Policy Initiatives

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure Policy Initiatives, also known as Policy Set Definitions, and how they simplify governance by grouping multiple policies into a single compliance framework.

---

## Overview

An **Azure Policy Initiative** is a logical collection of multiple Policy Definitions managed as a single unit.

Instead of assigning many individual policies, administrators assign one Initiative that enforces a complete governance or compliance objective.

Initiatives simplify policy management, improve consistency, and provide consolidated compliance reporting.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Policy Initiatives.
- Differentiate Policy Definitions from Initiatives.
- Assign Initiatives at the appropriate scope.
- Configure Initiative parameters.
- Understand compliance aggregation.
- Apply Initiatives to enterprise governance.

---

## Initiative Architecture

```text
Policy Initiative
        │
        ▼
 Policy Definitions
 ┌──────┼─────────┐
 │      │         │
 ▼      ▼         ▼
Policy  Policy   Policy
  A       B        C
        │
        ▼
 Initiative Assignment
        │
        ▼
 Compliance Results
```

---

## Policy Definition vs Initiative

| Policy Definition | Policy Initiative |
|-------------------|------------------|
| Single governance rule | Collection of policies |
| One compliance objective | Multiple related objectives |
| Assigned individually | Assigned as one unit |
| Individual compliance result | Aggregated compliance report |

---

## Initiative Assignments

Like individual policies, Initiatives become active only after they are assigned.

Assignments define:

- Scope
- Parameters
- Exclusions
- Exemptions
- Enforcement mode

All included Policy Definitions are evaluated within the assigned scope.

---

## Initiative Parameters

An Initiative can expose parameters that are shared by multiple Policy Definitions.

Examples include:

- Allowed Azure regions
- Required resource tags
- Approved VM SKUs
- Naming standards

This reduces duplication and simplifies administration.

---

## Compliance Aggregation

Each Policy Definition produces its own compliance result.

Azure Policy combines these individual results into a consolidated Initiative compliance report.

Administrators can:

- View overall compliance.
- Identify failing policies.
- Drill down into non-compliant resources.
- Launch remediation tasks for supported policies.

---

## Built-in vs Custom Initiatives

Azure provides both built-in and custom Initiatives.

| Type | Description |
|------|-------------|
| **Built-in Initiative** | Provided and maintained by Microsoft. |
| **Custom Initiative** | Created by the organization to group policies according to internal governance requirements. |

Microsoft recommends using built-in Initiatives whenever they satisfy business requirements.

---

## Enterprise Scenario

A company wants to enforce corporate governance across all subscriptions.

Instead of assigning separate policies for allowed locations, mandatory tags, secure Storage Accounts, and diagnostic settings, administrators create a single Initiative.

The Initiative is assigned at the Management Group scope, providing centralized governance and a unified compliance dashboard for all subscriptions.

---

## Best Practices

- Use Initiatives instead of assigning many individual policies.
- Reuse built-in Initiatives whenever possible.
- Group related policies according to business objectives.
- Assign Initiatives at the highest appropriate scope.
- Use parameters to maximize reusability.
- Monitor Initiative compliance regularly.

---

## Common Pitfalls

- Assigning dozens of individual policies instead of an Initiative.
- Creating duplicate Initiatives.
- Mixing unrelated policies in the same Initiative.
- Ignoring compliance reports.
- Using custom Initiatives when built-in alternatives already exist.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Policy Initiatives
> - Policy Set Definitions
> - Initiative Assignments
> - Shared Parameters
> - Compliance aggregation
> - Built-in vs Custom Initiatives

---

## Key Takeaways

- A Policy Initiative is a collection of Policy Definitions managed as a single unit.
- Initiatives simplify Azure governance and improve consistency.
- Shared parameters reduce duplication.
- Compliance is aggregated across all included policies.
- Microsoft recommends using Initiatives to manage enterprise-scale governance.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Policy initiatives](https://learn.microsoft.com/azure/governance/policy/concepts/initiative-definition-structure) | Initiative definition structure |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy concepts |
| [Policy assignment structure](https://learn.microsoft.com/azure/governance/policy/concepts/assignment-structure) | Initiative assignments |
| [Azure Policy compliance](https://learn.microsoft.com/azure/governance/policy/how-to/get-compliance-data) | Compliance reporting |
| [Microsoft Learn – Configure Azure Policy](https://learn.microsoft.com/training/modules/configure-azure-policy/) | Microsoft Learn module |
