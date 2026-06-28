# Azure Policy Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for designing, deploying, and maintaining Azure Policy in enterprise environments.

---

## Overview

Azure Policy helps organizations enforce governance, maintain compliance, and standardize Azure resource configurations.

A successful Azure Policy implementation balances security, operational flexibility, and automation while minimizing the impact on production workloads.

---

## Governance Lifecycle

```text
Define Standards
        │
        ▼
Create Policies
        │
        ▼
Group into Initiatives
        │
        ▼
Assign Policies
        │
        ▼
Monitor Compliance
        │
        ▼
Remediate Resources
        │
        ▼
Review & Improve
```

---

> [!TIP]
> **Key Concepts**
>
> - Prefer built-in policies.
> - Start with **Audit** before using **Deny**.
> - Use Initiatives to simplify governance.
> - Assign policies at the highest appropriate scope.
> - Review compliance regularly.

---

## Policy Design

Microsoft recommends:

- Use built-in Policy Definitions whenever possible.
- Create Custom Policies only when necessary.
- Reuse parameters instead of duplicating policies.
- Keep Policy Definitions simple and easy to maintain.
- Group related policies into Initiatives.

---

## Policy Deployment

To minimize operational risk:

- Test new policies in non-production environments.
- Use **DoNotEnforce** or **Audit** before enabling **Deny**.
- Assign policies at the highest appropriate scope.
- Use Exclusions only when required.
- Use Exemptions for approved governance exceptions.

---

## Compliance Management

Maintain compliance by:

- Reviewing compliance reports regularly.
- Investigating non-compliant resources promptly.
- Running remediation tasks when supported.
- Monitoring policy evaluation results after deployments.
- Triggering manual compliance scans after significant policy changes when immediate validation is required.

---

## Security

Strengthen governance by:

- Combining Azure Policy with Azure RBAC.
- Protecting critical resources with Resource Locks.
- Using Managed Identities for remediation tasks.
- Applying least privilege to remediation identities.
- Monitoring Activity Logs and Policy compliance reports.

---

## Governance

Good governance includes:

- Standardized naming conventions.
- Mandatory resource tags.
- Approved deployment locations.
- Consistent resource configuration.
- Regular policy reviews.
- Documentation of governance standards.

---

## Enterprise Scenario

An organization deploys a governance Initiative that requires approved Azure regions, mandatory resource tags, secure Storage Account settings, and diagnostic logging.

The Initiative is first deployed in **Audit** mode to evaluate existing resources.

After reviewing compliance and remediating non-compliant resources, the organization enables **Deny** for future deployments.

---

## Best Practices Checklist

- Prefer built-in policies.
- Group related policies into Initiatives.
- Test policies before enforcement.
- Start with Audit or DoNotEnforce.
- Use parameters for flexibility.
- Assign policies at the highest appropriate scope.
- Monitor compliance regularly.
- Run remediation tasks when supported.
- Protect remediation identities with least privilege.
- Review governance standards periodically.

---

## Common Pitfalls

- Applying Deny policies without testing.
- Creating duplicate custom policies.
- Ignoring compliance reports.
- Assigning policies at an unnecessarily broad scope.
- Confusing Exclusions with Exemptions.
- Forgetting RBAC permissions for remediation identities.
- Neglecting periodic governance reviews.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Policy governance
> - Audit vs Deny
> - Initiatives
> - Compliance monitoring
> - Remediation
> - Exclusions vs Exemptions
> - Least privilege for remediation identities

---

## Key Takeaways

- Azure Policy enforces organizational governance across Azure resources.
- Built-in policies and Initiatives simplify large-scale management.
- Audit and DoNotEnforce help validate policies before enforcement.
- Compliance should be monitored continuously and supported with remediation when appropriate.
- Combining Azure Policy with Azure RBAC provides strong governance and secure resource administration.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy concepts |
| [Azure Policy definition structure](https://learn.microsoft.com/azure/governance/policy/concepts/definition-structure) | Policy design |
| [Azure Policy initiatives](https://learn.microsoft.com/azure/governance/policy/concepts/initiative-definition-structure) | Policy initiatives |
| [Remediate non-compliant resources](https://learn.microsoft.com/azure/governance/policy/how-to/remediate-resources) | Remediation tasks |
| [Microsoft Learn – Configure Azure Policy](https://learn.microsoft.com/training/modules/configure-azure-policy/) | Microsoft Learn module |
