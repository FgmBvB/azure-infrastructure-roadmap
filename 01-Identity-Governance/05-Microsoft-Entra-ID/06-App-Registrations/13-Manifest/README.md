# Manifest

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how the Application Manifest represents the complete JSON configuration of an App Registration in Microsoft Entra ID.

---

## Configuration Model

```text
          App Registration
                  │
                  ▼
         Application Object
                  │
                  ▼
          Application Manifest
             (JSON File)
                  │
      ┌───────────┼───────────┐
      ▼           ▼           ▼
 Redirect URIs  App Roles   Scopes
      │           │           │
      └───────────┼───────────┘
                  ▼
       Microsoft Entra ID
```

---

> [!TIP]
> **Key Concepts**
>
> * The Manifest is the JSON representation of an Application Object.
> * Every App Registration has one Manifest.
> * Portal configuration updates the Manifest.
> * Microsoft Graph and automation tools modify the Manifest directly.
> * The Manifest stores the application's identity configuration.

---

## Overview

The Application Manifest is a JSON document that contains the complete configuration of an App Registration.

Although administrators usually configure applications through the Microsoft Entra Admin Center, every configuration change is ultimately stored inside the Manifest.

The Manifest represents the Application Object in a structured format that can be viewed and edited.

> [!NOTE]
>
> Microsoft Entra ID limits the maximum size of an Application Manifest to **2 MB**.
>
> Applications with very large numbers of App Roles, Redirect URIs, certificates, or other configuration entries may exceed this limit and require redesign.

---

## Why the Manifest Exists

The Microsoft Entra Admin Center provides a graphical interface for managing applications.

Behind the scenes, these settings are stored as JSON properties in the Application Manifest.

This enables:

* Automation
* Infrastructure as Code (IaC)
* Microsoft Graph management
* Configuration consistency

---

## Common Properties

The Manifest contains many configuration properties.

Some of the most commonly used include:

| Property                 | Purpose                                       |
| ------------------------ | --------------------------------------------- |
| `appId`                  | Application (Client) ID.                      |
| `id`                     | Object ID of the Application Object.          |
| `signInAudience`         | Supported Account Types.                      |
| `identifierUris`         | Application ID URI.                           |
| `replyUrlsWithType`      | Redirect URIs.                                |
| `appRoles`               | Application Roles.                            |
| `oauth2PermissionScopes` | Delegated Permissions (Scopes).               |
| `keyCredentials`         | Certificates.                                 |
| `passwordCredentials`    | Client Secrets.                               |
| `requiredResourceAccess` | API permissions requested by the application. |

---

## Manifest and the Portal

Changes made through the Microsoft Entra Admin Center automatically update the Manifest.

Likewise, changes performed through Microsoft Graph or automation tools modify the same underlying configuration.

Regardless of the management method, the Application Object remains the single source of truth.

---

## Manifest and Automation

Infrastructure automation tools frequently manage App Registrations by modifying Manifest properties.

Examples include:

* Microsoft Graph API
* Azure CLI
* Azure PowerShell
* Terraform
* Bicep

This enables repeatable and version-controlled application deployments.

---

## Manifest Example

A simplified Manifest may contain properties similar to:

```json
{
  "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "signInAudience": "AzureADMyOrg",
  "identifierUris": [
    "api://xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  ]
}
```

The actual Manifest contains many additional properties depending on the application's configuration.

---

## Enterprise Scenario

A company deploys the same internal application across multiple environments.

Instead of configuring every App Registration manually, administrators manage the Manifest through Infrastructure as Code.

The deployment automatically configures Redirect URIs, API permissions, App Roles, and certificates using a consistent configuration.

---

## Best Practices

* Prefer the portal for simple administration.
* Use automation for repeatable deployments.
* Keep configuration under version control.
* Review Manifest changes before deployment.
* Remove unused configuration properties when appropriate.

---

## Common Pitfalls

* Editing Manifest properties without understanding their purpose.
* Confusing `appId` with `id`.
* Making manual portal changes outside Infrastructure as Code.
* Forgetting to validate JSON syntax.
* Changing Manifest properties directly in production without testing.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Application Manifest
> * JSON configuration
> * Common Manifest properties
> * Relationship with the Application Object
> * Automation through Microsoft Graph
> * Infrastructure as Code

---

## Key Takeaways

* The Manifest is the JSON representation of an Application Object.
* Every App Registration has a Manifest.
* Portal changes modify the Manifest automatically.
* Automation tools manage App Registrations through the Manifest.
* The Manifest stores the application's configuration.

---

## References

| Microsoft Documentation                                                                                                                          | Purpose                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------- |
| [Microsoft Graph application resource type](https://learn.microsoft.com/graph/api/resources/application)                                         | Application Object properties |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals)             | Identity model                |
| [Application manifest reference](https://learn.microsoft.com/entra/identity-platform/reference-app-manifest)                                     | Manifest properties           |
| [Microsoft Graph API](https://learn.microsoft.com/graph/api/resources/application)                                                               | Application management        |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module        |

