# Conditional Access Policies and Conditions

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Conditional Access policies are configured, how assignments and conditions are evaluated, and how Microsoft Entra ID determines whether a policy applies to a sign-in.

---

## Policy Evaluation Flow

```text
Sign-in
    │
    ▼
Assignments
    │
    ▼
Users / Groups
Cloud Apps
User Actions
    │
    ▼
Conditions
    │
    ├── Device Platform
    ├── Locations
    ├── Client Apps
    ├── Device State
    ├── Sign-in Risk
    ├── User Risk
    └── Authentication Context
    │
    ▼
Policy Applies?
    │
 ┌──┴──┐
 │     │
 ▼     ▼
Yes    No
 │
 ▼
Grant Controls
```

---

> [!TIP]
> **Key Concepts**
>
> - A Conditional Access policy first evaluates assignments.
> - Conditions determine whether the policy applies.
> - Multiple conditions can be combined.
> - Policies support Report-only mode for testing.
> - Multiple policies may apply simultaneously.

---

## Overview

Conditional Access policies determine **when** additional security controls should be enforced.

Each policy consists of assignments and optional conditions that evaluate the context of every authentication request before access controls are applied.

---

## Assignments

Assignments define the scope of the policy.

They specify:

- Users
- Groups
- Directory Roles
- Guest Users
- Workload Identities (supported scenarios)

Assignments also specify the protected resources.

These include:

- Cloud Applications
- User Actions
- Authentication Contexts

Policies only continue evaluation if the sign-in matches the configured assignments.

---

## Users and Groups

Policies can target:

- All users
- Selected users
- Security groups
- Microsoft 365 groups
- Directory roles
- Guest users
- External users

Administrators can also configure exclusions.

Exclusions are commonly used for emergency access (break-glass) accounts.

---

## Cloud Applications

Policies may protect:

- All cloud applications
- Selected enterprise applications
- Microsoft applications
- Custom applications integrated with Microsoft Entra ID

Cloud applications determine which resources require Conditional Access evaluation.

---

## User Actions

Conditional Access can protect specific user actions instead of entire applications.

Examples include:

- Register security information
- Register or join devices

This allows administrators to secure sensitive identity operations.

---

## Conditions

Conditions evaluate the context of the authentication request.

Available conditions include:

- User Risk
- Sign-in Risk
- Device Platform
- Locations
- Client Applications
- Device Filter
- Authentication Context

Only when the configured conditions are satisfied does the policy continue to Grant Controls.

---

## Device Platform

Policies can target specific operating systems.

Supported platforms include:

- Windows
- macOS
- iOS
- Android
- Linux

This enables platform-specific security requirements.

---

## Locations

Conditional Access evaluates where authentication originates.

Policies may include:

- Any location
- Named Locations
- Trusted Locations
- Specific countries or regions
- Unknown locations

Organizations commonly require MFA outside trusted corporate networks.

---

### Named Locations

Conditional Access supports two types of Named Locations.

| Type | Description |
|------|-------------|
| **IP Address Ranges** | Uses IPv4 or IPv6 CIDR ranges to identify trusted networks. |
| **Countries** | Uses IP geolocation to identify the user's country or region. |

IP-based Named Locations can be marked as **Trusted Locations**.

Trusted Locations are commonly used to:

- Reduce unnecessary MFA prompts.
- Exclude trusted corporate networks from specific policies.
- Apply location-based access controls.

Country-based locations may also use GPS information from Microsoft Authenticator (when available) to improve location accuracy.

---

## Client Applications

Policies can differentiate between authentication clients.

Examples include:

- Browser
- Mobile apps
- Desktop applications
- Exchange ActiveSync
- Other legacy authentication clients

Blocking legacy authentication clients is a common security recommendation.

---

## Device Filter

Device Filters allow administrators to evaluate device attributes.

Examples include:

- Device ownership
- Operating system version
- Trust type
- Display name
- Extension attributes

Filters provide granular device targeting beyond simple platform selection.

---

## Sign-in Risk

Sign-in Risk represents the probability that a specific authentication attempt is malicious.

Microsoft evaluates signals such as:

- Anonymous IP addresses
- Impossible travel
- Malware-linked IPs
- Suspicious sign-in patterns

Policies can require MFA or block access based on the calculated risk.

---

## User Risk

User Risk estimates the likelihood that a user's identity has been compromised.

Risk detections may include:

- Leaked credentials
- Suspicious account activity
- Threat intelligence signals

Organizations can require password changes or stronger authentication for high-risk users.

---

## Authentication Context

Authentication Context allows applications to request stronger authentication for specific operations.

Rather than protecting an entire application, administrators can require additional controls only for sensitive actions.

This supports granular authorization scenarios.

---

## Report-only Mode

Policies can operate in **Report-only** mode.

When enabled:

- Policies are evaluated normally.
- Access is never blocked.
- MFA is not enforced.
- Expected results are written to the **Conditional Access** section of the Sign-in Logs.

Possible evaluation results include:

| Result | Meaning |
|---------|---------|
| **Success** | The policy requirements would have been satisfied. |
| **Failure** | The sign-in would have failed the policy requirements. |
| **Not Applied** | The policy did not match the sign-in context. |

Report-only mode allows administrators to validate policies before production deployment.

---

## Enterprise Scenario

A company deploys a Conditional Access policy protecting Microsoft 365.

The policy applies to all employees, targets Exchange Online and SharePoint Online, excludes emergency access accounts, requires MFA outside trusted locations, and blocks legacy authentication clients.

Before enabling enforcement, administrators validate the policy using Report-only mode and review the evaluation results in the Sign-in Logs.

---

## Best Practices

- Target groups instead of individual users whenever possible.
- Exclude emergency access accounts.
- Test new policies using Report-only mode.
- Block legacy authentication clients.
- Use Named Locations instead of individual IP addresses.
- Keep policies simple and well documented.

---

## Common Pitfalls

- Applying policies directly to individual users.
- Forgetting exclusions for emergency accounts.
- Blocking administrators accidentally.
- Creating overlapping or conflicting policies.
- Ignoring Report-only testing.
- Applying overly broad conditions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Assignments
> - Users and Groups
> - Cloud Applications
> - User Actions
> - Device Platform
> - Locations
> - Client Applications
> - Device Filters
> - User Risk
> - Sign-in Risk
> - Authentication Context
> - Report-only mode

---

## Key Takeaways

- Assignments define who and what a policy protects.
- Conditions determine when a policy applies.
- Report-only mode enables safe policy validation.
- Risk-based conditions improve security through adaptive access.
- Well-designed Conditional Access policies balance security and usability.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Conditional Access policy components](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-policies) | Policy structure |
| [Conditions in Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-conditions) | Policy conditions |
| [Named locations](https://learn.microsoft.com/entra/identity/conditional-access/concept-assignment-network) | Location-based conditions |
| [Authentication context](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-cloud-apps) | Authentication Context |
| [Report-only mode](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-report-only) | Policy testing |
| [Microsoft Learn – Conditional Access](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
