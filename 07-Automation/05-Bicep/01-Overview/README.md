# Bicep Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces **Bicep**, Microsoft's modern Infrastructure as Code (IaC) language for Azure deployments. Bicep simplifies ARM template authoring while using Azure Resource Manager (ARM) as the underlying deployment engine.

---

# Overview

Bicep is Microsoft's domain-specific language (DSL) for deploying Azure infrastructure.

It provides a cleaner, more readable syntax than ARM Templates while compiling directly into standard ARM JSON templates before deployment.

Bicep is **declarative**, meaning administrators describe the desired infrastructure state rather than the individual deployment steps.

Although Bicep replaces ARM Templates as the preferred authoring language, deployments are still executed by **Azure Resource Manager (ARM)**.

Microsoft recommends Bicep for all new Infrastructure as Code projects.

---

# Bicep Architecture

```text
Administrator

↓

Bicep File (.bicep)

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

The Bicep compiler converts the source file into a standard ARM template before Azure Resource Manager processes the deployment.

---

# Bicep Compilation

Bicep is an authoring language and is **not** sent directly to Azure.

Before deployment, Bicep is **transpiled** into a standard ARM Template (JSON).

The compilation can be performed explicitly:

```bash
bicep build main.bicep
```

or automatically when deploying with Azure CLI or Azure PowerShell.

Example:

```bash
az deployment group create \
    --resource-group MyRG \
    --template-file main.bicep
```

In this case, Azure CLI invokes the Bicep compiler automatically before submitting the generated ARM template to Azure Resource Manager.

> [!IMPORTANT]
> Azure Resource Manager never deploys Bicep files directly. Every deployment is ultimately processed as an ARM Template.

---

# Infrastructure as Code (IaC)

Bicep fully supports the Infrastructure as Code model.

Benefits include:

- Declarative deployments
- Repeatable infrastructure
- Version-controlled environments
- Reduced configuration drift
- Easier automation
- Improved readability
- Native ARM compatibility

---

# Declarative Language

Like ARM Templates, Bicep is declarative.

Administrators define:

- Resources
- Configuration
- Dependencies
- Relationships
- Desired end state

Azure Resource Manager determines the deployment sequence automatically.

---

# Bicep File Structure

A typical Bicep file contains:

```text
Parameters

↓

Variables

↓

Resources

↓

Modules

↓

Outputs
```

Each section contributes to building reusable infrastructure.

---

# Parameters

Parameters allow customization without modifying the template.

Typical parameters include:

- Resource names
- Location
- VM size
- Storage SKU
- Environment
- Tags

Parameters improve reusability across environments.

---

# Variables

Variables store reusable expressions.

Benefits:

- Cleaner code
- Less duplication
- Easier maintenance

Variables are evaluated during deployment.

---

# Resources

Resources define Azure infrastructure.

Examples include:

- Virtual Machines
- Storage Accounts
- Virtual Networks
- NSGs
- Key Vault
- Load Balancers
- Azure SQL
- App Service

Resources use strongly typed syntax that improves readability and editor support.

---

# Implicit Dependencies

One of Bicep's major advantages is its ability to infer resource dependencies automatically.

When one resource references another using its symbolic name, Bicep generates the required deployment dependency without requiring an explicit `dependsOn`.

Example:

```bicep
resource subnet 'Microsoft.Network/virtualNetworks/subnets@2023-11-01' = {
  ...
}

resource nic 'Microsoft.Network/networkInterfaces@2023-11-01' = {
  properties: {
    ipConfigurations: [
      {
        properties: {
          subnet: {
            id: subnet.id
          }
        }
      }
    ]
  }
}
```

Because the network interface references `subnet.id`, Bicep automatically creates the dependency.

This reduces template complexity and allows Azure Resource Manager to maximize parallel deployment whenever possible.

> [!TIP]
> Explicit `dependsOn` is only required when a dependency cannot be inferred automatically.

---

# Modules

Modules allow large deployments to be divided into reusable components.

Typical modules include:

- Networking
- Storage
- Compute
- Security
- Monitoring

Benefits:

- Code reuse
- Easier maintenance
- Team collaboration
- Smaller deployments

Modules are one of the major improvements over traditional ARM Templates.

---

# Existing Resources

Bicep can reference Azure resources that already exist without redeploying them.

The **existing** keyword declares an existing resource so that its properties and resource ID can be used by the deployment.

Example:

```bicep
resource vnet 'Microsoft.Network/virtualNetworks@2023-11-01' existing = {
  name: 'vnet-core-prod'
}
```

Typical scenarios include:

- Deploying a Virtual Machine into an existing Virtual Network.
- Using an existing Key Vault.
- Connecting to an existing Storage Account.
- Reusing shared networking infrastructure.

Using **existing** improves modularity and allows independent deployments to integrate with previously deployed Azure resources.

> [!IMPORTANT]
> The resource must already exist. The deployment references it but does not create or modify it unless explicitly declared elsewhere.

---

# Outputs

Outputs return values after deployment.

Examples:

- Resource IDs
- Public IP addresses
- Storage endpoints
- DNS names

Outputs are commonly consumed by automation pipelines and other deployments.

---

# Type Safety

Bicep provides strong type validation.

The language validates:

- Resource properties
- Parameter types
- Allowed values
- Functions
- Resource references

Many deployment errors are detected before Azure receives the deployment.

---

# IntelliSense Support

Bicep integrates with Visual Studio Code.

Features include:

- IntelliSense
- Auto-completion
- Syntax validation
- Resource documentation
- Parameter hints
- Error highlighting

This significantly improves the authoring experience.

---

# Bicep vs ARM Templates

| Bicep | ARM Templates |
|--------|---------------|
| Simple syntax | JSON syntax |
| Highly readable | Verbose |
| Native modules | Linked templates |
| Strong typing | Limited validation |
| Easier maintenance | More complex |
| Compiles to ARM JSON | Native deployment format |

Both ultimately deploy through Azure Resource Manager.

---

# Deployment Methods

Bicep files can be deployed using:

- Azure CLI
- Azure PowerShell
- Azure Portal
- Azure Cloud Shell
- Azure DevOps
- GitHub Actions

No manual conversion to JSON is required during deployment.

---

# Enterprise Scenario

A company deploys identical infrastructure to Development, Test, and Production.

Administrators:

- Create reusable Bicep modules.
- Store templates in Git.
- Parameterize each environment.
- Validate deployments.
- Deploy using Azure CLI through CI/CD pipelines.

The result is consistent, repeatable, and maintainable infrastructure.

---

# Common Pitfalls

- Hardcoding values.
- Ignoring parameterization.
- Creating overly large files instead of modules.
- Embedding secrets directly in templates.
- Using outdated resource API versions.
- Forgetting to validate deployments.
- Assuming Bicep bypasses Azure Resource Manager.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Bicep architecture
> - Infrastructure as Code
> - Parameters
> - Variables
> - Resources
> - Modules
> - Outputs
> - Type safety
> - Bicep vs ARM Templates
> - Deployment workflow

---

# Key Takeaways

- Bicep is Microsoft's recommended Infrastructure as Code language for Azure and provides a simpler, more maintainable alternative to ARM Templates.
- Bicep compiles into standard ARM JSON templates, which are deployed through Azure Resource Manager.
- Features such as modules, strong typing, IntelliSense, and reusable parameters improve development productivity and deployment reliability.
- Bicep supports the full Azure Resource Manager deployment model while significantly reducing template complexity.
- Understanding Bicep, its relationship with ARM, and its deployment workflow is an important objective of the AZ-104 certification.

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
