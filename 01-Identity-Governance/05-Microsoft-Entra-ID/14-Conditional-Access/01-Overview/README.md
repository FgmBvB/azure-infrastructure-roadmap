# Conditional Access Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra Conditional Access, explains how access decisions are evaluated, and describes its role within a Zero Trust security model.

---

## Conditional Access Flow

```text
User Sign-in
      │
      ▼
Primary Authentication
      │
      ▼
Microsoft Entra ID
      │
      ▼
Evaluate Policy
      │
      ▼
Assignments
      │
      ▼
Conditions
      │
      ▼
Access Controls
      │
      ▼
Access Granted / Blocked
```

---

> [!TIP]
> **Key Concepts**
>
> - Conditional Access is Microsoft's policy engine for access control.
> - Every sign-in is evaluated against configured policies.
> - Policies can require additional controls such as Multi-Factor Authentication (MFA).
> - Conditional Access is a core component of the Zero Trust security model.
> - Policies are evaluated before access is granted to protected resources.

---

## Overview

Conditional Access is Microsoft's policy-based access control engine built into Microsoft Entra ID.

It evaluates every authentication request using identity, device, application, location, and risk information before deciding whether access should be granted, blocked, or require additional security controls.

Conditional Access allows organizations to apply security only when necessary, improving both protection and user experience.

---

## Zero Trust

Conditional Access is a fundamental component of Microsoft's **Zero Trust** security strategy.

Instead of trusting users or devices automatically, every access request is continuously verified.

The evaluation considers:

- User identity
- Device identity
- Device compliance
- Application being accessed
- Network location
- Risk signals
- Authentication strength

Access is granted only after policy requirements are satisfied.

---

## Policy Components

Every Conditional Access policy consists of four logical components.

| Component | Purpose |
|-----------|---------|
| **Assignments** | Define who, what, and which resources are affected. |
| **Conditions** | Evaluate contextual information during sign-in. |
| **Access Controls** | Grant or block access and define security requirements. |
| **Enable Policy** | Controls whether the policy is Off, On, or Report-only. |

---

## Evaluation Process

During every authentication request Microsoft Entra ID evaluates:

```text
Identity
     │
     ▼
Assignments
     │
     ▼
Conditions
     │
     ▼
Grant Controls
     │
     ▼
Session Controls
     │
     ▼
Access Decision
```

If multiple Conditional Access policies apply simultaneously, all applicable policies are evaluated before a final access decision is made.

---

## Common Policy Conditions

Conditional Access policies can evaluate:

- Users and Groups
- Directory Roles
- Cloud Applications
- Device Platform
- Device State
- Client Applications
- Locations
- Sign-in Risk
- User Risk
- Authentication Context

These conditions determine whether additional security requirements must be enforced.

---

## Access Controls

Conditional Access supports several access decisions.

Common Grant Controls include:

- Require Multi-Factor Authentication (MFA)
- Require compliant device
- Require Microsoft Entra Hybrid Joined device
- Require authentication strength
- Require approved client application
- Block access

Policies may combine multiple Grant Controls to increase security.

---

## Session Controls

After authentication, Conditional Access can also manage the user's session.

Examples include:

- Sign-in frequency
- Persistent browser session
- Continuous Access Evaluation (CAE)
- Application-enforced restrictions

Session Controls help maintain security after authentication has completed.

---

## Enterprise Scenario

A company protects Microsoft 365 and Azure resources using Conditional Access.

Employees signing in from compliant corporate devices inside trusted locations receive seamless access.

When users attempt to sign in from an unmanaged device or an unfamiliar location, Conditional Access requires Multi-Factor Authentication before access is granted.

Administrators test all new policies in **Report-only** mode before enabling enforcement.

---

## Best Practices

- Design policies using the principle of least privilege.
- Test new policies with Report-only mode.
- Require MFA for privileged accounts.
- Protect sensitive applications with Conditional Access.
- Review Sign-in Logs regularly.
- Exclude emergency (break-glass) accounts from production policies.

---

## Common Pitfalls

- Enabling policies without testing.
- Forgetting emergency access accounts.
- Creating overlapping policies.
- Applying overly broad exclusions.
- Ignoring Sign-in Logs.
- Assuming Conditional Access replaces strong identity governance.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Conditional Access architecture
> - Policy evaluation process
> - Assignments
> - Conditions
> - Grant Controls
> - Session Controls
> - Zero Trust integration

---

## Key Takeaways

- Conditional Access evaluates every sign-in before granting access.
- Policies combine assignments, conditions, and access controls.
- Zero Trust relies heavily on Conditional Access.
- Multiple policies can apply to a single authentication request.
- Proper testing and monitoring are essential for secure deployments.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access concepts |
| [Conditional Access policy components](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-policies) | Policy structure |
| [Grant controls](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-grant) | Access controls |
| [Session controls](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-session) | Session management |
| [Microsoft Learn – Describe Conditional Access](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
