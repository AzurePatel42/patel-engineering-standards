# Azure Role-Based Access Control (RBAC)

## Overview

Azure Role-Based Access Control (RBAC) determines **what an authenticated identity is allowed to do** within Azure.

Authentication answers:

> Who are you?

Authorization answers:

> What are you allowed to do?

RBAC is Azure's authorization system and should be used for every production deployment.

---

# Engineering Objectives

The RBAC standard ensures:

- Secure access to Azure resources
- Least privilege access
- Centralized permission management
- Auditable security practices
- Consistent access control across environments

---

# RBAC Hierarchy

Azure permissions can be assigned at different scopes.

```
Management Group
        │
        ▼
Subscription
        │
        ▼
Resource Group
        │
        ▼
Individual Resource
```

Permissions assigned at higher scopes are inherited by lower scopes unless explicitly overridden.

---

# Principle of Least Privilege

Every identity should receive only the permissions required to perform its responsibilities.

### Good

Data Ingestion Pipeline

- Read Azure Blob Storage
- Write PostgreSQL
- Read Key Vault secrets

### Bad

Data Ingestion Pipeline

- Owner

Applications should never receive Owner permissions unless absolutely necessary.

---

# Built-in Azure Roles

| Role | Description |
|------|-------------|
| Owner | Full control including permission management |
| Contributor | Create and manage resources but cannot assign permissions |
| Reader | View resources only |
| User Access Administrator | Manage RBAC assignments |

Use built-in roles whenever possible before creating custom roles.

---

# Managed Identities

Applications deployed to Azure should authenticate using Managed Identity.

Recommended flow:

```
Application
        │
        ▼
Managed Identity
        │
        ▼
Azure Resource
```

Avoid:

- Client secrets
- Shared credentials
- Embedded passwords
- Long-lived service principal secrets

---

# Resource Group Permissions

Assign permissions at the Resource Group level whenever practical.

Example:

```
Production Resource Group
        │
Contributor
        │
Engineering Team
```

This simplifies administration and reduces repetitive role assignments.

---

# Auditing

RBAC assignments should be reviewed regularly.

Engineering teams should:

- Remove unused permissions
- Review privileged roles
- Enable Azure Activity Logs
- Audit permission changes

---

# Engineering Checklist

- Azure RBAC enabled
- Least Privilege enforced
- Managed Identity preferred
- No shared credentials
- Built-in roles preferred
- Activity Logs enabled
- Regular access reviews performed

---

# PPST Engineering Standard

Every PPST-based service deployed to Azure must:

- Authenticate using Managed Identity whenever possible
- Follow the Principle of Least Privilege
- Use Azure RBAC for authorization
- Avoid embedded credentials
- Be fully auditable