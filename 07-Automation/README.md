# Automation

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers the tools and techniques used to automate Azure administration, including Azure CLI, Azure PowerShell, Azure Cloud Shell, Azure Resource Manager (ARM), ARM Templates, and Bicep. Automation is a fundamental skill for deploying, managing, and governing Azure resources consistently at scale.

---

# Overview

Automation is one of the core pillars of Azure administration.

Rather than manually configuring resources through the Azure Portal, administrators automate deployments and operational tasks using command-line tools, Infrastructure as Code (IaC), and scripting.

Automation increases consistency, reduces human error, accelerates deployments, improves governance, and enables repeatable infrastructure across multiple environments.

This module introduces Microsoft's automation ecosystem and the recommended practices for building secure, maintainable, and enterprise-ready automation workflows.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure automation tools.
- Manage Azure using Azure CLI.
- Manage Azure using Azure PowerShell.
- Use Azure Cloud Shell.
- Understand Azure Resource Manager (ARM).
- Deploy Infrastructure as Code using ARM Templates.
- Understand Bicep architecture and deployment workflow.
- Apply Infrastructure as Code principles.
- Automate Azure resource management.
- Apply Microsoft's automation best practices.

---

# Section Structure

| Section | Description |
|---------|-------------|
| **01 - Azure CLI** | Azure CLI fundamentals, command structure, JMESPath queries, scripting, automation workflows, and production best practices. |
| **02 - Azure PowerShell** | Azure PowerShell cmdlets, object-based automation, pipelines, jobs, scripting, and production best practices. |
| **03 - Azure Cloud Shell** | Browser-based administration, persistent storage, Azure Files integration, session lifecycle, and operational best practices. |
| **04 - Azure Resource Manager** | Azure Resource Manager architecture, ARM Templates, deployment modes, Infrastructure as Code, validation, template functions, and ARM deployment best practices. |
| **05 - Bicep** | Microsoft's modern Infrastructure as Code language, transpilation, modules, symbolic references, existing resources, deployment workflow, and Bicep best practices. |
| **06 - Best Practices** | Cross-platform automation guidance covering Azure CLI, PowerShell, Cloud Shell, ARM, Bicep, Infrastructure as Code, governance, security, and enterprise deployment recommendations. |

---

# Azure Automation Ecosystem

```text
Administrator

↓

Azure CLI
Azure PowerShell
Azure Cloud Shell

↓

Bicep
ARM Templates

↓

Azure Resource Manager (ARM)

↓

Resource Providers

↓

Azure Resources
```

Regardless of the tool used, all deployments ultimately pass through **Azure Resource Manager (ARM)** before being processed by the appropriate Azure Resource Provider.

---

# Core Technologies

## Azure CLI

Cross-platform command-line interface for Azure administration.

Typical use cases:

- Resource management
- Bash automation
- CI/CD pipelines
- Linux administration

---

## Azure PowerShell

PowerShell module for Azure administration.

Typical use cases:

- Object-oriented scripting
- Windows administration
- Complex automation
- Enterprise scripting

---

## Azure Cloud Shell

Browser-based administration environment with Azure CLI and Azure PowerShell preinstalled.

Benefits include:

- No local installation
- Automatic authentication
- Persistent Azure Files storage
- Access from any browser

---

## Azure Resource Manager (ARM)

Azure Resource Manager is Azure's deployment and management service.

Responsibilities include:

- Authentication
- Authorization
- Deployment engine
- Dependency resolution
- Resource Providers
- Azure Policy
- Resource Locks
- Deployment history

Every Azure deployment uses ARM.

---

## ARM Templates

ARM Templates provide Microsoft's native Infrastructure as Code implementation.

Benefits include:

- Declarative deployments
- Repeatable infrastructure
- Parameterized environments
- Idempotent deployments
- Version-controlled infrastructure

---

## Bicep

Bicep is Microsoft's recommended Infrastructure as Code language.

Advantages over ARM JSON include:

- Cleaner syntax
- Strong typing
- Modules
- Symbolic references
- Better readability
- Easier maintenance

Bicep compiles into ARM Templates before deployment.

---

# Typical Automation Workflow

```text
Write Infrastructure as Code

↓

Validate

↓

Run What-If

↓

Deploy

↓

Azure Resource Manager

↓

Azure Resources

↓

Review Deployment
```

This workflow minimizes deployment risk while ensuring consistent infrastructure provisioning.

---

# Design Principles

Microsoft recommends following these principles:

- Prefer Infrastructure as Code over manual deployments.
- Use Bicep for new Azure projects.
- Keep deployments idempotent.
- Separate templates from parameter files.
- Protect secrets with Azure Key Vault.
- Validate deployments before execution.
- Use What-If analysis before production deployments.
- Store automation in source control.
- Apply least privilege.
- Design reusable modules.

---

# Choosing the Right Tool

| Requirement | Recommended Tool |
|------------|------------------|
| Interactive Linux administration | Azure CLI |
| Object-oriented scripting | Azure PowerShell |
| Browser-based administration | Azure Cloud Shell |
| Declarative Infrastructure as Code | Bicep |
| ARM JSON compatibility | ARM Templates |
| Enterprise Infrastructure as Code | Bicep + Azure Resource Manager |

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Azure CLI
- Azure PowerShell
- Azure Cloud Shell
- Azure Resource Manager
- Infrastructure as Code
- ARM Templates
- Bicep
- Deployment validation
- What-If analysis
- Automation best practices

---

# Key Takeaways

- Automation is a fundamental Azure administration skill that enables consistent, repeatable, and scalable infrastructure management.
- Azure CLI, Azure PowerShell, Azure Cloud Shell, ARM Templates, and Bicep complement one another and all rely on Azure Resource Manager as the central deployment engine.
- Microsoft recommends Infrastructure as Code, modular deployments, secure secret management, deployment validation, and What-If analysis to reduce operational risk.
- Bicep is the preferred authoring language for new Azure deployments, while ARM Templates remain the underlying deployment format processed by Azure Resource Manager.
- Mastering Azure automation tools and Infrastructure as Code concepts is essential for enterprise Azure administration and is a major objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure CLI | https://learn.microsoft.com/cli/azure/ |
| Azure PowerShell | https://learn.microsoft.com/powershell/azure/ |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| ARM Templates | https://learn.microsoft.com/azure/azure-resource-manager/templates/ |
| Bicep | https://learn.microsoft.com/azure/azure-resource-manager/bicep/ |
| Microsoft Learn – Automate Azure Tasks | https://learn.microsoft.com/training/browse/?terms=Azure%20automation |
