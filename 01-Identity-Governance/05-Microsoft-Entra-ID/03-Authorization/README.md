# Authorization

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Azure determines whether an authenticated identity is allowed to perform specific actions on Azure resources.

---

## Authorization Flow

```text
                User
                  │
      Authentication Success
                  │
                  ▼
         Microsoft Entra ID
                  │
         Identity Verified
                  │
                  ▼
          Azure Resource Manager
                  │
                  ▼
        Azure RBAC Evaluation
                  │
        Role Assignment Found?
          │               │
         Yes              No
          │               │
          ▼               ▼
 Permission Allowed?   Access Denied
          │
     ┌────┴────┐
     │         │
    Yes       No
     │         │
     ▼         ▼
Access      Access
Granted     Denied
```

---

> [!TIP]
> **Key Concepts**
>
> - Authorization determines what an identity is allowed to do.
> - Authorization always occurs after authentication.
> - Microsoft Entra ID authenticates identities.
> - Azure Resource Manager requests authorization.
> - Azure RBAC evaluates permissions.
> - Least privilege is a core Azure security principle.

---

## Overview

Authorization is the process of determining whether an authenticated identity is allowed to perform a requested operation.

Authentication confirms **who** the identity is.

Authorization determines **what** that identity can do.

In Microsoft Azure, authorization is primarily enforced through **Azure Role-Based Access Control (Azure RBAC)**.

Every request sent to Azure Resource Manager (ARM) is evaluated before access is granted.

---

## Authentication vs Authorization

Authentication and authorization are complementary but independent security processes.

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Determines permissions |
| Answers "Who are you?" | Answers "What are you allowed to do?" |
| Performed by Microsoft Entra ID | Evaluated by Azure RBAC |
| Happens first | Happens after authentication |

Authentication alone never grants access.

Every operation performed in Azure requires a successful authorization evaluation.

---

## How Authorization Works

Once Microsoft Entra ID successfully authenticates an identity, Azure Resource Manager evaluates whether that identity has sufficient permissions to perform the requested operation.

Azure RBAC evaluates several factors before allowing access, including:

- Assigned role(s)
- Scope
- Permission inheritance
- Deny Assignments (when applicable)

If all authorization requirements are satisfied, Azure Resource Manager performs the requested operation.

Otherwise, the request is rejected.

---

## Authorization Components

Azure authorization is based on three core components.

```text
Security Principal
        +
 Role Definition
        +
      Scope
        │
        ▼
  Role Assignment
```

| Component | Description |
|-----------|-------------|
| Security Principal | User, Group, Service Principal, or Managed Identity requesting access. |
| Role Definition | Collection of allowed permissions. |
| Scope | Location where permissions apply. |

A Role Assignment combines these three elements to determine what an identity can do within Azure.

---

## Authorization Scope

Azure RBAC permissions can be assigned at different levels of the Azure hierarchy.

```text
Management Group
        │
 Subscription
        │
 Resource Group
        │
    Resource
```

Permissions assigned at higher scopes are automatically inherited by lower scopes.

This inheritance model simplifies administration across large Azure environments.

---

## Role Definitions

A Role Definition specifies the operations that can be performed on Azure resources.

Role definitions contain one or more allowed operations (`Actions`) and may optionally include excluded operations (`NotActions`).

`NotActions` does **not** create an explicit deny. Instead, it removes permissions from that specific role definition.

If another assigned role grants the same permission, the operation is still allowed.

Azure role definitions can also include `DataActions` and `NotDataActions`, which apply to data-plane operations for supported Azure services.

---

## Deny Assignments

Azure RBAC is primarily an **allow-based** authorization system.

Permissions are granted through role assignments.

In some scenarios, Azure also evaluates **Deny Assignments**, which explicitly prevent certain operations regardless of other role assignments.

Unlike standard Azure RBAC roles, Deny Assignments are typically created and managed by Azure services rather than by administrators.

They are commonly used to protect managed resources from accidental modification or deletion.

When a Deny Assignment applies, it overrides inherited or directly assigned allow permissions.

For example, even if a user has the **Owner** role at the Subscription scope, a Deny Assignment protecting a Resource Group can still prevent specific operations such as deleting protected resources.

This precedence helps Azure protect managed resources from accidental or unauthorized changes.

---

## Microsoft Entra ID Roles vs Azure RBAC Roles

Microsoft Entra ID administrative roles and Azure RBAC roles serve different purposes.

| Microsoft Entra ID Roles | Azure RBAC Roles |
|---------------------------|------------------|
| Manage identities and directory objects | Manage Azure resources |
| Scope: Microsoft Entra ID tenant | Scope: Azure resources |
| Example: Global Administrator | Example: Owner |
| Example: User Administrator | Example: Virtual Machine Contributor |
| Example: Application Administrator | Example: Reader |

Microsoft Entra ID roles manage the identity platform.

Azure RBAC roles manage Azure infrastructure resources.

Although both use role-based authorization, they operate independently.

---

## Least Privilege

The principle of least privilege states that identities should receive only the permissions required to perform their tasks.

Granting excessive permissions increases security risks and administrative complexity.

Microsoft recommends assigning the minimum permissions necessary and periodically reviewing existing role assignments.

---

## Enterprise Scenario

An Azure Administrator assigns the **Virtual Machine Contributor** role to the Operations team at the Resource Group scope.

Team members can create, start, stop, and manage virtual machines inside that Resource Group.

However, they cannot modify virtual networks, create storage accounts outside their assigned scope, or manage resources in other Resource Groups.

Authentication verifies the user's identity.

Azure RBAC authorizes only the operations allowed by the assigned role.

---

## Best Practices

- Follow the principle of least privilege.
- Assign permissions to groups instead of individual users.
- Use the smallest appropriate scope.
- Review role assignments regularly.
- Use built-in roles whenever possible.
- Limit the number of Owner role assignments.
- Regularly audit privileged access.

---

## Common Pitfalls

- Confusing authentication with authorization.
- Assuming authentication automatically grants permissions.
- Assigning permissions directly to users.
- Using excessively broad scopes.
- Granting the Owner role unnecessarily.
- Ignoring inherited permissions.
- Confusing Microsoft Entra ID roles with Azure RBAC roles.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Authorization concepts
> - Azure RBAC fundamentals
> - Role Assignments
> - Role Definitions
> - Security Principals
> - Authorization Scope
> - Permission inheritance
> - Least privilege
> - Microsoft Entra ID roles versus Azure RBAC roles
> - Deny Assignments (conceptual understanding)

---

## Key Takeaways

- Authentication verifies identity.
- Authorization determines permissions.
- Azure Resource Manager evaluates authorization before performing operations.
- Azure RBAC is Azure's primary authorization system.
- A Role Assignment combines a Security Principal, a Role Definition, and a Scope.
- Permissions inherit from higher scopes to lower scopes.
- Microsoft Entra ID roles and Azure RBAC roles are independent authorization systems.
- Least privilege reduces security risks and improves governance.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC overview |
| https://learn.microsoft.com/azure/role-based-access-control/scope-overview | Scope and inheritance |
| https://learn.microsoft.com/azure/role-based-access-control/role-definitions | Azure role definitions |
| https://learn.microsoft.com/azure/role-based-access-control/deny-assignments | Deny Assignments |
| https://learn.microsoft.com/azure/role-based-access-control/built-in-roles | Built-in Azure roles |
| https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/ | Microsoft Learn – Secure Azure resources with RBAC |
