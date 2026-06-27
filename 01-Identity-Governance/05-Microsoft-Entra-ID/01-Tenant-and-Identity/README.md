# Tenant and Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the core concepts of Microsoft Entra ID tenants, identity boundaries, and how Azure uses identities to secure cloud resources.

---

## Microsoft Entra ID Tenant

```text
                    Microsoft Entra ID
                           │
                     Entra Tenant
                           │
      ┌─────────┬─────────┬──────────┬──────────────┬──────────┐
      │         │         │          │              │
    Users    Groups    Devices   Applications   Policies
                                               │
                                       Administrative Roles
```

---

> [!TIP]
> **Key Concepts**
>
> - A tenant is a dedicated Microsoft Entra ID instance.
> - Each tenant has its own identities, policies, and security configuration.
> - Every Azure subscription is associated with one Microsoft Entra ID tenant.
> - A tenant can manage multiple Azure subscriptions.
> - Authentication verifies identities.
> - Azure RBAC authorizes authenticated identities to Azure resources.

---

## Overview

Microsoft Entra ID is Microsoft's cloud-based Identity and Access Management (IAM) platform.

Its primary purpose is to authenticate identities and provide secure access to Azure, Microsoft 365, Microsoft services, and thousands of third-party applications.

Every organization that uses Microsoft Entra ID owns at least one tenant, which acts as the organization's dedicated identity directory.

Microsoft Entra ID is one of the most fundamental Azure services because every Azure subscription relies on a tenant to authenticate identities before they can access Azure resources.

---

## What Is a Tenant?

A tenant is an isolated instance of Microsoft Entra ID owned by an organization.

It represents the highest identity boundary within Microsoft Entra ID and stores all identity-related information for that organization.

A tenant can contain:

- Users
- Groups
- Devices
- Applications
- Enterprise Applications
- Service Principals
- Managed Identities
- Administrative Roles
- Authentication Policies
- Security Policies

A single tenant can manage multiple Azure subscriptions.

However, an Azure subscription can only belong to one Microsoft Entra ID tenant at any given time.

---

## Directory Terminology

Microsoft documentation commonly uses the terms **tenant** and **directory** interchangeably.

Historically, Azure documentation referred to an **Azure Active Directory (Azure AD) directory**.

Following the Microsoft Entra rebranding, the preferred terminology is **Microsoft Entra ID tenant**, although many APIs, tools, and enterprise environments still refer to it simply as a directory.

Understanding both terms is important because you will encounter them frequently in documentation, PowerShell, Azure CLI, Microsoft Graph, and production environments.

---

## Tenant Identifier

Every Microsoft Entra ID tenant has a globally unique identifier known as the **Tenant ID**.

This GUID uniquely identifies the tenant across Microsoft cloud services and is commonly required by:

- Azure Portal
- Azure CLI
- Azure PowerShell
- Microsoft Graph
- REST APIs
- Infrastructure as Code tools

Each tenant also has a default domain similar to:

```text
contoso.onmicrosoft.com
```

Organizations commonly add one or more custom domains such as:

```text
contoso.com
```

---

## What Is an Identity?

An identity is any object that Microsoft Entra ID can authenticate.

After authentication, Azure determines what that identity is allowed to access through authorization mechanisms such as Azure Role-Based Access Control (Azure RBAC).

Common identity types include:

| Identity | Purpose |
|----------|---------|
| User | Human users |
| Group | Permission management |
| Service Principal | Workload identity for applications and automation |
| Managed Identity | Azure-managed identity for Azure resources |
| Device | Registered devices |

> [!TIP]
> Service Principals and Managed Identities are workload identities used by applications and Azure resources.
>
> Their authentication model, architecture, and security considerations are covered in dedicated sections later in this roadmap.

Authentication answers the question:

> **Who are you?**

Authorization answers the question:

> **What are you allowed to do?**

Although closely related, they are completely different security processes.

---

## Tenant Isolation

Every Microsoft Entra ID tenant is isolated from every other tenant.

Objects stored inside one tenant cannot be accessed by another tenant unless explicitly shared.

Organizations can collaborate securely through **Microsoft Entra External ID (B2B collaboration)**, which allows guest users from external organizations to access selected resources without compromising tenant isolation.

Tenant isolation provides:

- Administrative separation
- Security boundaries
- Identity isolation
- Compliance boundaries

---

## Trust Relationship

