# Device Management Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended practices for managing device identities securely in Microsoft Entra ID.

---

## Secure Device Lifecycle

```text
Register Device
        │
        ▼
Establish Trust
        │
        ▼
Manage Device
        │
        ▼
Evaluate Compliance
        │
        ▼
Apply Conditional Access
        │
        ▼
Monitor Activity
        │
        ▼
Review and Remove
```

---

> [!TIP]
> **Key Concepts**
>
> - Register only trusted devices.
> - Choose the appropriate device registration model.
> - Require compliant devices for sensitive resources.
> - Review inactive devices regularly.
> - Apply the principle of least privilege.

---

## Overview

Microsoft recommends protecting organizational resources by combining device identities, compliance evaluation, and Conditional Access.

Device identities should be managed throughout their lifecycle to reduce security risks and maintain a healthy Microsoft Entra ID environment.

---

## Choose the Appropriate Registration Model

Select the registration model that matches the ownership of the device.

| Scenario | Recommended Model |
|----------|-------------------|
| Personal (BYOD) devices | Microsoft Entra Registered |
| Corporate cloud-first devices | Microsoft Entra Joined |
| Hybrid Active Directory environments | Microsoft Entra Hybrid Joined |

Using the appropriate model simplifies administration and improves security.

---

## Protect Device Registration

Control who can register or join devices.

Recommendations include:

- Limit which users can join devices to Microsoft Entra ID.
- Require Multi-Factor Authentication (MFA) during device registration.
- Configure an appropriate maximum number of devices per user.
- Review Device Settings periodically.

---

## Integrate with Microsoft Intune

When device management is required:

- Enroll supported devices in Microsoft Intune.
- Apply configuration policies.
- Deploy compliance policies.
- Monitor enrollment status.
- Keep devices updated.

Device identity and device management should work together.

---

## Require Device Compliance

For sensitive applications and resources:

- Require compliant devices through Conditional Access.
- Monitor compliance regularly.
- Investigate non-compliant devices promptly.
- Remove obsolete or unmanaged devices.

Compliance improves the organization's overall security posture.

---

## Manage Device Lifecycle

Device identities should be reviewed throughout their lifecycle.

```text
Register
    │
    ▼
Manage
    │
    ▼
Monitor
    │
    ▼
Review
    │
    ▼
Disable
    │
    ▼
Delete
```

Administrators should disable compromised devices and remove obsolete device objects when they are no longer required.

---

## Monitor Device Activity

Regularly review:

- Registered devices.
- Device sign-in activity.
- Disabled devices.
- Device ownership.
- Device compliance.
- Conditional Access results.

Continuous monitoring helps identify inactive, unmanaged, or compromised devices.

---

## Governance

Organizations should establish governance policies for device identities.

Recommended activities include:

- Review inactive devices regularly.
- Remove obsolete device identities.
- Audit device registrations.
- Review administrative permissions.
- Document registration policies.
- Standardize device onboarding procedures.

---

## Enterprise Scenario

A company deploys Microsoft Entra Joined Windows laptops to all employees.

Only designated administrators can join devices to Microsoft Entra ID, MFA is required during onboarding, and Microsoft Intune automatically enrolls each device.

Conditional Access requires compliant devices before granting access to Microsoft 365 and Azure resources.

Regular lifecycle reviews remove inactive devices and unnecessary registrations.

---

## Best Practices Checklist

- Register only trusted devices.
- Choose the correct registration model.
- Restrict who can register or join devices.
- Require MFA during device registration.
- Integrate with Microsoft Intune where appropriate.
- Require compliant devices for sensitive resources.
- Apply Conditional Access policies.
- Monitor device activity regularly.
- Remove inactive or obsolete devices.
- Review device governance periodically.

---

## Common Pitfalls

- Confusing device registration with device management.
- Registering corporate devices as BYOD.
- Allowing excessive device registrations.
- Ignoring inactive device identities.
- Granting access without evaluating device compliance.
- Failing to review Device Settings.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Device registration models
> - Device lifecycle management
> - Device compliance
> - Conditional Access integration
> - Microsoft Intune integration
> - Governance of device identities

---

## Key Takeaways

- Device identities strengthen Zero Trust security.
- Microsoft Entra ID manages device identities, while Microsoft Intune manages device configuration and compliance.
- Conditional Access can require trusted and compliant devices.
- Regular lifecycle reviews improve security and reduce unnecessary device objects.
- Governance is essential for maintaining a secure device environment.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Overview of device identity in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/devices/overview) | Device identity overview |
| [Manage device identities](https://learn.microsoft.com/entra/identity/devices/manage-device-identities) | Device lifecycle and administration |
| [What is Microsoft Intune?](https://learn.microsoft.com/mem/intune/fundamentals/what-is-intune) | Microsoft Intune overview |
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access integration |
| [Microsoft Learn – Secure identities with Microsoft Entra ID](https://learn.microsoft.com/training/modules/secure-identities-with-aad/) | Microsoft Learn module |
