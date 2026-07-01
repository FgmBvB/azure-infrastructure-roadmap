# ARM Templates Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Resource Manager (ARM) Templates, Microsoft's native Infrastructure as Code (IaC) solution for declaratively deploying and managing Azure resources.

---

# Overview

ARM Templates are JSON files that define Azure infrastructure using a declarative syntax.

Instead of manually creating Azure resources through the Azure Portal, administrators describe the desired infrastructure in a template, and Azure Resource Manager automatically provisions the required resources.

ARM Templates provide consistent, repeatable, and idempotent deployments, making them a fundamental technology for Infrastructure as Code (IaC) in Azure.

Although Microsoft now recommends **Bicep** as the preferred authoring language, ARM Templates remain the deployment engine behind Bicep and continue to be an important topic for the AZ-104 certification.

---

# Azure Resource Manager Deployment Architecture

```text
Administrator

↓

ARM Template (.json)

↓

Azure Resource Manager (ARM)

↓

Resource Providers

↓

Azure Resources
```

Azure Resource Manager interprets the ARM template, validates it, resolves dependencies, and deploys resources through the appropriate Azure Resource Providers.

---

# Infrastructure as Code (IaC)

ARM Templates implement the Infrastructure as Code (IaC) model.

Benefits include:

- Repeatable deployments
- Version-controlled infrastructure
- Consistent environments
- Automated provisioning
- Reduced configuration drift
- Easier disaster recovery

---

# Declarative Model

ARM Templates are **declarative**.

Administrators define:

- What resources should exist.
- Desired configuration.
- Resource relationships.
- Dependencies.

Azure Resource Manager determines the order of deployment automatically.

Unlike imperative scripting, administrators do not specify how to create each resource step by step.

---

# ARM Template Structure

An ARM template typically contains the following sections:

```text
Schema

↓

Content Version

↓

Parameters

↓

Variables

↓

Resources

↓

Outputs
```

Each section has a specific purpose during deployment.

---

# Parameters

Parameters allow administrators to customize deployments without modifying the template itself.

Typical parameters include:

- Resource names
- Locations
- VM sizes
- Storage SKU
- Network configuration

Parameters improve template reusability.

---

# Variables

Variables simplify templates by storing reusable values.

Variables:

- Reduce duplication.
- Improve readability.
- Simplify maintenance.

Variables are evaluated during deployment.

---

# Common ARM Template Functions

ARM Templates include built-in functions that generate dynamic values during deployment.

Some of the most frequently used functions are:

| Function | Purpose |
|----------|---------|
| `concat()` | Combines multiple strings into a single value. |
| `uniqueString()` | Generates a deterministic unique string based on the supplied value. Commonly used to create globally unique Storage Account names. |
| `resourceId()` | Returns the fully qualified Azure Resource Manager ID of a resource. Used to reference existing resources across deployments. |

Example:

```json
"name": "[concat(parameters('storagePrefix'), uniqueString(resourceGroup().id))]"
```

These functions improve template portability and eliminate hardcoded values.

---

# Resources

The **Resources** section defines the Azure infrastructure.

Examples include:

- Virtual Machines
- Virtual Networks
- Storage Accounts
- Network Security Groups
- Key Vault
- App Services
- Azure SQL
- Load Balancers

Each resource specifies:

- Resource type
- API version
- Properties
- Dependencies

---

# Outputs

Outputs return useful deployment information after completion.

Examples include:

- Resource IDs
- Public IP addresses
- DNS names
- Storage endpoints

Outputs can be consumed by automation pipelines or subsequent deployments.

---

# Deployment Modes

ARM supports two deployment modes.

| Mode | Description |
|------|-------------|
| Incremental | Creates or updates resources defined in the template while leaving unmanaged resources unchanged. **Recommended and default mode.** |
| Complete | Resources that exist in the target scope but are not defined in the template are deleted. Use with extreme caution. |

Incremental deployments are recommended for most production environments.

---

# Complete Deployment Mode

Complete mode should be used with extreme caution.