Azure subscriptions establish a trust relationship with a Microsoft Entra ID tenant.

The tenant is responsible for authenticating identities.

Azure Resource Manager trusts the tenant to verify identities before Azure RBAC evaluates permissions.

If an Azure subscription is transferred to another tenant, Azure RBAC assignments and identity relationships must be recreated because security principals are unique to each Microsoft Entra ID tenant.

---

## Relationship with Azure

```text
                 Microsoft Entra ID Tenant
                          │
                  Authentication
                          │
                     Azure RBAC
                          │
        ┌─────────────────┴─────────────────┐
        │                                   │
 Subscription A                      Subscription B
        │                                   │
  Resource Groups                   Resource Groups
        │                                   │
   Azure Resources                  Azure Resources
```

Microsoft Entra ID is responsible for identity management.

Azure Resource Manager manages Azure resources.

Azure RBAC connects both services by authorizing authenticated identities to perform actions on Azure resources.

---

## Administrative Boundary

Microsoft Entra ID administrative roles and Azure RBAC roles are independent security systems.

Being assigned the **Global Administrator** role in Microsoft Entra ID does **not** automatically grant administrative permissions over Azure subscriptions or Azure resources.

Azure resources are protected by Azure Role-Based Access Control (Azure RBAC), which operates independently from Microsoft Entra ID administrative roles.

In emergency scenarios, a Global Administrator can enable **Access management for Azure resources**.

When enabled, Azure assigns the **User Access Administrator** role at the **Root Management Group**, allowing RBAC permissions to be inherited across Azure subscriptions within the tenant.

This feature is intended for recovery scenarios, such as regaining administrative access when Azure RBAC permissions have been lost.

---

## Enterprise Scenario

A multinational company manages more than 5,000 employees across several countries.

The organization creates a single Microsoft Entra ID tenant to centralize identity management.

Within the tenant, administrators manage:

- Employee accounts
- Security Groups
- Devices
- Enterprise Applications
- Authentication Policies

Two Azure subscriptions are associated with the tenant:

- Production
- Development

Employees authenticate once using Microsoft Entra ID.

Azure RBAC then determines which Azure resources each identity is allowed to access.

This centralized identity model simplifies administration while maintaining strong security boundaries.

---

## Best Practices

- Use a single tenant unless multiple tenants are required for business or regulatory reasons.
- Protect privileged identities using Multi-Factor Authentication (MFA).
- Apply the principle of least privilege.
- Assign permissions to Security Groups instead of individual users whenever possible.
- Review guest users regularly.
- Limit the number of Global Administrators.
- Protect privileged accounts using Conditional Access policies.
- Document tenant ownership and administrative responsibilities.

---

## Common Pitfalls

- Confusing a Microsoft Entra ID tenant with an Azure subscription.
- Confusing authentication with authorization.
- Assuming Global Administrators automatically have Azure RBAC permissions.
- Assigning Azure permissions directly to users instead of groups.
- Creating unnecessary Global Administrator accounts.
- Forgetting to review guest user access.
- Mixing identity administration with Azure resource administration.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID tenants
> - Tenant isolation
> - Tenant ID
> - Tenant domains
> - Identity concepts
> - Authentication versus authorization
> - Trust relationship between Microsoft Entra ID and Azure subscriptions
> - Azure RBAC relationship
> - Administrative boundaries
> - Root Management Group access elevation

---

## Key Takeaways

- A tenant is an isolated Microsoft Entra ID directory.
- Every tenant has a globally unique Tenant ID.
- A tenant stores identities, security settings, and authentication policies.
- Multiple Azure subscriptions can belong to one tenant.
- Every Azure subscription belongs to only one tenant at a time.
- Microsoft Entra ID authenticates identities.
- Azure RBAC authorizes authenticated identities.
- Microsoft Entra ID administrative roles are different from Azure RBAC roles.
- Microsoft documentation may use the terms **tenant** and **directory** interchangeably.
- Tenant isolation is one of the fundamental security boundaries in Microsoft Azure.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/fundamentals/whatis | Microsoft Entra ID overview |
| https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users | Tenant and identity management |
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC overview |
| https://learn.microsoft.com/azure/role-based-access-control/elevate-access-global-admin | Elevate access for Global Administrators |
| https://learn.microsoft.com/entra/external-id/external-identities-overview | Microsoft Entra External ID (B2B collaboration) |
| https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/ | Microsoft Learn – Identity concepts |
