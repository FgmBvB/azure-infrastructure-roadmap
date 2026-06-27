# Authorization

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how authenticated identities are authorized to access Azure resources, applications, and services.

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
        Azure RBAC / Policies
                │
      Evaluate Permissions
                │
      ┌─────────┴─────────┐
      │                   │
 Access Granted      Access Denied
```

---

> [!TIP]
> **Key Concepts**
>
> - Authorization determines what an identity is allowed to do.
> - Authorization always occurs after authentication.
> - Azure RBAC is Azure's primary authorization system.
> - Permissions are evaluated before access is granted.
> - Least privilege is a fundamental security principle.

---

## Overview

Authorization is the process of determining whether an authenticated identity is allowed to perform a specific action.

While authentication verifies the identity of a user or workload, authorization evaluates permissions assigned to that identity.

In Microsoft Azure, authorization is primarily performed through Azure Role-Based Access Control (Azure RBAC).

---

## Authentication vs Authorization

Authentication and authorization are closely related but represent different stages of the access process.

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Determines permissions |
| Answers "Who are you?" | Answers "What are you allowed to do?" |
| Performed first | Performed after authentication |
| Microsoft Entra ID | Azure RBAC |

Authentication alone never grants access.

Every request must also pass authorization.

---

## How Authorization Works

Once Microsoft Entra ID successfully authenticates an identity, Azure evaluates whether the identity has sufficient permissions to perform the requested operation.

Azure RBAC evaluates:

- Assigned roles
- Scope
- Inheritance
- Deny assignments (when applicable)

If the required permissions exist, Azure authorizes the request.

Otherwise, access is denied.

---

## Authorization Scope

Azure RBAC permissions are assigned at different scopes.

```text
Management Group
        │
 Subscription
        │
 Resource Group
        │
     Resource
```

Permissions assigned at higher scopes are inherited by lower scopes unless restricted.

This inheritance model simplifies administration in enterprise environments.

---

## Role Assignments

Authorization is based on three fundamental components:

| Component | Description |
|-----------|-------------|
| Security Principal | User, Group, Service Principal or Managed Identity |
| Role Definition | Collection of permissions |
| Scope | Where the permissions apply |

A role assignment combines these three elements.

---

## Least Privilege

The principle of least privilege states that identities should receive only the permissions required to perform their tasks.

Granting excessive permissions increases security risks and administrative complexity.

Microsoft recommends assigning the minimum permissions necessary.

---

## Enterprise Scenario

An Azure Administrator assigns the **Virtual Machine Contributor** role to a support engineer at the Resource Group scope.

The engineer can manage virtual machines within that Resource Group but cannot modify networking resources or resources located in other Resource Groups.

Authentication verifies the engineer's identity.

Azure RBAC authorizes only the actions allowed by the assigned role.

---

## Best Practices

- Follow the principle of least privilege.
- Assign permissions to groups instead of individual users.
- Use the smallest appropriate scope.
- Review role assignments regularly.
- Avoid assigning Owner permissions unless required.
- Use built-in roles whenever possible.

---

## Common Pitfalls

- Confusing authentication with authorization.
- Assigning permissions directly to users.
- Using overly broad scopes.
- Granting Owner unnecessarily.
- Ignoring inherited permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Authorization concepts
> - Azure RBAC
> - Role assignments
> - Security principals
> - Scope
> - Inheritance
> - Least privilege
> - Authentication versus authorization

---

## Key Takeaways

- Authentication verifies identity.
- Authorization determines permissions.
- Azure RBAC is Azure's authorization system.
- Permissions are evaluated after authentication.
- Scope and inheritance determine where permissions apply.
- Least privilege reduces security risks.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC overview |
| https://learn.microsoft.com/azure/role-based-access-control/scope-overview | RBAC scope and inheritance |
| https://learn.microsoft.com/azure/role-based-access-control/built-in-roles | Built-in Azure roles |
| https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/ | Microsoft Learn – Azure RBAC |
