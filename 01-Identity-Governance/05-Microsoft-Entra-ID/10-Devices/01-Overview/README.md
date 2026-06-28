# Devices Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra device identities, explains how devices are registered, and describes their role in authentication, Conditional Access, and modern identity management.

---

## Device Identity Model

```text
          User Device
   (PC, Laptop, Mobile)
              │
              ▼
     Microsoft Entra ID
      Device Registration
              │
              ▼
        Device Identity
              │
              ▼
 Authentication & Trust
              │
              ▼
Conditional Access
      Device-Based Policies
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra ID can manage device identities.
> - Devices become trusted after registration or joining.
> - Device identities support Conditional Access decisions.
> - Authentication evaluates both the user and the device.
> - Device management is independent from device identity.

---

## Overview

Microsoft Entra ID allows organizations to register and manage device identities in addition to user and application identities.

A registered device receives its own identity within Microsoft Entra ID, allowing Azure services to evaluate both the user and the device during authentication.

This improves security by enabling device-based access controls and compliance policies.

---

## Why Device Identities

Device identities provide several security benefits.

Organizations can:

- Identify trusted devices.
- Apply Conditional Access policies.
- Require compliant devices.
- Enable Single Sign-On (SSO).
- Improve security for remote work.

Without a device identity, Microsoft Entra ID evaluates only the user's identity.

---

## Device Identity Types

Microsoft Entra ID supports multiple device registration models.

| Device Type | Description |
|-------------|-------------|
| **Microsoft Entra Registered** | Personal or BYOD devices registered to Microsoft Entra ID. |
| **Microsoft Entra Joined** | Organization-owned devices joined directly to Microsoft Entra ID. |
| **Microsoft Entra Hybrid Joined** | Devices joined to on-premises Active Directory and synchronized with Microsoft Entra ID. |

Each model provides a different level of trust and management.

---

## Authentication

During authentication, Microsoft Entra ID evaluates multiple signals.

Typical signals include:

- User identity.
- Device identity.
- Device state.
- Authentication method.
- Conditional Access policies.
- Risk signals.

Authentication decisions are based on both the user and the device whenever device identities are available.

---

## Device Trust

Device identities help establish trust between users, devices, and Azure resources.

```text
User
 │
 ▼
Authenticate
 │
 ▼
Microsoft Entra ID
 │
 ├──────────────┐
 ▼              ▼
User Identity  Device Identity
 │              │
 └──────┬───────┘
        ▼
 Conditional Access
        │
        ▼
 Access Decision
```

Trusted devices can satisfy Conditional Access requirements that unregistered devices cannot.

---

## Device Management

Device identity and device management are separate concepts.

- **Microsoft Entra ID** provides the device identity.
- **Microsoft Intune** manages device configuration and compliance.
- **Conditional Access** combines identity and compliance information to make access decisions.

A device can exist in Microsoft Entra ID without being managed by Intune.

---

## Enterprise Scenario

A company issues Windows laptops to all employees.

Each laptop is Microsoft Entra Joined and managed through Microsoft Intune.

When an employee signs in to Microsoft 365, Microsoft Entra ID evaluates both the user's identity and the trusted device before applying Conditional Access policies.

Access is granted only if both identities satisfy the organization's security requirements.

---

## Best Practices

- Register all corporate devices.
- Use Microsoft Entra Joined devices for organization-owned equipment.
- Protect access with Conditional Access.
- Monitor device identities regularly.
- Remove inactive or obsolete devices.
- Integrate device identities with Microsoft Intune where appropriate.

---

## Common Pitfalls

- Confusing device identity with device management.
- Assuming device registration automatically grants resource access.
- Leaving obsolete devices registered.
- Ignoring device state in Conditional Access policies.
- Managing devices without reviewing compliance status.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Device identities
> - Microsoft Entra Registered devices
> - Microsoft Entra Joined devices
> - Microsoft Entra Hybrid Joined devices
> - Device authentication
> - Conditional Access integration

---

## Key Takeaways

- Microsoft Entra ID manages identities for devices as well as users and applications.
- Device identities strengthen authentication and access control.
- Conditional Access can evaluate both user and device identities.
- Device identity is independent from device management.
- Different registration models support different organizational scenarios.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Overview of device identity in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/devices/overview) | Device identity overview |
| [What is a device identity?](https://learn.microsoft.com/entra/identity/devices/device-identities) | Device identity concepts |
| [Microsoft Entra joined devices](https://learn.microsoft.com/entra/identity/devices/concept-directory-join) | Microsoft Entra Joined devices |
| [Hybrid Microsoft Entra joined devices](https://learn.microsoft.com/entra/identity/devices/concept-hybrid-join) | Hybrid device identity |
| [Microsoft Learn – Secure identities with Microsoft Entra ID](https://learn.microsoft.com/training/modules/secure-identities-with-aad/) | Microsoft Learn module |
