# Device Management

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID device identities integrate with device management solutions such as Microsoft Intune and how management differs from device registration.

---

## Device Identity vs Device Management

```text
        Device
          │
          ▼
 Microsoft Entra ID
(Device Identity)
          │
          ▼
 Microsoft Intune
(Device Management)
          │
          ▼
Configuration Policies
Compliance Policies
Application Deployment
Security Baselines
          │
          ▼
 Conditional Access
```

---

> [!TIP]
> **Key Concepts**
>
> - Device identity and device management are different concepts.
> - Microsoft Entra ID creates and maintains device identities.
> - Microsoft Intune manages device configuration and compliance.
> - Conditional Access combines identity and compliance information.
> - Device management helps protect corporate resources.

---

## Overview

Microsoft Entra ID provides the identity of a device, while Microsoft Intune manages its configuration, compliance, and security settings.

Although these services work closely together, they perform different functions.

A device can exist in Microsoft Entra ID without being managed by Microsoft Intune.

---

## MDM and MAM User Scopes

Microsoft Entra ID integrates with Microsoft Intune through **Mobility (MDM and MAM)** settings.

Administrators configure:

| Setting | Purpose |
|---------|---------|
| **MDM User Scope** | Determines which users automatically enroll their devices in Microsoft Intune. |
| **MAM User Scope** | Determines which users receive Mobile Application Management (MAM) policies without requiring device enrollment. |

The MDM User Scope can be configured for:

- All users
- Selected security groups
- None

If a user is outside the configured MDM User Scope, the device can still be registered in Microsoft Entra ID, but it will not automatically enroll in Microsoft Intune.

---

## Device Identity

Microsoft Entra ID is responsible for:

- Creating device identities.
- Authenticating devices.
- Maintaining trust relationships.
- Supporting Conditional Access.
- Providing Single Sign-On (SSO).

It does not configure or secure the operating system.

---

## Device Management

Microsoft Intune provides centralized management for supported devices.

Typical management tasks include:

- Device configuration.
- Security policies.
- Compliance evaluation.
- Application deployment.
- Operating system updates.
- Remote actions.

These capabilities extend beyond identity management.

---

## Device Compliance

Compliance policies determine whether a device satisfies organizational security requirements.

Typical compliance checks include:

- Device encryption enabled.
- Password or PIN configured.
- Operating system supported.
- Operating system updated.
- Device not rooted or jailbroken.

Compliance results can be used by Conditional Access policies.

---

## Compliance State

Microsoft Intune evaluates whether a device complies with the organization's security requirements.

After evaluation, Intune updates the device object in Microsoft Entra ID with its compliance state.

Conditional Access policies use this information when evaluating requirements such as **Require device to be marked as compliant** before granting access to protected resources.

---

## Conditional Access Integration

Conditional Access combines several signals before granting access.

```text
User
 │
 ▼
Authentication
 │
 ├─────────────┐
 ▼             ▼
User Identity Device Identity
 │             │
 └──────┬──────┘
        ▼
 Device Compliance
        │
        ▼
Conditional Access
        │
        ▼
Access Decision
```

A registered device is not necessarily a compliant device.

---

## Management Lifecycle

```text
Register Device
        │
        ▼
Enroll in Intune
        │
        ▼
Apply Configuration
        │
        ▼
Evaluate Compliance
        │
        ▼
Conditional Access
        │
        ▼
Monitor and Update
```

---

## Enterprise Scenario

A company deploys Windows laptops to all employees.

Each device is Microsoft Entra Joined and enrolled in Microsoft Intune.

Intune applies security baselines, configures BitLocker, deploys Microsoft 365 Apps, and evaluates compliance.

Conditional Access allows access to corporate resources only from compliant devices.

---

## Administrative Roles

Different Microsoft Entra and Microsoft Intune roles are responsible for device administration.

| Role | Responsibilities |
|------|------------------|
| **Cloud Device Administrator** | Manage device objects in Microsoft Entra ID, including enabling, disabling, and deleting devices. |
| **Intune Administrator** | Manage device enrollment, compliance policies, configuration profiles, and device management through Microsoft Intune. |

Using dedicated administrative roles helps implement the principle of least privilege.

---

## Best Practices

- Register all corporate devices.
- Enroll managed devices in Microsoft Intune.
- Require compliant devices for sensitive resources.
- Review compliance policies regularly.
- Remove obsolete devices.
- Monitor device compliance continuously.

---

## Common Pitfalls

- Confusing registration with management.
- Assuming registered devices are automatically compliant.
- Ignoring compliance evaluation.
- Leaving inactive devices enrolled.
- Applying overly broad management policies.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Device identity
> - Device management
> - Microsoft Intune integration
> - Device compliance
> - Conditional Access
> - Device lifecycle

---

## Key Takeaways

- Microsoft Entra ID manages device identities.
- Microsoft Intune manages device configuration and compliance.
- Registered devices are not automatically compliant.
- Conditional Access can require compliant devices before granting access.
- Device identity and device management complement each other.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Overview of device identity in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/devices/overview) | Device identity overview |
| [What is Microsoft Intune?](https://learn.microsoft.com/mem/intune/fundamentals/what-is-intune) | Microsoft Intune overview |
| [Device compliance policies in Microsoft Intune](https://learn.microsoft.com/mem/intune/protect/device-compliance-get-started) | Device compliance concepts |
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access integration |
| [Microsoft Learn – Secure identities with Microsoft Entra ID](https://learn.microsoft.com/training/modules/secure-identities-with-aad/) | Microsoft Learn module |
