# Azure Policy

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Policy, including policy definitions, assignments, initiatives, compliance evaluation, remediation, and Microsoft's recommended governance practices.

---

## Overview

Azure Policy is Azure's governance service for enforcing organizational standards and ensuring Azure resources remain compliant with business, security, and regulatory requirements.

Unlike Azure RBAC, which determines **who** can perform actions, Azure Policy determines **how** Azure resources should be configured and whether they comply with organizational rules.

Azure Policy enables organizations to automate governance, improve consistency, and maintain compliance across subscriptions and management groups.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Policy architecture.
- Create and assign Policy Definitions.
- Configure Policy Assignments.
- Understand Policy Effects.
- Use Policy Initiatives.
- Monitor compliance.
- Perform remediation.
- Apply Azure Policy best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure Policy architecture, governance concepts, evaluation process, compliance, and Policy Effects. |
| **02 - Policy Definitions and Assignments** | Policy Definitions, Assignments, Parameters, Effects, Exclusions, Exemptions, Enforcement Mode, and Remediation Tasks. |
| **03 - Initiatives** | Policy Initiatives (Policy Set Definitions), shared parameters, compliance aggregation, and enterprise governance. |
| **04 - Best Practices** | Governance recommendations, compliance management, remediation, and operational best practices. |

---

## Architecture

```text
           Azure Resource Manager
                    │
                    ▼
              Azure Policy
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
 Policy      Policy Assignment  Initiative
Definition
        │
        ▼
 Policy Evaluation
        │
        ▼
 Compliance Results
        │
        ▼
 Remediation (if supported)
```

---

## Skills Covered

This section includes:

- Azure Policy
- Policy Definitions
- Policy Assignments
- Policy Parameters
- Policy Effects
- Scope Inheritance
- Exclusions
- Exemptions
- Enforcement Mode
- Remediation Tasks
- Policy Initiatives
- Compliance Monitoring
- Governance

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure Policy.
- Create and assign Policy Definitions.
- Configure Policy Initiatives.
- Apply governance across Azure resources.
- Monitor compliance.
- Perform remediation.
- Implement organizational standards.

---

## Key Takeaways

- Azure Policy enforces governance and compliance across Azure resources.
- Policy Definitions define governance rules, while Policy Assignments apply them to Azure scopes.
- Policy Initiatives simplify governance by grouping related policies.
- Compliance is evaluated continuously throughout the resource lifecycle.
- Azure Policy and Azure RBAC complement each other to provide secure and well-governed Azure environments.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy concepts and architecture |
| [Azure Policy definition structure](https://learn.microsoft.com/azure/governance/policy/concepts/definition-structure) | Policy definition schema |
| [Azure Policy initiatives](https://learn.microsoft.com/azure/governance/policy/concepts/initiative-definition-structure) | Initiative definitions |
| [Azure Policy effects](https://learn.microsoft.com/azure/governance/policy/concepts/effect-basics) | Built-in policy effects |
| [Microsoft Learn – Configure Azure Policy](https://learn.microsoft.com/training/modules/configure-azure-policy/) | Microsoft Learn module |
