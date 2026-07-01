# Azure Resource Manager (ARM)

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Resource Manager (ARM), Microsoft's deployment and management service for Azure resources. This section focuses on ARM Templates, Infrastructure as Code (IaC), deployment strategies, and modern deployment practices used throughout Azure.

---

# Overview

Azure Resource Manager (ARM) is the deployment and management layer of Microsoft Azure.

Every deployment performed through the Azure Portal, Azure CLI, Azure PowerShell, Bicep, Terraform, REST API, or SDKs ultimately passes through Azure Resource Manager.

ARM provides a consistent management plane responsible for authentication, authorization, resource deployment, dependency resolution, tagging, policy enforcement, resource locking, and deployment history.

Understanding ARM is fundamental for every Azure administrator and is heavily evaluated throughout the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Resource Manager architecture.
- Understand Infrastructure as Code (IaC).
- Deploy resources using ARM Templates.
- Understand template structure.
- Manage deployment modes.
- Validate deployments.
- Use ARM template functions.
- Understand Bicep and its relationship with ARM.
- Apply ARM deployment best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - ARM Templates** | ARM Template architecture, template structure, parameters, variables, resources, outputs, deployment modes, template functions, dependency management, validation, and AZ-104 concepts. |
| **02 - Best Practices** | Parameterization, Key Vault references, deployment validation, What-If analysis, Incremental deployments, template modularity, API versions, governance, source control, and Microsoft's production recommendations. |
| **05 - Bicep** | Microsoft's modern Infrastructure as Code language, Bicep syntax, modules, compilation to ARM Templates, deployment workflow, and comparison with JSON templates. |
| **06 - Best Practices** | Recommended practices for Bicep development, modular design, parameter management, version control, validation, deployment strategies, and enterprise Infrastructure as Code guidance. |

---

# Azure Resource Manager Architecture

```text
Administrator

↓

Azure Portal
Azure CLI
Azure PowerShell
Bicep
Terraform
REST API
SDKs

↓

Azure Resource Manager (ARM)

↓

Authentication
Authorization
Azure Policy
RBAC
Resource Locks
Deployment Engine

↓

Resource Providers

↓

Azure Resources
```

ARM acts as the centralized control plane for all Azure resource deployments.

---

# Core Capabilities

This section covers the primary Azure Resource Manager capabilities.

## Resource Deployment

- Resource provisioning
- Infrastructure as Code
- Dependency resolution
- Deployment validation
- Deployment history

---

## Governance

- Azure RBAC
- Azure Policy
- Resource Locks
- Tags
- Management Groups

---

## Infrastructure as Code

- ARM Templates
- Bicep
- Parameter files
- Template functions
- Modular deployments

---

## Deployment Management

- Incremental deployments
- Complete deployments
- What-If analysis
- Template validation
- Rollback through redeployment

---

# Typical Workflow

```text
Author Template

↓

Validate Template

↓

Run What-If

↓

Deploy

↓

Review Deployment

↓

Manage Resources
```

ARM provides a consistent deployment experience regardless of the tool used.

---

# Design Principles

Microsoft recommends following these principles:

- Prefer Infrastructure as Code over manual deployments.
- Use Incremental deployment mode for production.
- Separate templates from parameter files.
- Protect secrets with Azure Key Vault.
- Validate deployments before execution.
- Use What-If to predict deployment impact.
- Store templates in source control.
- Keep templates modular and reusable.
- Use current API versions.
- Design idempotent deployments.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Resource Manager
- ARM Templates
- Infrastructure as Code
- Deployment modes
- Template functions
- Parameters and variables
- Dependency management
- Validation
- What-If
- Bicep

---

# Key Takeaways

- Azure Resource Manager is the centralized control plane responsible for deploying, organizing, securing, and managing Azure resources.
- ARM enables consistent Infrastructure as Code deployments through ARM Templates and serves as the deployment engine behind Bicep.
- Features such as deployment validation, What-If analysis, dependency resolution, parameterization, and template functions improve deployment reliability and reduce operational risk.
- Microsoft recommends modular templates, Incremental deployments, Azure Key Vault integration for secrets, and version control for Infrastructure as Code projects.
- A solid understanding of Azure Resource Manager, ARM Templates, and Bicep is essential for both enterprise Azure administration and success in the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Resource Manager documentation | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| ARM Templates | https://learn.microsoft.com/azure/azure-resource-manager/templates/ |
| ARM Template reference | https://learn.microsoft.com/azure/templates/ |
| Bicep documentation | https://learn.microsoft.com/azure/azure-resource-manager/bicep/ |
| ARM deployment modes | https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes |
| Microsoft Learn – Azure Resource Manager | https://learn.microsoft.com/training/modules/create-azure-resource-manager-template-vs-code/ |
