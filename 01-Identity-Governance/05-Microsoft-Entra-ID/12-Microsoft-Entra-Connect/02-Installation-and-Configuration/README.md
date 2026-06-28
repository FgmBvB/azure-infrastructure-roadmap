# Microsoft Entra Connect Installation and Configuration

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra Connect is installed and configured to synchronize identities between Active Directory and Microsoft Entra ID.

---

## Deployment Process

```text
Prepare Environment
         │
         ▼
Install Microsoft Entra Connect
         │
         ▼
Connect Active Directory
         │
         ▼
Connect Microsoft Entra ID
         │
         ▼
Choose Authentication Method
         │
         ▼
Configure Synchronization
         │
         ▼
Run Initial Synchronization
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra Connect is installed on a domain-joined Windows Server.
> - Installation can use Express or Custom settings.
> - Authentication and synchronization are configured during installation.
> - Synchronization scope can be customized.
> - Initial synchronization validates the deployment.

---

## Overview

Microsoft Entra Connect provides a guided installation wizard that connects an on-premises Active Directory environment with Microsoft Entra ID.

During installation, administrators configure synchronization, authentication, filtering, and optional hybrid identity features.

---

## Prerequisites

Before installing Microsoft Entra Connect:

- Active Directory Domain Services (AD DS) must be healthy.
- A supported Windows Server must be available.
- Internet connectivity to Microsoft Entra ID is required.
- Enterprise Administrator credentials for Active Directory.
- Global Administrator credentials for Microsoft Entra ID.

The synchronization server should be dedicated to Microsoft Entra Connect whenever possible.

---

## Installation Options

Microsoft Entra Connect offers two installation modes.

| Mode | Description |
|------|-------------|
| **Express Settings** | Recommended for simple environments using Password Hash Synchronization (PHS) with default synchronization settings. |
| **Custom Settings** | Allows administrators to configure authentication methods, synchronization filtering, sourceAnchor, writeback features, and advanced options. |

Most production environments use **Custom Settings**.

---

## Connect to Active Directory

The installation wizard connects to Active Directory using Enterprise Administrator credentials.

Microsoft Entra Connect automatically discovers:

- Domains
- Forests
- Organizational Units (OUs)
- Directory schema
- User and group objects

These objects become available for synchronization.

---

## Connect to Microsoft Entra ID

Microsoft Entra Connect connects to Microsoft Entra ID using a Global Administrator account.

The wizard registers the synchronization service and prepares the Microsoft Entra tenant for Hybrid Identity.

---

## Select the Authentication Method

During installation, administrators choose the authentication model.

Available options include:

- Password Hash Synchronization (PHS)
- Pass-through Authentication (PTA)
- Federation
- Seamless Single Sign-On (optional with supported authentication methods)

The selected authentication method determines how users authenticate to cloud services.

---

## Configure Synchronization

Administrators define which objects are synchronized.

Configuration options include:

- Organizational Unit (OU) filtering
- Domain filtering
- Attribute filtering
- Optional writeback features

Synchronizing only required objects improves performance and simplifies administration.

---

## Source Anchor

Microsoft Entra Connect associates each Active Directory object with its corresponding Microsoft Entra ID object using an immutable identifier called the **sourceAnchor**.

Modern deployments typically use **ms-DS-ConsistencyGuid**, while older environments may use the Active Directory **objectGUID**.

The sourceAnchor is synchronized to Microsoft Entra ID as the **ImmutableId**, ensuring that synchronized identities remain linked throughout their lifecycle.

---

## Seamless Single Sign-On

When enabled, **Seamless Single Sign-On (Seamless SSO)** allows domain-joined users to authenticate automatically to supported Microsoft cloud services.

Microsoft Entra Connect creates a computer account named **AZUREADSSOACC** in Active Directory to support this functionality.

Seamless SSO is commonly used together with Password Hash Synchronization or Pass-through Authentication.

---

## Initial Synchronization

After configuration is complete, Microsoft Entra Connect performs the initial synchronization.

```text
Active Directory
        │
        ▼
Initial Synchronization
        │
        ▼
Microsoft Entra ID
        │
        ▼
Users
Groups
Devices
```

The initial synchronization creates the corresponding cloud identities.

---

## Enterprise Scenario

A company migrates to Microsoft 365 while maintaining its on-premises Active Directory.

Administrators install Microsoft Entra Connect using **Custom Settings**, enable Password Hash Synchronization and Seamless SSO, configure OU filtering, and synchronize only corporate users and security groups.

Employees continue using their existing Active Directory credentials to access both on-premises and cloud resources.

---

## Best Practices

- Deploy Microsoft Entra Connect on a dedicated server.
- Prefer **Custom Settings** for production deployments.
- Synchronize only required Organizational Units.
- Validate Active Directory health before installation.
- Use Password Hash Synchronization unless another authentication method is required.
- Test synchronization before onboarding production users.

---

## Common Pitfalls

- Using Express Settings in complex environments.
- Synchronizing unnecessary objects.
- Selecting the wrong authentication method.
- Forgetting to configure synchronization filtering.
- Ignoring Active Directory health before installation.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Installation prerequisites
> - Express vs Custom installation
> - Authentication method selection
> - Synchronization configuration
> - SourceAnchor
> - Seamless Single Sign-On

---

## Key Takeaways

- Microsoft Entra Connect connects Active Directory with Microsoft Entra ID.
- Installation can use Express or Custom configuration.
- Authentication methods are selected during deployment.
- Synchronization scope should include only required objects.
- Proper planning simplifies Hybrid Identity deployments.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Install Microsoft Entra Connect](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-install-express) | Installation guide |
| [Custom installation](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-install-custom) | Advanced deployment options |
| [Choose the right authentication method](https://learn.microsoft.com/entra/identity/hybrid/connect/choose-ad-authn) | Authentication methods |
| [SourceAnchor and ImmutableId](https://learn.microsoft.com/entra/identity/hybrid/connect/plan-connect-design-concepts) | Identity matching concepts |
| [Microsoft Learn – Plan a hybrid identity solution](https://learn.microsoft.com/training/modules/plan-design-identity-solution/) | Microsoft Learn module |
