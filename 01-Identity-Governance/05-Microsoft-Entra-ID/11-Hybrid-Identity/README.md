# Hybrid Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Hybrid Identity, including hybrid authentication methods, identity synchronization, and best practices for integrating on-premises Active Directory with Microsoft Entra ID.

---

## Overview

Hybrid Identity enables organizations to integrate their on-premises Active Directory with Microsoft Entra ID.

This integration allows users to access both on-premises and cloud resources using the same identity while maintaining centralized identity management.

Hybrid Identity is a key technology for organizations migrating workloads to Microsoft Azure and Microsoft 365.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Hybrid Identity architecture.
- Compare hybrid authentication methods.
- Understand identity synchronization.
- Deploy Microsoft Entra Connect and Cloud Sync solutions.
- Troubleshoot synchronization issues.
- Apply Microsoft best practices for hybrid identity.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Hybrid Identity concepts, architecture, and identity integration. |
| **02 - Authentication Methods** | Password Hash Synchronization (PHS), Pass-through Authentication (PTA), Federation, and Seamless SSO. |
| **03 - Synchronization** | Microsoft Entra Connect, Cloud Sync, synchronization cycles, sourceAnchor, and identity synchronization. |
| **04 - Best Practices** | Security recommendations, high availability, monitoring, and operational guidance. |

---

## Architecture

```text
           On-Premises
        Active Directory
               │
               ▼
   Microsoft Entra Connect
      or Cloud Sync Agent
               │
               ▼
      Microsoft Entra ID
               │
       ┌───────┴────────┐
       │                │
       ▼                ▼
 Microsoft 365      Azure Services
```

---

## Skills Covered

This section includes:

- Hybrid Identity
- Active Directory
- Microsoft Entra ID
- Password Hash Synchronization (PHS)
- Pass-through Authentication (PTA)
- Federation
- Seamless Single Sign-On (SSO)
- Microsoft Entra Connect
- Microsoft Entra Cloud Sync
- Identity Synchronization
- sourceAnchor (Immutable ID)
- Hybrid Authentication
- Synchronization Scheduler
- Identity Lifecycle

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Hybrid Identity.
- Choose the appropriate authentication method.
- Deploy Microsoft Entra Connect.
- Configure identity synchronization.
- Troubleshoot synchronization issues.
- Maintain hybrid identity environments.

---

## Key Takeaways

- Hybrid Identity integrates on-premises Active Directory with Microsoft Entra ID.
- Multiple authentication methods support different business requirements.
- Microsoft Entra Connect and Cloud Sync synchronize identities between environments.
- Proper synchronization is essential for authentication and identity consistency.
- Hybrid Identity enables a gradual migration from on-premises infrastructure to the cloud.
