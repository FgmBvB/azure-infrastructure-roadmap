# Microsoft Entra Connect

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra Connect, including installation, synchronization architecture, maintenance, and best practices for hybrid identity deployments.

---

## Overview

Microsoft Entra Connect is Microsoft's identity synchronization solution for hybrid environments.

It connects on-premises Active Directory with Microsoft Entra ID, synchronizing users, groups, devices, and selected attributes while supporting hybrid authentication methods such as Password Hash Synchronization (PHS), Pass-through Authentication (PTA), and Federation.

Microsoft Entra Connect is a core component of Hybrid Identity deployments.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Microsoft Entra Connect architecture.
- Install and configure Microsoft Entra Connect.
- Configure identity synchronization.
- Understand synchronization cycles and maintenance.
- Deploy staging servers for high availability.
- Troubleshoot synchronization issues.
- Apply Microsoft best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Microsoft Entra Connect architecture, components, and synchronization concepts. |
| **02 - Installation and Configuration** | Installation, authentication methods, staging mode, filtering, and configuration options. |
| **03 - Synchronization and Maintenance** | Synchronization engine, scheduler, metaverse, maintenance tasks, monitoring, and troubleshooting. |

---

## Architecture

```text
      On-Premises
    Active Directory
            │
            ▼
 Microsoft Entra Connect
            │
    Synchronization Engine
            │
            ▼
    Microsoft Entra ID
            │
     Microsoft 365
     Azure Services
```

---

## Skills Covered

This section includes:

- Microsoft Entra Connect
- Hybrid Identity
- Identity Synchronization
- Password Hash Synchronization (PHS)
- Pass-through Authentication (PTA)
- Federation
- Staging Mode
- Synchronization Scheduler
- Metaverse
- Connector Space
- Attribute Filtering
- OU Filtering
- Synchronization Rules
- Microsoft Entra Connect Health
- Troubleshooting

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Deploy Microsoft Entra Connect.
- Configure hybrid identity.
- Configure synchronization.
- Manage synchronization schedules.
- Troubleshoot synchronization failures.
- Maintain hybrid identity infrastructure.

---

## Key Takeaways

- Microsoft Entra Connect synchronizes identities between Active Directory and Microsoft Entra ID.
- It supports multiple hybrid authentication methods.
- Staging Mode enables high availability and safe configuration testing.
- The synchronization engine maintains identity consistency across environments.
- Regular monitoring and maintenance are essential for reliable hybrid identity operations.
