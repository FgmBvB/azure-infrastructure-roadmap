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

If multiple Conditional Access policies apply simultaneously, Microsoft Entra ID evaluates all applicable policies before making a final access decision.

---

## Policy Evaluation Rules

Multiple Conditional Access policies can apply to a single sign-in.

Microsoft Entra ID follows two fundamental evaluation rules.

### Block Controls Take Priority

If **any** applicable policy contains a **Block access** control, access is denied immediately.

A **Block** decision always overrides any **Grant** decision from other policies.

### Grant Controls Are Cumulative

If multiple policies require different Grant Controls, users must satisfy **all required controls** before access is granted.

For example:

- Policy A requires **Multi-Factor Authentication (MFA)**.
- Policy B requires a **Compliant Device**.

The user must successfully complete **both** requirements.

---

## Report-only Validation

Conditional Access policies can be configured in **Report-only** mode.

When a policy is in this mode:

- The policy is fully evaluated during sign-in.
- Grant Controls are **not enforced**.
- Users are **not blocked**.
- MFA is **not requested**.

Instead, Microsoft Entra ID records the expected result in the **Sign-in Logs** under the **Conditional Access** tab.

Possible evaluation results include:

| Result | Meaning |
|---------|---------|
| **Success** | The user would have satisfied the policy requirements. |
| **Failure** | The user would have failed the policy requirements. |
| **Not Applied** | The policy did not apply because its assignments or conditions were not met. |

Report-only mode allows administrators to validate new policies safely before enabling enforcement.

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

Multiple Grant Controls can be combined to increase security.

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

## Best Practice: Emergency Access Accounts

Microsoft recommends maintaining at least **two emergency access (break-glass) accounts**.

These accounts provide administrative access if Conditional Access policies accidentally prevent all administrators from signing in.

Recommendations include:

- Exclude the accounts from all Conditional Access policies.
- Use long, highly secure passwords.
- Do not associate the accounts with individual employees.
- Store credentials securely.
- Monitor sign-in activity regularly.
- Test the accounts periodically.

Emergency access accounts help prevent tenant lockout during configuration errors or service disruptions.

---

## Enterprise Scenario

A company protects Microsoft 365 and Azure resources using Conditional Access.

Employees signing in from compliant corporate devices inside trusted locations receive seamless access.

When users attempt to sign in from an unmanaged device or an unfamiliar location, Conditional Access requires Multi-Factor Authentication before access is granted.

Administrators test all new policies in **Report-only** mode before enabling enforcement.

---

## Emergency Access Accounts

Microsoft recommends maintaining at least **two emergency access (break-glass) accounts**.

These accounts provide administrative access if Conditional Access policies accidentally prevent all administrators from signing in.

Best practices include:

- Exclude the accounts from all Conditional Access policies.
- Use long, highly secure passwords.
- Do not associate the accounts with individual employees.
- Store credentials securely.
- Monitor sign-in activity regularly.
- Test the accounts periodically.

Emergency access accounts help prevent tenant lockout during configuration errors or service disruptions.

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
