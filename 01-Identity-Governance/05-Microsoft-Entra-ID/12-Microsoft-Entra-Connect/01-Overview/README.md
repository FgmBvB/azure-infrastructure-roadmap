# Microsoft Entra Connect Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra Connect, explains its architecture, components, and role in Hybrid Identity deployments.

---

## Microsoft Entra Connect Architecture

```text
        On-Premises
     Active Directory
             │
             ▼
   Microsoft Entra Connect
             │
             ▼
 Synchronization Engine
             │
             ▼
    Microsoft Entra ID
             │
             ▼
 Microsoft 365 • Azure • SaaS
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra Connect synchronizes identities between Active Directory and Microsoft Entra ID.
> - It supports multiple hybrid authentication methods.
> - It enables organizations to maintain a single identity across on-premises and cloud environments.
> - It synchronizes only selected directory objects.
> - Synchronization and authentication are separate processes.

---

## Overview

Microsoft Entra Connect is Microsoft's synchronization solution for Hybrid Identity environments.

It connects on-premises Active Directory Domain Services (AD DS) with Microsoft Entra ID, allowing users to maintain a single identity while accessing both on-premises and cloud resources.

Microsoft Entra Connect is commonly deployed during cloud migration projects or in organizations that operate hybrid infrastructures.

---

## Main Components

Microsoft Entra Connect includes several components that work together.

| Component | Purpose |
|----------|---------|
| **Synchronization Engine** | Synchronizes directory objects between Active Directory and Microsoft Entra ID. |
| **Microsoft Entra Connect Wizard** | Installs and configures synchronization. |
| **Authentication Components** | Configure Password Hash Synchronization (PHS), Pass-through Authentication (PTA), Federation, and Seamless SSO. |
| **Synchronization Scheduler** | Runs synchronization cycles automatically. |

---

## Supported Authentication Methods

Microsoft Entra Connect supports several authentication models.

| Authentication Method | Description |
|-----------------------|-------------|
| **Password Hash Synchronization (PHS)** | Cloud authentication using synchronized password hashes. |
| **Pass-through Authentication (PTA)** | Password validation remains on-premises. |
| **Federation** | Authentication is delegated to a federation service such as AD FS. |

The selected authentication method determines where user passwords are validated.

---

## What Can Be Synchronized?

Microsoft Entra Connect can synchronize:

- Users
- Security Groups
- Contacts
- Devices (when configured)
- Selected directory attributes

Administrators control which objects are synchronized through filtering options.

---

## Synchronization Workflow

```text
User Created
       │
       ▼
Active Directory
       │
       ▼
Microsoft Entra Connect
       │
       ▼
Synchronization Engine
       │
       ▼
Microsoft Entra ID
       │
       ▼
Microsoft 365 / Azure
```

---

## Synchronization Features

Microsoft Entra Connect supports additional Hybrid Identity capabilities, including:

- Password Hash Synchronization
- Pass-through Authentication
- Seamless Single Sign-On
- Password Writeback
- Group Writeback (supported scenarios)
- Device Writeback (supported hybrid scenarios)

Feature availability depends on licensing and deployment configuration.

---

## Typical Deployment

A standard deployment consists of:

- One Active Directory forest.
- One Microsoft Entra tenant.
- One Microsoft Entra Connect server.
- Internet connectivity to Microsoft Entra ID.

Larger organizations may implement more advanced synchronization architectures depending on business requirements.

---

## Enterprise Scenario

A company with 3,000 Active Directory users migrates to Microsoft 365.

Microsoft Entra Connect synchronizes users, groups, and selected attributes to Microsoft Entra ID.

Employees continue using their existing Active Directory accounts while accessing Exchange Online, Microsoft Teams, SharePoint Online, and Azure resources with the same identity.

---

## Best Practices

- Deploy Microsoft Entra Connect on a dedicated server.
- Synchronize only required objects.
- Choose the appropriate authentication method.
- Monitor synchronization health regularly.
- Keep Microsoft Entra Connect updated.
- Protect the synchronization server as a privileged system.

---

## Common Pitfalls

- Synchronizing unnecessary objects.
- Choosing the wrong authentication method.
- Ignoring synchronization failures.
- Modifying synchronized objects directly in Microsoft Entra ID.
- Forgetting to monitor synchronization health.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra Connect architecture
> - Synchronization engine
> - Supported authentication methods
> - Synchronization workflow
> - Hybrid Identity
> - Core synchronization features

---

## Key Takeaways

- Microsoft Entra Connect synchronizes identities between Active Directory and Microsoft Entra ID.
- It enables Hybrid Identity with a single user identity across environments.
- Authentication and synchronization are independent processes.
- Multiple authentication methods are supported.
- Microsoft Entra Connect is the foundation of most Hybrid Identity deployments.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra Connect overview](https://learn.microsoft.com/entra/identity/hybrid/connect/whatis-azure-ad-connect) | Microsoft Entra Connect overview |
| [Synchronization features](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-sync-whatis) | Synchronization engine and features |
| [Choose the right authentication method](https://learn.microsoft.com/entra/identity/hybrid/connect/choose-ad-authn) | Authentication methods |
| [Microsoft Entra Connect architecture](https://learn.microsoft.com/entra/identity/hybrid/connect/plan-connect-topologies) | Supported deployment topologies |
| [Microsoft Learn – Plan a hybrid identity solution](https://learn.microsoft.com/training/modules/plan-design-identity-solution/) | Microsoft Learn module |
