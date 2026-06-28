# Device Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID represents devices as identities and how those identities are used during authentication, Conditional Access, and resource access decisions.

---

## Device Identity Lifecycle

```text
      Device
         │
         ▼
 Register / Join
         │
         ▼
 Device Object
 (Microsoft Entra ID)
         │
         ▼
 Device Identity
         │
         ▼
 Authentication
         │
         ▼
 Conditional Access
         │
         ▼
 Access Decision
```

---

> [!TIP]
> **Key Concepts**
>
> - Every registered or joined device receives a unique identity in Microsoft Entra ID.
> - Devices are represented by Device Objects.
> - Device identities participate in authentication and Conditional Access.
> - Device identity is separate from device management.
> - Device identities can be enabled, disabled, or deleted independently.

---

## Overview

Microsoft Entra ID treats registered and joined devices as security principals.

Each device is represented by a **Device Object**, allowing Microsoft Entra ID to identify, authenticate, and evaluate the device during access requests.

Device identities improve security by allowing organizations to evaluate both the user and the device before granting access.

---

## Device Identifiers

Each device registered in Microsoft Entra ID has multiple identifiers.

| Identifier | Purpose |
|------------|---------|
| **Device ID** | Uniquely identifies the physical or virtual device and is shared with the operating system. |
| **Object ID** | Identifies the Device Object stored in Microsoft Entra ID and is used by directory services and Microsoft Graph. |

Although both values are GUIDs, they serve different administrative purposes and should not be confused.

---

## Device Object

Every registered device has a corresponding **Device Object** stored in Microsoft Entra ID.

Typical properties include:

- Device ID
- Display name
- Operating system
- Join type
- Trust type
- Registration date
- Ownership
- Enabled state

This object represents the device throughout its lifecycle.

---

## BitLocker Recovery Keys

For supported Microsoft Entra Joined and Hybrid Joined Windows devices, BitLocker recovery information can be backed up to Microsoft Entra ID.

Authorized administrators can retrieve BitLocker recovery keys from the device's properties in the Microsoft Entra admin center when recovery is required.

This simplifies recovery operations while maintaining centralized management.

---

## Device Authentication

When a user signs in from a registered device, Microsoft Entra ID evaluates:

- User identity
- Device identity
- Authentication method
- Device state
- Conditional Access policies

Both the user and the device may influence the final authentication result.

---

## Device States

A device identity can exist in different administrative states.

| State | Description |
|--------|-------------|
| **Enabled** | The device can authenticate normally. |
| **Disabled** | Authentication from the device is blocked. |
| **Deleted** | The device identity has been removed from Microsoft Entra ID. |

Disabling a device is often preferred over immediate deletion during investigations.

---

## Device Activity

Microsoft Entra ID records the approximate last sign-in time for each device.

Administrators can use this information to identify inactive devices and support lifecycle management processes.

Reviewing device activity helps organizations remove obsolete device identities and reduce unnecessary security exposure.

---

## Device Trust

Microsoft Entra ID establishes trust based on how the device was registered.

| Trust Level | Registration Method |
|-------------|---------------------|
| Microsoft Entra Registered | Personal (BYOD) devices |
| Microsoft Entra Joined | Organization-owned devices |
| Microsoft Entra Hybrid Joined | Hybrid Active Directory environments |

The trust relationship influences Conditional Access decisions.

---

## Device Identity and Conditional Access

```text
User
 │
 ▼
Authentication
 │
 ├──────────────┐
 ▼              ▼
User Identity Device Identity
 │              │
 └──────┬───────┘
        ▼
 Conditional Access
        │
        ▼
 Access Granted / Denied
```

Conditional Access policies can require a trusted or compliant device before access is granted.

---

## Device Identity vs Device Management

| Device Identity | Device Management |
|-----------------|-------------------|
| Microsoft Entra ID | Microsoft Intune |
| Creates the device identity | Configures the device |
| Used during authentication | Used to manage security and compliance |
| Supports Conditional Access | Applies configuration and compliance policies |

Although closely integrated, these are separate services.

---

## Enterprise Scenario

A company deploys Microsoft Entra Joined laptops to all employees.

When users sign in to Microsoft 365, Microsoft Entra ID verifies both the user's identity and the device identity.

Conditional Access grants access only if the device remains enabled and satisfies the organization's security requirements.

---

## Best Practices

- Register all corporate devices.
- Remove obsolete device identities.
- Disable compromised devices immediately.
- Review inactive devices regularly.
- Combine device identities with Conditional Access.
- Integrate with Microsoft Intune when device management is required.

---

## Common Pitfalls

- Confusing device identity with device management.
- Leaving inactive devices enabled.
- Assuming registered devices are automatically compliant.
- Deleting devices instead of disabling them during investigations.
- Ignoring device lifecycle management.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Device Objects
> - Device identities
> - Device authentication
> - Device trust
> - Conditional Access integration
> - Device lifecycle

---

## Key Takeaways

- Every registered device has a unique identity in Microsoft Entra ID.
- Device identities participate in authentication decisions.
- Conditional Access evaluates both user and device identities.
- Device identity is different from device management.
- Regular lifecycle management improves security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Overview of device identity in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/devices/overview) | Device identity overview |
| [What is a device identity?](https://learn.microsoft.com/entra/identity/devices/device-identities) | Device identity concepts |
| [Microsoft Entra joined devices](https://learn.microsoft.com/entra/identity/devices/concept-directory-join) | Microsoft Entra Joined devices |
| [Manage device identities](https://learn.microsoft.com/entra/identity/devices/manage-device-identities) | Device administration in Microsoft Entra ID |
| [Microsoft Learn – Secure identities with Microsoft Entra ID](https://learn.microsoft.com/training/modules/secure-identities-with-aad/) | Microsoft Learn module |
