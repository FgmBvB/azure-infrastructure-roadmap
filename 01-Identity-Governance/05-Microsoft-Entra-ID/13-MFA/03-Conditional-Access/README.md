# Conditional Access and Multi-Factor Authentication

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra Conditional Access uses Multi-Factor Authentication (MFA) to protect cloud resources through policy-based access decisions.

---

## Conditional Access Flow

```text
User Sign-in
      │
      ▼
Primary Authentication
      │
      ▼
Conditional Access Evaluation
      │
      ├───────────────┐
      │               │
      ▼               ▼
MFA Required      No MFA Required
      │               │
      ▼               ▼
Second Factor    Access Granted
      │
      ▼
Access Granted
```

---

> [!TIP]
> **Key Concepts**
>
> - Conditional Access evaluates every sign-in request.
> - MFA can be required based on policy conditions.
> - Policies can target users, groups, applications, locations, devices, and risk levels.
> - Report-only mode allows policies to be tested safely.
> - Conditional Access is Microsoft's recommended way to enforce MFA.

---

## Overview

Conditional Access is Microsoft's policy engine for controlling access to cloud resources.

Rather than requiring MFA for every sign-in, Conditional Access evaluates contextual information and decides whether additional authentication is necessary.

This enables organizations to balance security and user experience.

---

## Policy Components

Every Conditional Access policy contains four main elements.

| Component | Purpose |
|-----------|---------|
| **Assignments** | Define who and what the policy applies to. |
| **Conditions** | Evaluate contextual information such as location, device, or risk. |
| **Access Controls** | Grant or block access, including requiring MFA. |
| **Enable Policy** | Determines whether the policy is On, Off, or Report-only. |

---

## Assignments

Policies can target:

- Users
- Security Groups
- Directory Roles
- Guest Users
- Cloud Applications
- User Actions

Exclusions can also be configured to prevent unintended lockouts.

---

## Conditions

Conditional Access can evaluate:

- Device platform
- Client applications
- Device state
- Locations
- Sign-in risk
- User risk
- Authentication context

Conditions determine whether additional controls such as MFA should be applied.

---

## Grant Controls

Common Grant Controls include:

- Require Multi-Factor Authentication
- Require compliant device
- Require Microsoft Entra Hybrid Joined device
- Require approved client app
- Require authentication strength
- Block access

Multiple Grant Controls can be combined when higher security is required.

---

## Authentication Strengths

Authentication Strengths allow administrators to require specific authentication methods.

Examples include:

- Multi-Factor Authentication
- Passwordless MFA
- Phishing-resistant MFA

This enables organizations to require stronger authentication methods for sensitive applications.

---

## Report-only Mode

Conditional Access policies support **Report-only** mode.

When enabled:

- Policies are evaluated.
- Access is never blocked.
- MFA is not enforced.
- Administrators can review what the policy **would have done** before enabling it.

Report-only mode is recommended when deploying new Conditional Access policies.

---

## Trusted Locations

Trusted Locations identify known corporate networks.

Organizations commonly use them to:

- Reduce unnecessary MFA prompts.
- Apply different Conditional Access policies.
- Improve user experience while maintaining security.

Trusted Locations should be configured carefully and reviewed regularly.

---

## Conditional Access Evaluation

```text
User
 │
 ▼
Sign-in
 │
 ▼
Conditional Access
 │
 ├── Users
 ├── Application
 ├── Device
 ├── Location
 ├── Risk
 │
 ▼
Grant Controls
 │
 ▼
Require MFA?
 │
 ▼
Access Granted / Blocked
```

---

## Enterprise Scenario

A company protects Microsoft 365 using Conditional Access.

Employees signing in from compliant corporate devices within trusted office locations are granted access with minimal friction.

When users sign in from an unknown location or unmanaged device, Conditional Access requires Microsoft Authenticator before access is granted.

Administrators validate all new policies in **Report-only** mode before enabling enforcement.

---

## Best Practices

- Require MFA through Conditional Access instead of per-user MFA.
- Test new policies using Report-only mode.
- Protect privileged accounts with phishing-resistant authentication methods.
- Configure emergency access (break-glass) accounts and exclude them from Conditional Access policies.
- Use Trusted Locations carefully.
- Review policy effectiveness regularly through Sign-in Logs.

---

## Common Pitfalls

- Enabling policies without testing.
- Forgetting administrator exclusions.
- Creating overlapping policies.
- Trusting all locations without validation.
- Relying only on location-based controls.
- Using legacy per-user MFA instead of Conditional Access.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Conditional Access policy structure
> - Assignments and Conditions
> - Grant Controls
> - Authentication Strengths
> - Report-only mode
> - Trusted Locations
> - MFA enforcement through Conditional Access

---

## Key Takeaways

- Conditional Access is Microsoft's recommended method for enforcing MFA.
- Policies evaluate contextual information before granting access.
- Report-only mode enables safe policy testing.
- Authentication Strengths allow organizations to require stronger authentication methods.
- Properly designed Conditional Access policies improve both security and user experience.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access concepts |
| [Grant controls in Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-grant) | Grant controls and MFA |
| [Authentication strengths](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-strengths) | Authentication Strengths |
| [Named locations](https://learn.microsoft.com/entra/identity/conditional-access/concept-assignment-network) | Trusted (Named) Locations |
| [Report-only mode](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-report-only) | Testing Conditional Access policies |
| [Microsoft Learn – Describe Conditional Access](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
