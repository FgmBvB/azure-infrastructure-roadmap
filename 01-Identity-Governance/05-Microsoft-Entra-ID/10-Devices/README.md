# Microsoft Entra Devices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra device identities, device registration, management, compliance, and security integration with Microsoft Intune and Conditional Access.

---

## Overview

Microsoft Entra Devices enable organizations to register, join, and manage corporate and personal devices within Microsoft Entra ID.

Device identities strengthen security by allowing administrators to enforce compliance policies, enable Single Sign-On (SSO), integrate with Microsoft Intune, and control access through Conditional Access.

Proper device management is an essential component of Microsoft's Zero Trust security model.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Microsoft Entra device identities.
- Differentiate between Registered, Joined, and Hybrid Joined devices.
- Configure device registration.
- Manage devices using Microsoft Intune.
- Understand device compliance.
- Integrate devices with Conditional Access.
- Apply Microsoft security recommendations.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Device identities, registration models, and architecture. |
| **02 - Device Registration** | Microsoft Entra Registered, Joined, and Hybrid Joined devices. |
| **03 - Device Management** | Microsoft Intune integration, compliance, enrollment, and lifecycle management. |
| **04 - Device Identity** | Device objects, identifiers, BitLocker recovery keys, and identity attributes. |
| **05 - Best Practices** | Security recommendations, governance, and operational guidance. |

---

## Architecture

```text
                 Device
                    │
                    ▼
        Microsoft Entra ID
                    │
      Device Registration
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
 Registered     Joined     Hybrid Joined
        │           │           │
        └───────────┼───────────┘
                    ▼
          Microsoft Intune
                    │
                    ▼
         Compliance Evaluation
                    │
                    ▼
        Conditional Access
```

---

## Skills Covered

This section includes:

- Microsoft Entra Devices
- Device Registration
- Microsoft Entra Joined
- Microsoft Entra Registered
- Hybrid Microsoft Entra Joined
- Device Identity
- Primary Refresh Token (PRT)
- Microsoft Intune
- Device Compliance
- Conditional Access
- BitLocker Recovery Keys
- Device Lifecycle
- Zero Trust

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure device registration.
- Manage Microsoft Entra devices.
- Integrate Microsoft Intune.
- Configure compliance policies.
- Secure device access with Conditional Access.
- Troubleshoot device identity issues.

---

## Key Takeaways

- Microsoft Entra ID treats devices as identity objects.
- Device identities improve authentication and authorization decisions.
- Microsoft Intune manages device configuration and compliance.
- Conditional Access uses device identity and compliance to secure access.
- Device management is a key component of Microsoft's Zero Trust architecture.
