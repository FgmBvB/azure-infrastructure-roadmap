# Group Management

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers group administration in Microsoft Entra ID, including membership management, Dynamic Groups, Group-based Licensing, Administrative Units, and common management operations.

---

## Overview

Microsoft Entra ID provides centralized management for groups used across Azure, Microsoft 365, Enterprise Applications, Conditional Access, and Intune.

Efficient group management simplifies administration, reduces manual effort, and improves security by ensuring permissions and licenses are assigned consistently.

---

## Learning Objectives

After completing this section you should be able to:

- Manage group membership.
- Configure Dynamic Groups.
- Manage Group-based Licensing.
- Delegate administration using Administrative Units.
- Perform bulk group operations.
- Troubleshoot common group management issues.
- Apply Microsoft best practices.

---

## Group Management Lifecycle

```text
Create Group
      │
      ▼
Configure Properties
      │
      ▼
Assign Owners
      │
      ▼
Add Members
      │
      ▼
Assign Permissions
      │
      ▼
Monitor & Review
      │
      ▼
Update or Remove
```

---

## Membership Management

Administrators can manage group membership manually or automatically.

Common operations include:

- Add members.
- Remove members.
- Assign owners.
- Transfer ownership.
- Review memberships.
- Restore deleted Microsoft 365 Groups.

Membership changes are reflected automatically across supported Microsoft Entra services.

---

## Dynamic Groups

Dynamic Groups automatically calculate membership based on Microsoft Entra attributes.

Administrators define membership rules instead of manually managing users.

Common attributes include:

- Department
- Job Title
- Country
- User Type
- Device Ownership
- Operating System

Dynamic Groups automatically update whenever matching attributes change.

---

## Group-based Licensing

Group-based Licensing automatically assigns licenses to members of a licensed Security Group.

Benefits include:

- Automatic license assignment.
- Simplified administration.
- Consistent onboarding.
- Automatic license removal when users leave the group.

Administrators should monitor licensing errors and available license capacity.

---

## Administrative Units

Administrative Units allow delegated management of users, groups, and devices within a limited administrative scope.

Typical scenarios include:

- Regional IT teams.
- Department administrators.
- Campus administration.
- Business unit delegation.

Administrative Units reduce the need for tenant-wide administrative permissions.

---

## Bulk Operations

Microsoft Entra ID supports bulk administration for groups.

Examples include:

- Bulk member import.
- Bulk member removal.
- Bulk updates.
- Bulk ownership changes.

Bulk operations can be performed using CSV files, PowerShell, Microsoft Graph, or Azure CLI.

---

## Monitoring and Troubleshooting

Administrators should regularly monitor:

- Group membership changes.
- Dynamic Group evaluation.
- License assignment errors.
- Group ownership.
- Audit Logs.

Audit Logs provide visibility into administrative changes and simplify troubleshooting.

---

## Enterprise Scenario

A multinational company creates Dynamic Groups based on department attributes.

Group-based Licensing automatically assigns Microsoft 365 licenses to employees, while Administrative Units allow regional IT teams to manage only their local users and groups.

Audit Logs are reviewed regularly to monitor administrative activity.

---

## Best Practices

- Use Dynamic Groups whenever appropriate.
- Assign multiple group owners.
- Prefer Group-based Licensing over individual assignments.
- Review group membership periodically.
- Monitor licensing errors.
- Delegate administration using Administrative Units.
- Audit group changes regularly.

---

## Common Pitfalls

- Creating unnecessary duplicate groups.
- Forgetting to assign group owners.
- Ignoring Dynamic Group rule validation.
- Managing licenses individually.
- Not monitoring licensing failures.
- Granting excessive administrative permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Membership management
> - Dynamic Groups
> - Group-based Licensing
> - Administrative Units
> - Bulk operations
> - Audit Logs

---

## Key Takeaways

- Effective group management simplifies identity administration.
- Dynamic Groups automate membership based on user or device attributes.
- Group-based Licensing reduces administrative overhead.
- Administrative Units support delegated administration.
- Regular monitoring and auditing improve security and operational efficiency.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Manage Microsoft Entra groups](https://learn.microsoft.com/entra/identity/users/groups-manage-groups) | Group administration |
| [Dynamic membership rules](https://learn.microsoft.com/entra/identity/users/groups-create-rule) | Configure Dynamic Groups |
| [Group-based licensing](https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing) | Automatic license assignment |
| [Administrative Units](https://learn.microsoft.com/entra/identity/role-based-access-control/administrative-units) | Delegated administration |
| [Microsoft Learn – Create users and groups](https://learn.microsoft.com/training/modules/create-users-and-groups-in-azure-active-directory/) | Microsoft Learn module |
