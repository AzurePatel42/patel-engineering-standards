# Azure Storage Authentication

## Executive Summary

Azure Storage Authentication is the process of securely controlling access to Azure Storage resources such as Blob Storage, Azure Files, Queue Storage, and Table Storage.

Azure provides multiple authentication mechanisms designed for different scenarios, ranging from Azure Active Directory (Microsoft Entra ID) for enterprise applications to Shared Access Signatures (SAS) for temporary delegated access.

Choosing the correct authentication method is critical for building secure, scalable, and maintainable cloud solutions.

---

# Learning Objectives

After completing this guide, you should understand:

- Azure Storage authentication methods
- Microsoft Entra ID authentication
- Azure RBAC
- Shared Key authorization
- Shared Access Signature (SAS)
- User Delegation SAS
- Managed Identity
- Storage Account Access Keys
- Authentication best practices
- Common interview questions

---

# Authentication Overview

Azure Storage supports multiple authentication methods.

```
                    Azure Storage

                          │

        ┌─────────────────┼─────────────────┐

        │                 │                 │

 Microsoft Entra ID   Shared Key          SAS Token

        │

        └──────────────┐

                       │

               Managed Identity
```

---

# Authentication Methods

| Method | Recommended | Typical Use |
|----------|------------|-------------|
| Microsoft Entra ID | ✅ Yes | Enterprise applications |
| Azure RBAC | ✅ Yes | Permission management |
| Managed Identity | ✅ Yes | Azure services |
| User Delegation SAS | ✅ Yes | Temporary delegated access |
| Service SAS | Yes | Limited resource access |
| Account SAS | Sometimes | Administrative scenarios |
| Shared Key | Legacy | Backward compatibility |

---

# 1. Microsoft Entra ID Authentication

Microsoft Entra ID is Microsoft's cloud identity provider.

Instead of storing usernames and passwords inside applications, Azure authenticates users through Entra ID.

```
User

↓

Microsoft Entra ID

↓

Azure RBAC

↓

Storage Account
```

Advantages

- Centralized identity
- Multi-Factor Authentication
- Conditional Access
- Password policies
- Single Sign-On
- Least privilege access

This is Microsoft's recommended authentication method.

---

# 2. Azure Role-Based Access Control (RBAC)

Authentication answers:

> Who are you?

Authorization answers:

> What are you allowed to do?

RBAC controls permissions after authentication.

Example

```
Mahesh

↓

Storage Blob Data Contributor

↓

Blob Container
```

Common Storage Roles

- Storage Blob Data Reader
- Storage Blob Data Contributor
- Storage Blob Data Owner
- Storage Queue Data Contributor
- Storage Table Data Contributor
- Storage Table Data Owner
- Reader
- Contributor
- Owner

---

# 3. Shared Key Authentication

Every Storage Account has two access keys.

```
Storage Account

↓

Access Keys

↓

Key1

Key2
```

Applications can authenticate using these keys.

Advantages

- Simple
- Supported everywhere

Disadvantages

- Full account access
- Difficult to rotate
- Not recommended for modern applications

Microsoft recommends disabling Shared Key authentication whenever possible.

---

# 4. Shared Access Signature (SAS)

A SAS provides temporary delegated access to Azure Storage resources.

Instead of giving someone the storage account key, Azure generates a signed URL with limited permissions.

Example

```
Read

Write

Delete

Expire in 2 hours
```

Advantages

- Temporary access
- Fine-grained permissions
- No account key sharing

---

# Types of SAS

## User Delegation SAS

Uses Microsoft Entra ID credentials.

Recommended.

```
User

↓

Microsoft Entra ID

↓

Generate SAS

↓

Blob
```

---

## Service SAS

Applies to a single storage service.

Examples

- Blob
- Queue
- Table
- File

---

## Account SAS

Grants access to multiple storage services.

Generally used for administrative scenarios.

---

# 5. Managed Identity

Managed Identity allows Azure resources to authenticate without storing credentials.

Example

```
Azure VM

↓

Managed Identity

↓

Microsoft Entra ID

↓

Storage Account
```

No passwords.

No secrets.

No connection strings.

Examples

- Azure VM
- Azure App Service
- Azure Container Apps
- Azure Functions
- Azure Automation

This is the preferred authentication method for Azure-hosted applications.

---

# Storage Account Access Keys

Every Storage Account contains:

- Key1
- Key2

Why two keys?

Key rotation.

Example

```
Application

↓

Key1

↓

Rotate Key2

↓

Switch Application

↓

Rotate Key1
```

This allows zero-downtime key rotation.

---

# Authentication Comparison

| Method | Security | Recommended |
|----------|----------|-------------|
| Microsoft Entra ID | Excellent | ⭐⭐⭐⭐⭐ |
| Managed Identity | Excellent | ⭐⭐⭐⭐⭐ |
| User Delegation SAS | Excellent | ⭐⭐⭐⭐⭐ |
| Service SAS | Good | ⭐⭐⭐⭐ |
| Account SAS | Good | ⭐⭐⭐ |
| Shared Key | Fair | ⭐⭐ |

---

# PPST Authentication Architecture

Future PPST deployment

```
Azure Container Apps

        │

Managed Identity

        │

Microsoft Entra ID

        │

Azure RBAC

        │

Storage Account
```

No passwords.

No access keys.

No secrets inside source code.

---

# Best Practices

✅ Use Microsoft Entra ID whenever possible

✅ Use RBAC

✅ Use Managed Identity

✅ Prefer User Delegation SAS over Shared Key

✅ Rotate Storage Account keys regularly

✅ Disable Shared Key authentication if possible

✅ Follow the Principle of Least Privilege

---

# Common Mistakes

❌ Hardcoding Storage Account keys

❌ Storing secrets in source code

❌ Giving Owner permission unnecessarily

❌ Creating long-lived SAS tokens

❌ Sharing Account SAS publicly

---

# AZ-104 Exam Tips

Remember:

- Authentication identifies users.
- Authorization controls permissions.
- Microsoft Entra ID is the preferred authentication method.
- RBAC manages access.
- Managed Identity removes credential management.
- SAS provides temporary delegated access.
- Shared Key should be avoided for new applications.

---

# Interview Questions

## What is the recommended authentication method for Azure Storage?

Microsoft Entra ID with Azure RBAC.

---

## What is the difference between authentication and authorization?

Authentication verifies identity.

Authorization determines permissions.

---

## What is Managed Identity?

An Azure identity that allows Azure resources to authenticate without storing credentials.

---

## What is a SAS?

A Shared Access Signature that provides temporary delegated access to Azure Storage resources.

---

## Why are there two Storage Account keys?

To support secure key rotation without downtime.

---

## What is the difference between Shared Key and SAS?

Shared Key grants broad access to the storage account.

SAS grants temporary, limited permissions to specific resources.

---

# Key Takeaways

- Microsoft Entra ID is the preferred authentication mechanism.
- RBAC controls permissions after authentication.
- Managed Identity is the recommended approach for Azure-hosted applications.
- SAS enables secure, temporary access.
- Shared Key should only be used when necessary.
- Always follow the Principle of Least Privilege.