When an ARM template is deployed in **Complete** mode, Azure Resource Manager removes resources that exist in the deployment scope but are not defined in the template.

For example, if the deployment target is a Resource Group:

- Resources defined in the template are created or updated.
- Resources not defined in the template may be deleted.

Because Complete mode can unintentionally remove infrastructure, Microsoft recommends using **Incremental** mode for most production deployments.

> [!IMPORTANT]
> Resource deletion behavior depends on the deployment scope and the resource provider. Always validate the expected impact before using Complete mode in production.

---

# Dependency Management

Azure Resource Manager automatically determines deployment order.

Dependencies can be defined explicitly using:

```json
dependsOn
```

When possible, ARM also detects implicit dependencies automatically.

Parallel deployment improves provisioning performance.

---

# Resource Iteration

ARM Templates support deploying multiple similar resources using the **copy** element.

The associated **copyIndex()** function returns the current iteration number during deployment.

Example:

```json
"name": "[concat('vm', copyIndex())]"
```

This mechanism allows Azure Resource Manager to generate sequential resource names such as:

- vm0
- vm1
- vm2

Typical use cases include deploying:

- Multiple Virtual Machines
- Storage Accounts
- Managed Disks
- Network Interfaces

Using **copy** reduces template duplication and simplifies large deployments.

---

# Validation

Templates can be validated before deployment.

Validation checks include:

- Syntax
- Parameters
- Resource types
- API versions
- Permissions

Validation helps detect deployment issues before Azure provisions resources.

---

# ARM Templates and Bicep

Bicep is Microsoft's recommended authoring language.

Relationship:

```text
Bicep

↓

Compilation

↓

ARM Template (JSON)

↓

Azure Resource Manager

↓

Azure Resources
```

Bicep simplifies authoring while ARM Templates remain the underlying deployment format.

---

# Deployment Methods

ARM Templates can be deployed using:

- Azure Portal
- Azure CLI
- Azure PowerShell
- Azure DevOps
- GitHub Actions
- Azure Cloud Shell

---

# Enterprise Scenario

A company must deploy identical infrastructure across Development, Test, and Production environments.

Using ARM Templates, administrators:

- Define infrastructure once.
- Parameterize environment-specific values.
- Store templates in Git.
- Validate deployments.
- Deploy consistently across all environments.

This approach minimizes configuration drift and simplifies infrastructure management.

---

# Common Pitfalls

- Hardcoding values instead of using parameters.
- Using Complete mode unintentionally.
- Ignoring template validation.
- Duplicating reusable values instead of variables.
- Using outdated API versions.
- Storing secrets directly inside templates.
- Creating unnecessary explicit dependencies.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - ARM Templates
> - Infrastructure as Code
> - Declarative deployments
> - Template structure
> - Parameters
> - Variables
> - Resources
> - Outputs
> - Deployment modes
> - Dependencies
> - Validation
> - ARM Templates vs Bicep

---

# Key Takeaways

- ARM Templates are Microsoft's native Infrastructure as Code solution for declaratively deploying Azure resources through Azure Resource Manager.
- Templates consist of reusable sections such as parameters, variables, resources, and outputs, enabling consistent and repeatable infrastructure deployments.
- Azure Resource Manager automatically validates templates, resolves dependencies, and provisions resources in the appropriate order.
- Incremental deployment mode is the recommended option for most production environments, while Complete mode should be used with caution.
- Although Bicep is the preferred authoring language, understanding ARM Templates remains essential because they are the underlying deployment engine and continue to be evaluated in the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| ARM Templates documentation | https://learn.microsoft.com/azure/azure-resource-manager/templates/ |
| ARM Template reference | https://learn.microsoft.com/azure/templates/ |
| Deploy ARM templates | https://learn.microsoft.com/azure/azure-resource-manager/templates/deploy-portal |
| ARM deployment modes | https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes |
| Bicep documentation | https://learn.microsoft.com/azure/azure-resource-manager/bicep/ |
| Microsoft Learn – Deploy Azure resources by using ARM templates | https://learn.microsoft.com/training/modules/create-azure-resource-manager-template-vs-code/ |
