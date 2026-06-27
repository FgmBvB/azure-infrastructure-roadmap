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
> - Identities are used to authenticate and access Azure resources.

---

## Overview

Microsoft Entra ID is organized around the concept of a **tenant**.

A tenant is a dedicated and isolated instance of Microsoft Entra ID that represents an organization.

It stores all identity-related information, including users, groups, applications, devices, administrative roles, and security settings.

Every organization that uses Microsoft Entra ID owns at least one tenant.

---

## What Is a Tenant?

A tenant is the highest-level identity boundary within Microsoft Entra ID.

It acts as the identity directory for an organization and provides centralized identity management across Azure and Microsoft cloud services.

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

Multiple Azure subscriptions can be associated with the same tenant.

However, each Azure subscription can only belong to one tenant at any given time.

---

## What Is an Identity?

An identity is any object that can be authenticated by Microsoft Entra ID.

Once authenticated, the identity can be authorized to access Azure resources or cloud applications.

Common identity types include:

- User identities
- Application identities
- Service Principals
- Managed Identities
- Device identities

Authentication proves **who the identity is**.

Authorization determines **what the identity is allowed to do**.

---

## Tenant Isolation

Each Microsoft Entra ID tenant is isolated from other tenants.

Objects stored inside one tenant are not visible to another tenant unless explicitly shared through collaboration features such as Azure AD B2B (Microsoft Entra External ID).

This isolation provides security and administrative separation between organizations.

---

## Relationship with Azure

```text
                 Microsoft Entra ID Tenant
                          │
         ┌────────────────┴────────────────┐
         │                                 │
 Subscription A                     Subscription B
         │                                 │
   Resource Groups                  Resource Groups
         │                                 │
     Azure Resources                 Azure Resources
```

Microsoft Entra ID manages identities.

Azure subscriptions contain Azure resources.

Azure RBAC connects both by granting identities permissions over Azure resources.

---

## Enterprise Scenario

A company creates a Microsoft Entra ID tenant for its organization.

Employees authenticate using corporate accounts stored in the tenant.

The organization manages two Azure subscriptions:

- Production
- Development

Both subscriptions use the same Microsoft Entra ID tenant for authentication while remaining independent for billing and resource management.

---

## Best Practices

- Use a single tenant unless multiple tenants are required.
- Protect privileged identities with Multi-Factor Authentication.
- Apply the principle of least privilege.
- Regularly review guest users.
- Document tenant ownership and administrative roles.

---

## Common Pitfalls

- Confusing a tenant with an Azure subscription.
- Assuming users automatically receive Azure permissions.
- Creating unnecessary Global Administrators.
- Mixing authentication with authorization concepts.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID tenants
> - Identity concepts
> - Tenant isolation
> - Tenant and subscription relationship
> - Authentication versus authorization
> - Identity boundaries in Azure

---

## Key Takeaways

- A tenant is an isolated Microsoft Entra ID directory.
- A tenant stores identities and security configuration.
- Multiple subscriptions can belong to one tenant.
- Every subscription belongs to only one tenant.
- Identities authenticate to Microsoft Entra ID before accessing Azure resources.
- Azure RBAC authorizes authenticated identities to perform actions.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/fundamentals/whatis | Microsoft Entra ID overview |
| https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users | Identity management |
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC overview |
| https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/ | Microsoft Learn – Identity concepts |
