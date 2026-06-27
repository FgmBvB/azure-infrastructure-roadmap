# Microsoft Entra ID

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

## Microsoft Entra ID Architecture

```text
                   Microsoft Entra ID
                          │
                     Entra Tenant
                          │
      ┌──────────┬─────────┼──────────┬──────────┐
      │          │         │          │          │
    Users     Groups    Devices   Applications  Identities
                                             │
                                  ┌──────────┴──────────┐
                                  │                     │
                         Service Principals   Managed Identities
```

---

> [!TIP]
> **Key Concepts**
>
> * Microsoft Entra ID is Microsoft's cloud-based identity and access management (IAM) service.
> * Every Azure subscription is associated with one Microsoft Entra ID tenant.
> * Authentication verifies identity.
> * Authorization determines permissions.
> * Microsoft Entra ID manages identities, not Azure resources.
> * Azure RBAC uses Microsoft Entra ID identities to control access to Azure resources.

---

## Overview

Microsoft Entra ID is Microsoft's cloud-based Identity and Access Management (IAM) platform.

It provides authentication, authorization, identity lifecycle management, application integration, and secure access to Microsoft cloud services and thousands of third-party applications.

Microsoft Entra ID is a fundamental component of Azure because every Azure subscription relies on a Microsoft Entra ID tenant to manage identities and access.

---

## Why Identity Matters

Before a user or application can access any Azure resource, Azure must answer two questions:

1. **Who are you?**
2. **What are you allowed to do?**

Microsoft Entra ID answers the first question by authenticating identities.

Azure Role-Based Access Control (Azure RBAC) answers the second by authorizing access to Azure resources.

Without Microsoft Entra ID, Azure cannot securely identify users, services, or applications.

---

## Authentication vs Authorization

```text
User
 │
 │ Credentials
 ▼
Microsoft Entra ID
 │
 ├── Authentication
 │      "Who are you?"
 │
 ▼
Azure RBAC
 │
 ├── Authorization
 │      "What can you do?"
 │
 ▼
Azure Resources
```

Authentication verifies the identity of a user, application, or workload.

Authorization determines which resources that identity is allowed to access and which operations it can perform.

These are independent processes that work together to secure Azure environments.

---

## Microsoft Entra ID Tenant

A Microsoft Entra ID tenant is a dedicated and isolated identity instance owned by an organization.

A tenant stores:

* Users
* Groups
* Devices
* Applications
* Service Principals
* Administrative roles
* Authentication policies

A single tenant can manage multiple Azure subscriptions.

However, an Azure subscription can only be associated with one Microsoft Entra ID tenant at a time.

---

## Identity Objects

Microsoft Entra ID manages several types of identity objects.

### Users

Represent people who need access to Azure resources or cloud applications.

Users can be:

* Cloud-only users
* Synchronized from on-premises Active Directory
* Guest users (B2B collaboration)

---

### Groups

Groups simplify permission management.

Instead of assigning permissions individually, administrators assign permissions to groups.

Supported group types include:

* Security Groups
* Microsoft 365 Groups

---

### Applications

Applications represent software registered within Microsoft Entra ID.

Application registrations define the identity of an application.

Applications themselves do not receive permissions directly.

---

### Service Principals

A Service Principal is the security identity created from an application registration.

Azure uses Service Principals when applications authenticate and access Azure resources securely.

Every enterprise application has an associated Service Principal within a tenant.

---

### Managed Identities

Managed Identities provide automatically managed identities for Azure resources.

They eliminate the need to store credentials, passwords, or secrets inside applications.

Azure automatically manages credential rotation.

Managed Identities can be:

* System-assigned
* User-assigned

---

### Devices

Microsoft Entra ID can manage registered, joined, or hybrid-joined devices.

Device identities enable secure authentication and Conditional Access policies.

---

## Hybrid Identity

```text
On-Premises Active Directory
              │
     Microsoft Entra Connect
              │
      Microsoft Entra ID
              │
 Azure, Microsoft 365,
 SaaS Applications
```

Many organizations continue using Active Directory on-premises.

Microsoft Entra Connect synchronizes users, groups, and selected identity information between Active Directory and Microsoft Entra ID.

This allows users to access both on-premises and cloud resources using a common identity.

---

## Enterprise Scenario

A company employs 2,000 users across multiple countries.

Employees access Azure Virtual Machines, Microsoft 365, internal web applications, and third-party SaaS services.

Instead of creating separate accounts for every platform, the organization manages identities centrally through Microsoft Entra ID.

Authentication occurs once, while Azure RBAC, Conditional Access, and application permissions determine what each user can access.

---

## Best Practices

* Enable Multi-Factor Authentication (MFA).
* Apply the principle of least privilege.
* Use Security Groups instead of assigning permissions directly to users.
* Protect privileged accounts.
* Use Managed Identities whenever possible.
* Monitor sign-in activity regularly.
* Use Conditional Access policies for additional security.

---

## Common Pitfalls

* Confusing authentication with authorization.
* Assigning permissions directly to individual users.
* Storing credentials inside applications.
* Creating excessive Global Administrators.
* Forgetting to review guest user access.
* Ignoring identity lifecycle management.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Microsoft Entra ID architecture
> * Tenants
> * Users
> * Groups
> * Devices
> * Applications
> * Service Principals
> * Managed Identities
> * Authentication vs Authorization
> * Microsoft Entra Connect
> * Azure RBAC relationship

---

## Key Takeaways

* Microsoft Entra ID is the identity platform for Azure.
* Every Azure subscription is associated with a Microsoft Entra ID tenant.
* Authentication verifies identity.
* Authorization determines permissions.
* Azure RBAC uses Microsoft Entra ID identities.
* Managed Identities eliminate credential management for Azure resources.
* Service Principals enable secure application authentication.
* Hybrid Identity connects on-premises Active Directory with Microsoft Entra ID.

---

## References

| Microsoft Documentation                                                                | Purpose                     |
| -------------------------------------------------------------------------------------- | --------------------------- |
| https://learn.microsoft.com/entra/fundamentals/whatis                                  | Microsoft Entra ID overview |
| https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users              | User management             |
| https://learn.microsoft.com/entra/fundamentals/concept-secure-remote-workers           | Identity fundamentals       |
| https://learn.microsoft.com/azure/role-based-access-control/overview                   | Azure RBAC overview         |
| https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview | Managed Identities          |
| https://learn.microsoft.com/entra/identity/hybrid/connect/whatis-azure-ad-connect-v2   | Microsoft Entra Connect     |

