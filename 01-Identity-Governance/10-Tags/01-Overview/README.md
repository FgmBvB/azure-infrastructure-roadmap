# Azure Tags Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Tags, explains how they organize Azure resources, and describes their role in governance, cost management, automation, and compliance.

---

## Overview

Azure Tags are metadata in the form of **name-value pairs** that can be assigned to Azure resources and Resource Groups.

Tags help organizations organize resources, simplify administration, improve cost reporting, automate management tasks, and enforce governance standards across Azure environments.

Although tags do not affect the behavior or performance of Azure resources, they provide valuable contextual information used by administrators and Azure services.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Tags.
- Create and manage resource tags.
- Differentiate Resource Group and Resource tags.
- Understand tag inheritance limitations.
- Use tags for governance and cost management.
- Integrate Azure Tags with Azure Policy.

---

## Tag Structure

Every Azure Tag consists of two elements.

```text
Tag
 │
 ├── Name
 │
 └── Value
```

Example:

| Name | Value |
|------|-------|
| Environment | Production |
| Department | Finance |
| Owner | IT Team |
| CostCenter | CC-100 |

---

## Supported Resources

Most Azure resources support tags, including:

- Virtual Machines
- Storage Accounts
- Virtual Networks
- Resource Groups
- Managed Disks
- Network Security Groups

Some Azure resources do not support tags or have implementation limitations.

---

## Resource Groups vs Resources

Tags applied to a **Resource Group** are **not automatically inherited** by its resources.

If child resources require the same tags, administrators typically use **Azure Policy** with the **Modify** or **Append** effects to apply or inherit tags automatically.

---

## Tag Limits

Azure supports:

- Up to **50 tags** per resource or Resource Group.
- Each tag consists of a **Name** and a **Value**.
- Tag names are case-insensitive for operations, although the original casing is preserved for display.

---

## Common Uses

Azure Tags are commonly used for:

- Cost allocation
- Department ownership
- Environment identification
- Automation
- Resource organization
- Governance
- Reporting

---

## Azure Policy Integration

Azure Policy can enforce tagging standards.

Common scenarios include:

- Require mandatory tags.
- Add missing tags automatically.
- Inherit tags from Resource Groups.
- Audit resources missing required tags.

---

## Enterprise Scenario

A company requires every Azure resource to include the following tags:

- Environment
- Department
- CostCenter
- Owner

Azure Policy automatically adds missing tags where possible and reports resources that do not comply with the organization's tagging standards.

This allows Finance to allocate Azure costs accurately while simplifying operational management.

---

## Best Practices

- Define a standardized tagging strategy.
- Use consistent naming conventions.
- Keep tag values simple and meaningful.
- Use Azure Policy to enforce mandatory tags.
- Review tags regularly.
- Remove obsolete or unused tags.

---

## Common Pitfalls

- Assuming Resource Group tags are inherited automatically.
- Using inconsistent tag names.
- Creating duplicate tags with different naming conventions.
- Ignoring mandatory business tags.
- Using tags as a security mechanism.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Tags
> - Name-value pairs
> - Resource Group vs Resource tags
> - Tag inheritance limitations
> - Azure Policy integration
> - Cost management

---

## Key Takeaways

- Azure Tags are metadata used to organize Azure resources.
- Tags improve governance, reporting, automation, and cost management.
- Resource Group tags are not automatically inherited by child resources.
- Azure Policy can enforce and automatically apply tagging standards.
- A consistent tagging strategy simplifies Azure administration.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Use tags to organize your Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/tag-resources) | Azure Tags overview and management |
| [Azure Policy tag samples](https://learn.microsoft.com/azure/governance/policy/samples/built-in-policies#tags) | Built-in tag policies |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Policy enforcement for tags |
| [Cost Management + Billing](https://learn.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) | Using tags for cost allocation |
| [Microsoft Learn – Organize Azure resources by using tags](https://learn.microsoft.com/training/modules/organize-azure-resources-tags/) | Microsoft Learn module |
