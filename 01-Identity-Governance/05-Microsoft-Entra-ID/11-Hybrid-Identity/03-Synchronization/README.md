# Identity Synchronization

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how identities are synchronized between on-premises Active Directory and Microsoft Entra ID, covering Microsoft Entra Connect and Microsoft Entra Cloud Sync.

---

## Synchronization Architecture

```text
      On-Premises
   Active Directory
          │
          │
 ┌────────┴─────────┐
 │                  │
 ▼                  ▼
Microsoft      Microsoft
Entra Connect  Entra Cloud Sync
 │                  │
 └────────┬─────────┘
          ▼
 Microsoft Entra ID
          │
          ▼
 Microsoft 365
 Azure
 SaaS Applications
```

---

> [!TIP]
> **Key Concepts**
>
> - Identity synchronization keeps on-premises and cloud identities consistent.
> - Microsoft Entra Connect is the traditional synchronization solution.
> - Microsoft Entra Cloud Sync is the lightweight cloud-based alternative.
> - Synchronization does not authenticate users by itself.
> - Only selected objects are synchronized.

---

## Overview

Identity synchronization allows organizations to maintain a single identity for users across both on-premises Active Directory and Microsoft Entra ID.

Synchronization replicates directory information while preserving a unified identity experience across cloud and on-premises services.

---

## Microsoft Entra Connect

Microsoft Entra Connect is Microsoft's primary synchronization tool for hybrid identity deployments.

It runs on a Windows Server joined to the Active Directory domain and synchronizes directory objects to Microsoft Entra ID.

Typical synchronized objects include:

- Users
- Groups
- Contacts
- Devices (when configured)

Microsoft Entra Connect also supports hybrid authentication features such as:

- Password Hash Synchronization (PHS)
- Pass-through Authentication (PTA)
- Seamless Single Sign-On
- Federation integration

---

## Microsoft Entra Cloud Sync

Microsoft Entra Cloud Sync is a lightweight synchronization solution that uses provisioning agents instead of a full synchronization server.

Compared to Microsoft Entra Connect:

- Simpler deployment
- Lightweight provisioning agents
- Cloud-managed configuration
- Supports multiple Active Directory forests
- Reduced infrastructure requirements

Cloud Sync is suitable for many organizations but currently supports fewer synchronization features than Microsoft Entra Connect.

---

## Synchronization Process

```text
Active Directory
        │
        ▼
Object Change
        │
        ▼
Synchronization Engine
        │
        ▼
Microsoft Entra ID
        │
        ▼
Cloud Applications
```

Synchronization propagates directory changes from Active Directory to Microsoft Entra ID on a scheduled basis.

---

## Synchronized Objects

Organizations decide which objects are synchronized.

Common object types include:

- Users
- Security Groups
- Microsoft 365 Groups (where applicable)
- Contacts
- Devices

Synchronizing only the required objects improves performance and reduces administrative complexity.

---

## Filtering

Microsoft Entra Connect supports multiple filtering methods.

| Filtering Method | Purpose |
|------------------|---------|
| **Domain Filtering** | Synchronize selected Active Directory domains. |
| **Organizational Unit (OU) Filtering** | Synchronize only selected OUs. |
| **Attribute Filtering** | Synchronize objects based on attribute values. |
| **Group-Based Filtering** | Limit synchronization to members of selected groups (Cloud Sync). |

Filtering helps reduce unnecessary synchronization.

---

## Attribute Synchronization

Microsoft Entra Connect synchronizes selected Active Directory attributes to Microsoft Entra ID.

Examples include:

- User Principal Name (UPN)
- Display Name
- Email Address
- Department
- Job Title
- Telephone Number

Attribute synchronization helps maintain consistent user identities across environments.

---

## Writeback Features

Some hybrid identity features allow changes made in Microsoft Entra ID to be written back to on-premises Active Directory.

Examples include:

- Password Writeback
- Group Writeback (supported scenarios)
- Device Writeback (legacy and specific hybrid scenarios)

Writeback availability depends on the synchronization solution and licensing.

---

## Enterprise Scenario

A company maintains an on-premises Active Directory while migrating users to Microsoft 365.

Microsoft Entra Connect synchronizes users, groups, and selected organizational units to Microsoft Entra ID.

Employees continue using the same corporate identities across both environments while administrators manage only one identity source.

---

## Best Practices

- Synchronize only required objects.
- Use OU filtering to reduce unnecessary synchronization.
- Monitor synchronization health regularly.
- Keep Microsoft Entra Connect updated.
- Review synchronization errors promptly.
- Document filtering and synchronization rules.

---

## Common Pitfalls

- Synchronizing unnecessary objects.
- Forgetting to include required Organizational Units.
- Ignoring synchronization failures.
- Modifying synchronized cloud objects directly.
- Confusing synchronization with authentication.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra Connect
> - Microsoft Entra Cloud Sync
> - Synchronization process
> - Filtering methods
> - Attribute synchronization
> - Writeback features

---

## Key Takeaways

- Identity synchronization keeps Active Directory and Microsoft Entra ID consistent.
- Microsoft Entra Connect provides the most complete hybrid synchronization capabilities.
- Microsoft Entra Cloud Sync offers a lighter cloud-managed alternative.
- Filtering helps synchronize only the required objects.
- Synchronization and authentication are separate processes.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra Connect overview](https://learn.microsoft.com/entra/identity/hybrid/connect/whatis-azure-ad-connect) | Microsoft Entra Connect overview |
| [Microsoft Entra Cloud Sync overview](https://learn.microsoft.com/entra/identity/hybrid/cloud-sync/what-is-cloud-sync) | Cloud Sync overview |
| [Synchronization features](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-sync-whatis) | Identity synchronization concepts |
| [Filtering users and groups](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-sync-configure-filtering) | Synchronization filtering |
| [Microsoft Learn – Hybrid identity](https://learn.microsoft.com/training/modules/plan-design-identity-solution/) | Microsoft Learn module |
