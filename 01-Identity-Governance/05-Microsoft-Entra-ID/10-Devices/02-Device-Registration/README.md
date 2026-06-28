# Device Registration

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how devices are registered in Microsoft Entra ID, the available registration models, and their role in authentication and access management.

---

## Registration Process

```text
      Device
        │
        ▼
 Registration / Join
        │
        ▼
 Microsoft Entra ID
        │
        ▼
 Device Object Created
        │
        ▼
 Device Identity
        │
        ▼
 Authentication &
 Conditional Access
```

---

> [!TIP]
> **Key Concepts**
>
> - Device registration creates a device identity in Microsoft Entra ID.
> - Registration establishes trust between the device and the organization.
> - Different registration methods support different ownership models.
> - Registered devices can participate in Conditional Access decisions.
> - Device registration does not automatically mean device management.

---

## Overview

Device registration creates a trusted identity for a device inside Microsoft Entra ID.

Once registered or joined, the device receives its own identity that can be evaluated during authentication.

This enables organizations to apply security controls based on both the user and the device.

---

## Registration Models

Microsoft Entra ID supports three primary registration models.

| Registration Model | Typical Scenario |
|--------------------|------------------|
| **Microsoft Entra Registered** | Personal (BYOD) devices |
| **Microsoft Entra Joined** | Organization-owned cloud-first devices |
| **Microsoft Entra Hybrid Joined** | Devices joined to on-premises Active Directory and synchronized with Microsoft Entra ID |

Each model provides a different level of trust and administrative control.

---

## Microsoft Entra Registered

Microsoft Entra Registered devices are typically personal devices owned by users.

Characteristics include:

- Bring Your Own Device (BYOD).
- User registration.
- Personal ownership.
- Limited organizational control.
- Supports Single Sign-On (SSO).

These devices are commonly used to access Microsoft 365 and other cloud applications.

---

## Microsoft Entra Joined

Microsoft Entra Joined devices are owned and managed by the organization.

Characteristics include:

- Corporate ownership.
- Joined directly to Microsoft Entra ID.
- No dependency on on-premises Active Directory.
- Supports centralized identity management.
- Frequently managed with Microsoft Intune.

This model is recommended for cloud-native organizations.

---

## Microsoft Entra Hybrid Joined

Hybrid Joined devices combine on-premises Active Directory with Microsoft Entra ID.

Characteristics include:

- Joined to Active Directory.
- Automatically registered with Microsoft Entra ID.
- Supports hybrid environments.
- Enables cloud authentication while maintaining on-premises domain membership.

Hybrid Join is commonly used during cloud migration.

---

## Device Registration Flow

```text
Device
   │
   ▼
Registration / Join
   │
   ▼
Microsoft Entra ID
   │
   ▼
Device Object
   │
   ▼
Authentication
   │
   ▼
Conditional Access
```

---

## Device Object

When registration completes successfully, Microsoft Entra ID creates a **Device Object**.

The Device Object contains information such as:

- Device ID
- Display name
- Operating system
- Ownership
- Join type
- Registration state
- Trust relationship

This information is used during authentication and Conditional Access evaluation.

---

## Registration vs Management

Device registration and device management are independent processes.

| Device Registration | Device Management |
|---------------------|-------------------|
| Creates a device identity | Configures the device |
| Microsoft Entra ID | Microsoft Intune (typically) |
| Supports authentication | Applies configuration and compliance policies |
| Required for device identity | Optional depending on organizational requirements |

A device can be registered without being managed.

---

## Enterprise Scenario

A company allows employees to use personal laptops to access Microsoft 365.

Employees register their devices with Microsoft Entra ID.

The devices receive unique identities, allowing Conditional Access policies to evaluate both the user and the registered device before granting access.

---

## Best Practices

- Use Microsoft Entra Joined for corporate-owned devices.
- Use Microsoft Entra Registered for BYOD scenarios.
- Use Hybrid Join during hybrid migrations.
- Regularly review registered devices.
- Remove obsolete or inactive devices.
- Integrate with Microsoft Intune for compliance management.

---

## Common Pitfalls

- Confusing registration with device management.
- Registering corporate devices as BYOD.
- Leaving inactive devices registered.
- Ignoring device lifecycle management.
- Assuming registration automatically grants resource access.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Device registration
> - Microsoft Entra Registered devices
> - Microsoft Entra Joined devices
> - Microsoft Entra Hybrid Joined devices
> - Device Objects
> - Registration versus management

---

## Key Takeaways

- Device registration creates a trusted identity in Microsoft Entra ID.
- Microsoft Entra supports Registered, Joined, and Hybrid Joined devices.
- Device registration strengthens authentication and Conditional Access.
- Registration is different from device management.
- Device identities improve organizational security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Overview of device identity in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/devices/overview) | Device identity overview |
| [What is a device identity?](https://learn.microsoft.com/entra/identity/devices/device-identities) | Device identity concepts |
| [Microsoft Entra joined devices](https://learn.microsoft.com/entra/identity/devices/concept-directory-join) | Microsoft Entra Joined devices |
| [Hybrid Microsoft Entra joined devices](https://learn.microsoft.com/entra/identity/devices/concept-hybrid-join) | Hybrid Microsoft Entra Joined devices |
| [Microsoft Learn – Secure identities with Microsoft Entra ID](https://learn.microsoft.com/training/modules/secure-identities-with-aad/) | Microsoft Learn module |
