# Tenant and Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the core concepts of Microsoft Entra ID tenants and digital identities.

---

## Microsoft Entra ID Tenant

```text
                    Microsoft Entra ID
                           │
                     Entra Tenant
                           │
        ┌──────────┬──────────┬──────────┐
        │          │          │
      Users      Groups    Applications
        │
        └───────────────► Azure Resources
```

---

> [!TIP]
> **Key Concepts**
>
> - A tenant is a dedicated Microsoft Entra ID instance.
> - Each tenant has its own identities and security configuration.
> - A tenant can manage multiple Azure subscriptions.
> - Every Azure subscription is associated with one tenant.
> - Identities authenticate to Microsoft Entra ID before accessing Azure resources.
> - Azure RBAC authorizes authenticated identities to Azure resources.

---

## Overview

Microsoft Entra ID is organized around the concept of a **tenant**.

A tenant is a dedicated and isolated instance of Microsoft Entra ID that represents an organization.

It stores identity-related objects such as users, groups, applications, devices, administrative roles, authentication policies, and security settings.

Every organization using Microsoft Entra ID owns at least one tenant.

---

## What Is a Tenant?

A tenant is the highest identity boundary within Microsoft Entra ID.

It provides centralized identity management for Azure, Microsoft 365, and thousands of integrated applications.

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

A single Microsoft Entra ID tenant can be associated with multiple Azure subscriptions.

However, each Azure subscription can belong to only one tenant at a time.

---

## Tenant Identifier

Every Microsoft Entra ID tenant has a globally unique identifier known as the **Tenant ID**.

The Tenant ID is widely used by Azure Portal, Azure CLI, PowerShell, Microsoft Graph, and automation tools when authenticating or managing Azure environments.

Each tenant also has a default domain, typically in the following format:

```text
contoso.onmicrosoft.com
```

Organizations commonly add one or more custom domains, such as:

```text
contoso.com
```

---

## What Is an Identity?

An identity is any object that Microsoft Entra ID can authenticate.

After authentication, Azure services determine what that identity is allowed to access through authorization mechanisms such as Azure RBAC.

Common identity types include:

| Identity | Purpose |
|----------|---------|
| User | Human users |
| Group | Permission management |
| Service Principal | Applications and automation |
| Managed Identity | Azure resources |
| Device | Registered devices |

Authentication verifies **who the identity is**.

Authorization determines **what the identity is allowed to do**.

---

## Tenant Isolation

Each Microsoft Entra ID tenant is isolated from every other tenant.

Objects stored inside one tenant are not visible to another tenant unless explicitly shared using **Microsoft Entra External ID (B2B collaboration)**.

This isolation provides administrative, security, and compliance boundaries between organizations.

---

## Trust Relationship

Azure subscriptions establish a trust relationship with a Microsoft Entra ID tenant.

The tenant authenticates identities, while the Azure subscription relies on those identities to perform authorization through Azure RBAC.

If an Azure subscription is transferred to another tenant, Azure RBAC assignments and identity relationships must be reconfigured because security principals are unique to each tenant.

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

Microsoft Entra ID manages identities.

Azure Resource Manager manages Azure resources.

Azure RBAC connects both by authorizing authenticated identities to perform actions on Azure resources.

---

## Administrative Boundary

Microsoft Entra ID administrative roles and Azure RBAC roles are independent.

Being a **Global Administrator** in Microsoft Entra ID does not automatically grant administrative permissions over Azure subscriptions or Azure resources.

In emergency scenarios, a Global Administrator can enable **Access management for Azure resources**, which temporarily grants the **User Access Administrator** role at the root scope of Azure subscriptions. This capability is intended for recovery and administrative scenarios.

---

## Enterprise Scenario

A company creates a Microsoft Entra ID tenant for its organization.

Employees authenticate using corporate accounts stored in the tenant.

The organization manages two Azure subscriptions:

- Development
- Production

Both subscriptions trust the same Microsoft Entra ID tenant for authentication while remaining independent for billing, governance, and resource management.

Azure RBAC determines which users can administer each subscription.

---

## Best Practices

- Use a single tenant unless multiple tenants are required.
- Protect privileged identities with Multi-Factor Authentication.
- Apply the principle of least privilege.
- Review guest users regularly.
- Use Security Groups instead of assigning permissions directly to users.
- Document tenant ownership and administrative responsibilities.

---

## Common Pitfalls

- Confusing a tenant with an Azure subscription.
- Confusing authentication with authorization.
- Assuming Global Administrators automatically manage Azure resources.
- Assigning permissions directly to individual users.
- Creating unnecessary Global Administrator accounts.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID tenants
> - Tenant isolation
> - Tenant ID
> - Tenant and subscription relationship
> - Identity concepts
> - Authentication versus authorization
> - Trust relationship between tenant and subscriptions
> - Azure RBAC relationship
> - Administrative boundaries

---

## Key Takeaways

- A tenant is an isolated Microsoft Entra ID directory.
- Every tenant has a unique Tenant ID.
- A tenant stores identities and security configuration.
- Multiple Azure subscriptions can belong to one tenant.
- Every Azure subscription belongs to only one tenant.
- Microsoft Entra ID authenticates identities.
- Azure RBAC authorizes authenticated identities.
- Microsoft Entra ID administrative roles are different from Azure RBAC roles.

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
