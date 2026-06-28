# Hybrid Identity Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Hybrid Identity, explains how on-premises Active Directory integrates with Microsoft Entra ID, and describes the authentication and synchronization models used in hybrid environments.

---

## Hybrid Identity Architecture

```text
        On-Premises
     Active Directory
             │
             │
   Identity Synchronization
             │
             ▼
   Microsoft Entra ID
             │
             ▼
 Cloud Authentication
             │
             ▼
Microsoft 365 • Azure • SaaS Apps
```

---

> [!TIP]
> **Key Concepts**
>
> - Hybrid Identity connects on-premises Active Directory with Microsoft Entra ID.
> - Users can access both on-premises and cloud resources with a single identity.
> - Synchronization keeps identity information consistent.
> - Multiple authentication methods are available.
> - Hybrid Identity simplifies migration to the cloud.

---

## Overview

Hybrid Identity allows organizations to integrate their on-premises Active Directory with Microsoft Entra ID.

Users continue using their existing corporate identities while gaining access to Microsoft 365, Azure, and other cloud services.

This approach enables organizations to adopt cloud services gradually without replacing their existing identity infrastructure.

---

## Why Hybrid Identity?

Organizations commonly adopt Hybrid Identity to:

- Maintain existing Active Directory environments.
- Provide Single Sign-On (SSO).
- Simplify user management.
- Support cloud migration.
- Centralize identity governance.
- Improve security with Microsoft Entra ID features.

---

## Core Components

A Hybrid Identity deployment typically includes:

| Component | Purpose |
|----------|---------|
| **Active Directory Domain Services (AD DS)** | Stores on-premises identities. |
| **Microsoft Entra ID** | Provides cloud identity services. |
| **Microsoft Entra Connect** | Synchronizes identities between AD DS and Microsoft Entra ID. |
| **Authentication Method** | Determines how users authenticate to cloud services. |

---

## Authentication Models

Microsoft Entra ID supports multiple authentication methods for hybrid environments.

| Method | Description |
|--------|-------------|
| **Password Hash Synchronization (PHS)** | Synchronizes password hashes to Microsoft Entra ID. |
| **Pass-through Authentication (PTA)** | Password validation occurs against on-premises Active Directory. |
| **Federation** | Authentication is delegated to a federation service such as AD FS. |

Each method offers different balances between simplicity, infrastructure requirements, and security.

---

## Identity Synchronization

Hybrid Identity depends on synchronization between Active Directory and Microsoft Entra ID.

Synchronization includes information such as:

- Users
- Groups
- Contacts
- Device objects (when configured)

Microsoft Entra Connect or Microsoft Entra Cloud Sync maintains identity consistency between both environments.

---

## Single Sign-On

Hybrid Identity enables users to access cloud resources using their corporate credentials.

After successful authentication, users can access supported Microsoft cloud services without repeatedly entering credentials.

The authentication experience depends on the selected authentication method.

---

## Typical Authentication Flow

```text
User
 │
 ▼
Active Directory
 │
 ▼
Microsoft Entra Connect
 │
 ▼
Microsoft Entra ID
 │
 ▼
Microsoft 365 / Azure
```

---

## Enterprise Scenario

A company has an on-premises Active Directory with 2,000 employees.

Instead of creating separate cloud accounts, Microsoft Entra Connect synchronizes the existing identities to Microsoft Entra ID.

Employees continue using their corporate usernames and passwords to access both internal resources and Microsoft 365 services.

---

## Best Practices

- Synchronize only the required objects.
- Choose the authentication method that matches business requirements.
- Monitor synchronization regularly.
- Keep synchronization services updated.
- Protect privileged accounts with Multi-Factor Authentication (MFA).
- Plan hybrid identity deployments carefully before migration.

---

## Common Pitfalls

- Synchronizing unnecessary objects.
- Choosing an authentication method without evaluating business requirements.
- Ignoring synchronization errors.
- Forgetting to monitor Microsoft Entra Connect.
- Assuming synchronization provides authorization automatically.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Hybrid Identity
> - Microsoft Entra Connect
> - Password Hash Synchronization (PHS)
> - Pass-through Authentication (PTA)
> - Federation
> - Identity synchronization

---

## Key Takeaways

- Hybrid Identity integrates on-premises Active Directory with Microsoft Entra ID.
- Users can access cloud and on-premises resources using the same identity.
- Synchronization keeps identity information consistent.
- Multiple authentication methods support different business requirements.
- Hybrid Identity enables gradual cloud adoption.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Hybrid identity documentation](https://learn.microsoft.com/entra/identity/hybrid/) | Hybrid Identity overview |
| [Choose the right authentication method](https://learn.microsoft.com/entra/identity/hybrid/connect/choose-ad-authn) | Compare PHS, PTA, and Federation |
| [Microsoft Entra Connect overview](https://learn.microsoft.com/entra/identity/hybrid/connect/whatis-azure-ad-connect) | Identity synchronization |
| [Cloud Sync overview](https://learn.microsoft.com/entra/identity/hybrid/cloud-sync/what-is-cloud-sync) | Cloud Sync overview |
| [Microsoft Learn – Hybrid identity](https://learn.microsoft.com/training/modules/plan-design-identity-solution/) | Microsoft Learn module |
