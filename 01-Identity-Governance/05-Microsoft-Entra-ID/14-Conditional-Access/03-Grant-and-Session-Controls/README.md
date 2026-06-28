# Conditional Access Grant and Session Controls

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Grant Controls and Session Controls determine the final access decision after a Conditional Access policy has been evaluated.

---

## Conditional Access Decision Flow

```text
Policy Applies
      │
      ▼
Grant Controls
      │
      ▼
Requirements Satisfied?
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Yes        No
 │          │
 ▼          ▼
Session   Access
Controls  Blocked
 │
 ▼
Access Granted
```

---

> [!TIP]
> **Key Concepts**
>
> - Grant Controls determine whether access is allowed.
> - Multiple Grant Controls are cumulative.
> - Session Controls apply after successful authentication.
> - Authentication Strengths require specific authentication methods.
> - Continuous Access Evaluation (CAE) improves real-time security.

---

## Overview

Once a Conditional Access policy matches a sign-in request, Microsoft Entra ID evaluates its **Grant Controls**.

If all required controls are satisfied, authentication succeeds and **Session Controls** are applied to manage the user's session.

---

## Grant Controls

Grant Controls define the security requirements that users must satisfy before access is granted.

Available Grant Controls include:

- Require Multi-Factor Authentication (MFA)
- Require Authentication Strength
- Require device to be marked as compliant
- Require Microsoft Entra Hybrid Joined device
- Require approved client app
- Require app protection policy
- Block access

---

## Grant Control Logic

Multiple Grant Controls can be combined within a policy.

Administrators choose how they are evaluated:

| Option | Description |
|---------|-------------|
| **Require all selected controls** | Every selected control must be satisfied. |
| **Require one of the selected controls** | Any one of the selected controls satisfies the policy. |

When multiple Conditional Access policies apply simultaneously, their Grant Controls are cumulative.

---

## Require Multi-Factor Authentication

The most common Grant Control is **Require Multi-Factor Authentication**.

When triggered, users must successfully complete an approved MFA method before access is granted.

MFA requirements are evaluated together with the other configured Grant Controls.

---

## Authentication Strengths

Authentication Strengths allow organizations to require specific authentication methods instead of accepting any MFA method.

Examples include:

- Multi-Factor Authentication
- Passwordless MFA
- Phishing-resistant MFA

This enables administrators to require stronger authentication for sensitive applications or privileged accounts.

---

## Require Compliant Device

This Grant Control requires the device to be marked as compliant.

Compliance is evaluated by Microsoft Intune and reported to Microsoft Entra ID before access is granted.

---

## Require Microsoft Entra Hybrid Joined Device

This control allows access only from devices that are joined to both:

- Active Directory
- Microsoft Entra ID

It is commonly used in Hybrid Identity environments.

---

## Require Approved Client App

Organizations can require users to access resources only through Microsoft-approved applications.

This is commonly used with Microsoft Intune App Protection Policies.

---

## Require App Protection Policy

This control verifies that mobile applications are protected by Microsoft Intune App Protection Policies (MAM).

It is commonly used for Bring Your Own Device (BYOD) scenarios where devices are not fully managed.

---

## Block Access

The **Block Access** control immediately denies access whenever the policy applies.

If any applicable Conditional Access policy contains a Block Access control, access is denied regardless of any Grant Controls defined in other policies.

---

## Session Controls

After successful authentication, Session Controls manage how the authenticated session behaves.

Common Session Controls include:

- Sign-in Frequency
- Persistent Browser Session
- Continuous Access Evaluation (CAE)
- Application-Enforced Restrictions

---

## Sign-in Frequency

Sign-in Frequency determines how often users must reauthenticate.

Organizations commonly configure shorter intervals for privileged accounts and sensitive applications.

---

## Persistent Browser Session

Administrators can control whether browser sessions remain signed in after users close their browsers.

Policies can:

- Always persist sessions
- Never persist sessions

This improves security on shared devices.

---

## Continuous Access Evaluation (CAE)

Continuous Access Evaluation (CAE) reduces reliance on token expiration.

Instead of waiting for access tokens to expire, supported Microsoft services can react immediately to events such as:

- User account disabled
- Password changed
- MFA requirement triggered
- User risk changes
- Account revocation

CAE improves both security and user experience by responding to changes in near real time.

---

## Enterprise Scenario

A company protects Microsoft 365 with Conditional Access.

Employees must authenticate using phishing-resistant MFA and use compliant corporate devices.

After authentication, Sign-in Frequency requires administrators to reauthenticate every eight hours, while Continuous Access Evaluation immediately revokes access if an administrator account is disabled.

---

## Best Practices

- Require MFA through Conditional Access.
- Prefer Authentication Strengths over generic MFA for privileged accounts.
- Require compliant devices for corporate resources.
- Block legacy authentication.
- Configure Sign-in Frequency according to risk.
- Enable Continuous Access Evaluation where supported.

---

## Common Pitfalls

- Using weak authentication methods.
- Applying excessive session restrictions.
- Forgetting that multiple Grant Controls are cumulative.
- Assuming CAE replaces Conditional Access.
- Allowing unmanaged devices to access sensitive resources.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Grant Controls
> - Authentication Strengths
> - Require Compliant Device
> - Require Hybrid Joined Device
> - App Protection Policies
> - Session Controls
> - Continuous Access Evaluation (CAE)

---

## Key Takeaways

- Grant Controls determine whether access is granted.
- Multiple Grant Controls may need to be satisfied simultaneously.
- Authentication Strengths require specific authentication methods.
- Session Controls manage authenticated sessions after sign-in.
- Continuous Access Evaluation strengthens security by reacting quickly to identity changes.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Grant controls in Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-grant) | Grant Controls |
| [Session controls in Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-session) | Session Controls |
| [Authentication strengths](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-strengths) | Authentication Strengths |
| [Continuous Access Evaluation](https://learn.microsoft.com/entra/identity/conditional-access/concept-continuous-access-evaluation) | CAE overview |
| [Microsoft Learn – Conditional Access](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
