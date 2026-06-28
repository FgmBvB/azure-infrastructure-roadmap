# Azure Tags

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Tags, including tag structure, governance, Azure Policy integration, cost management, automation, and Microsoft's recommended tagging practices.

---

## Overview

Azure Tags are **name-value pairs** that provide metadata for Azure resources and Resource Groups.

Tags help organizations organize resources, improve governance, automate management tasks, and allocate Azure costs accurately across departments, projects, and environments.

Although tags do not modify the behavior of Azure resources, they play a critical role in enterprise governance and operational management.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Tags.
- Create and manage resource tags.
- Differentiate Resource Group and Resource tags.
- Understand tag inheritance limitations.
- Use Azure Policy to enforce tagging standards.
- Improve governance and Cost Management using tags.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure Tags architecture, tag structure, supported resources, inheritance limitations, Azure Policy integration, and common use cases. |
| **02 - Best Practices** | Tagging strategies, governance recommendations, Cost Management, automation, Azure Policy enforcement, and common implementation pitfalls. |

---

## Architecture

```text
        Azure Resources
               │
               ▼
          Azure Tags
       (Name-Value Pairs)
               │
     ┌─────────┼─────────┐
     │         │         │
     ▼         ▼         ▼
Governance  Cost Mgmt  Automation
               │
               ▼
        Azure Policy
         (Enforcement)
```

---

## Skills Covered

This section includes:

- Azure Tags
- Name-Value Pairs
- Resource Organization
- Cost Management
- Governance
- Azure Policy Integration
- Automation
- Tag Inheritance
- Mandatory Tags
- Tagging Strategy

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure Tags.
- Organize Azure resources.
- Implement governance standards.
- Use Azure Policy to enforce tagging.
- Support Cost Management reporting.
- Apply tagging best practices.

---

## Key Takeaways

- Azure Tags provide metadata that improves resource organization and governance.
- Tags support Cost Management, automation, reporting, and operational visibility.
- Resource Group tags are **not automatically inherited** by child resources.
- Azure Policy can enforce, append, or inherit tags automatically.
- A standardized tagging strategy simplifies Azure administration and improves governance.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Use tags to organize your Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/tag-resources) | Azure Tags concepts and management |
| [Azure Policy tag samples](https://learn.microsoft.com/azure/governance/policy/samples/built-in-policies#tags) | Built-in policies for tag enforcement |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure Policy governance |
| [Cost Management best practices](https://learn.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) | Using tags for cost allocation |
| [Microsoft Learn – Organize Azure resources by using tags](https://learn.microsoft.com/training/modules/organize-azure-resources-tags/) | Microsoft Learn module |
