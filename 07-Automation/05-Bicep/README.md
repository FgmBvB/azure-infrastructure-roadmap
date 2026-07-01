# Bicep

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers **Bicep**, Microsoft's modern Infrastructure as Code (IaC) language for Azure. Bicep simplifies ARM Template authoring while using Azure Resource Manager (ARM) as the underlying deployment engine.

---

# Overview

Bicep is Microsoft's recommended Infrastructure as Code language for deploying Azure resources.

Rather than writing complex ARM Templates in JSON, administrators can author infrastructure using a concise, strongly typed, and highly readable syntax that is automatically transpiled into ARM Templates before deployment.

Bicep combines simplicity with the full capabilities of Azure Resource Manager, making it the preferred choice for modern Azure infrastructure deployments.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Bicep architecture.
- Understand the Bicep deployment workflow.
- Understand Bicep transpilation.
- Create reusable Infrastructure as Code.
- Use parameters and variables.
- Deploy Azure resources.
- Reference existing resources.
- Understand modules.
- Understand implicit dependencies.
- Compare Bicep with ARM Templates.
- Apply Microsoft's Bicep best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Bicep architecture, Infrastructure as Code, transpilation, template structure, parameters, variables, resources, modules, existing resources, implicit dependencies, deployment workflow, and AZ-104 concepts. |
| **02 - Best Practices** | Modular design, parameter management, Key Vault integration, deployment validation, What-If analysis, source control, naming conventions, reusable modules, production recommendations, and Microsoft's best practices. |

---

# Bicep Architecture

```text
Administrator

↓

Bicep (.bicep)

↓

Bicep Compiler

↓

ARM Template (JSON)

↓

Azure Resource Manager (ARM)

↓

Resource Providers

↓

Azure Resources
```

Although administrators work with Bicep files, Azure Resource Manager always receives and deploys the compiled ARM Template.

---

# Core Capabilities

This section covers the primary Bicep capabilities.

## Infrastructure as Code

- Declarative deployments
- Repeatable infrastructure
- Version-controlled templates
- Reduced configuration drift
- Environment consistency

---

## Modern Authoring

- Clean syntax
- Strong typing
- IntelliSense
- Symbolic resource references
- Built-in validation

---

## Modular Design

- Reusable modules
- Shared infrastructure
- Environment separation
- Parameter files
- Existing resource references

---

## Deployment Integration

- Azure CLI
- Azure PowerShell
- Azure Portal
- Azure Cloud Shell
- Azure DevOps
- GitHub Actions

---

# Typical Workflow

```text
Write Bicep

↓

Validate

↓

Compile

↓

Deploy

↓

Azure Resource Manager

↓

Azure Resources
```

Azure CLI and Azure PowerShell perform the compilation automatically during deployment.

---

# Design Principles

Microsoft recommends following these principles:

- Prefer Bicep over ARM JSON for new deployments.
- Design reusable modules.
- Separate templates from parameter files.
- Use parameters instead of hardcoded values.
- Protect secrets with Azure Key Vault.
- Reference existing resources when appropriate.
- Use symbolic references instead of explicit dependencies.
- Validate deployments before execution.
- Store Infrastructure as Code in source control.
- Design idempotent deployments.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Bicep
- Infrastructure as Code
- ARM Templates
- Bicep compilation
- Parameters
- Variables
- Modules
- Existing resources
- Implicit dependencies
- Deployment workflow

---

# Key Takeaways

- Bicep is Microsoft's recommended Infrastructure as Code language for Azure and provides a simpler, more maintainable alternative to ARM Templates.
- Bicep code is automatically transpiled into ARM Templates, which are deployed through Azure Resource Manager.
- Features such as modules, strong typing, IntelliSense, implicit dependencies, and existing resource references simplify Azure infrastructure deployments.
- Bicep integrates seamlessly with Azure CLI, Azure PowerShell, Azure DevOps, GitHub Actions, and Azure Cloud Shell for automated deployments.
- Understanding Bicep, its relationship with ARM, and modern Infrastructure as Code practices is an important objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Bicep documentation | https://learn.microsoft.com/azure/azure-resource-manager/bicep/ |
| Bicep file structure | https://learn.microsoft.com/azure/azure-resource-manager/bicep/file |
| Bicep modules | https://learn.microsoft.com/azure/azure-resource-manager/bicep/modules |
| Deploy Bicep files | https://learn.microsoft.com/azure/azure-resource-manager/bicep/deploy-cli |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Build reusable Bicep templates | https://learn.microsoft.com/training/modules/build-reusable-bicep-templates-parameters/ |
