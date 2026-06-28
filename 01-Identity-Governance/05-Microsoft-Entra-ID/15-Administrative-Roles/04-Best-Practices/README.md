# Microsoft Entra Administrative Roles Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended practices for assigning, managing, and auditing administrative roles in Microsoft Entra ID.

---

## Administrative Lifecycle

```text
Identify Responsibility
        │
        ▼
Select the Appropriate Role
        │
        ▼
Assign the Minimum Permissions
        │
        ▼
Protect the Role
        │
        ▼
Monitor Activity
        │
        ▼
Review and Remove Access
```

---

> [!TIP]
> **Key Concepts**
>
> - Follow the principle of least privilege.
> - Minimize permanent privileged access.
> - Use Privileged Identity Management (PIM) whenever available.
> - Protect privileged accounts with Multi-Factor Authentication (MFA).
> - Review administrative assignments regularly.

---

## Overview

Administrative roles control access to identity management operations across Microsoft Entra ID.

Proper role assignment reduces security risks while ensuring administrators have the permissions required to perform their responsibilities.

Microsoft recommends minimizing privileged access and continuously reviewing administrative permissions.

---

## Follow the Principle of Least Privilege

Always assign the role with the minimum permissions required.

Instead of assigning **Global Administrator**, use specialized roles such as:

- User Administrator
- Groups Administrator
- Authentication Administrator
- Cloud Application Administrator
- Security Administrator

Reducing unnecessary privileges lowers the attack surface.

---

## Limit Global Administrators

Global Administrator is the most privileged built-in role.

Microsoft recommends:

- Keeping only two to five permanent Global Administrators.
- Assigning Global Administrator only when absolutely necessary.
- Using Privileged Identity Management (PIM) for temporary elevation.
- Monitoring Global Administrator activity closely.

---

## Use Privileged Identity Management (PIM)

Where licensing permits, Microsoft recommends using Microsoft Entra Privileged Identity Management.

Benefits include:

- Just-in-Time (JIT) administration.
- Eligible role assignments.
- Approval workflows.
- Multi-Factor Authentication during activation.
- Automatic expiration of elevated permissions.
- Complete auditing of privileged operations.

PIM significantly reduces standing privileged access.

---

## Assign Roles to Role-Assignable Groups

Instead of assigning roles directly to users, assign them to **Role-Assignable Groups** whenever appropriate.

Benefits include:

- Simplified administration.
- Centralized permission management.
- Easier onboarding and offboarding.
- Consistent administrative delegation.

Only cloud-created Security Groups with the **isAssignableToRole** property can receive Microsoft Entra administrative roles.

---

## Protect Administrator Accounts

Administrative accounts should receive stronger protection than standard users.

Recommendations include:

- Require Multi-Factor Authentication.
- Prefer phishing-resistant authentication methods.
- Use Conditional Access.
- Monitor administrator sign-ins.
- Avoid using privileged accounts for daily productivity tasks.

---

## Maintain Emergency Access Accounts

Maintain at least two emergency (break-glass) accounts.

Recommendations:

- Exclude them from Conditional Access policies.
- Use long, complex passwords.
- Store credentials securely.
- Monitor sign-ins.
- Test them periodically.

Emergency accounts protect against tenant lockout.

---

## Review Role Assignments

Administrative permissions should be reviewed regularly.

Review activities include:

- Removing obsolete assignments.
- Verifying least privilege.
- Auditing privileged accounts.
- Reviewing inactive administrators.
- Validating emergency accounts.

Where available, Microsoft Entra **Access Reviews** can automate periodic reviews of privileged role assignments.

---

## Audit Administrative Activity

Regularly monitor:

- Audit Logs
- Sign-in Logs
- PIM activation history
- Administrative role assignments
- Privileged operations

Auditing helps detect unauthorized privilege changes and supports compliance.

---

## Enterprise Scenario

A company protects privileged administration using Microsoft Entra PIM.

Most administrators receive **Eligible** assignments instead of permanent privileges.

Administrative roles are assigned through Role-Assignable Groups, privileged accounts authenticate using phishing-resistant MFA, and emergency access accounts remain excluded from Conditional Access.

Quarterly Access Reviews validate that privileged assignments remain appropriate.

---

## Best Practices Checklist

- Apply least privilege.
- Limit Global Administrators.
- Use Privileged Identity Management.
- Prefer Eligible over permanent assignments.
- Assign roles through Role-Assignable Groups.
- Protect administrator accounts with MFA.
- Maintain emergency access accounts.
- Review privileged assignments regularly.
- Audit administrative activity continuously.

---

## Common Pitfalls

- Assigning Global Administrator unnecessarily.
- Granting permanent privileged access.
- Ignoring Role-Assignable Groups.
- Not reviewing privileged assignments.
- Using privileged accounts for everyday work.
- Forgetting emergency access accounts.
- Leaving inactive administrators assigned to privileged roles.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Least privilege
> - Global Administrator recommendations
> - Privileged Identity Management (PIM)
> - Eligible vs Active assignments
> - Role-Assignable Groups
> - Emergency access accounts
> - Administrative auditing

---

## Key Takeaways

- Administrative roles should follow the principle of least privilege.
- Global Administrator should be assigned sparingly.
- Privileged Identity Management reduces standing administrative privileges.
- Role-Assignable Groups simplify secure administration.
- Regular reviews and auditing are essential for maintaining a secure Microsoft Entra environment.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra built-in roles](https://learn.microsoft.com/entra/identity/role-based-access-control/permissions-reference) | Built-in administrative roles |
| [Assign Microsoft Entra roles](https://learn.microsoft.com/entra/identity/role-based-access-control/manage-roles-portal) | Role assignment |
| [Role-Assignable Groups](https://learn.microsoft.com/entra/identity/role-based-access-control/groups-concept) | Administrative role groups |
| [Microsoft Entra Privileged Identity Management](https://learn.microsoft.com/entra/id-governance/privileged-identity-management/pim-configure) | PIM overview |
| [Access Reviews](https://learn.microsoft.com/entra/id-governance/access-reviews-overview) | Periodic access reviews |
| [Microsoft Learn – Manage Microsoft Entra permissions by using RBAC](https://learn.microsoft.com/training/modules/manage-permissions-entra-id/) | Microsoft Learn module |
