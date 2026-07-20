# Naming Standards

## Overview

Naming Standards establish a consistent approach for naming Azure resources across the Patel Engineering cloud platform.

A standardized naming convention improves resource discovery, operational efficiency, automation, governance, troubleshooting, and long-term maintainability.

As the cloud environment grows, consistent naming becomes essential for managing infrastructure at scale.

Within Patel Engineering, every Azure resource must follow approved naming conventions to ensure clarity, predictability, and consistency across all environments.

---

# Purpose

The purpose of Naming Standards is to create a uniform language for identifying Azure resources throughout the engineering platform.

Consistent naming enables engineers to quickly understand a resource's purpose, environment, ownership, and role without additional documentation.

These standards also improve automation, Infrastructure as Code (IaC), monitoring, security, and operational management.

---

# Why Naming Standards Matter

Cloud environments often contain hundreds or thousands of resources.

Without consistent naming conventions, engineers may experience:

- Difficulty locating resources
- Confusing deployments
- Operational mistakes
- Security management challenges
- Inconsistent automation
- Poor cost visibility
- Slower troubleshooting

A well-defined naming strategy eliminates ambiguity and creates a predictable cloud environment.

---

# Patel Engineering Standard

Patel Engineering follows a standardized naming convention based on resource type, application, and environment.

General format:

```
<resource-type>-<application>-<environment>
```

Example:

```
rg-ppst-dev
```

Where:

- **resource-type** identifies the Azure resource.
- **application** identifies the platform or service.
- **environment** identifies the deployment environment.

Every Azure resource should be immediately recognizable by its name.

---

# Standard Resource Prefixes

| Resource | Prefix |
|----------|--------|
| Resource Group | rg |
| Virtual Network | vnet |
| Subnet | snet |
| Network Security Group | nsg |
| Storage Account | st |
| Key Vault | kv |
| Azure Container Registry | acr |
| Container App Environment | cae |
| Container App | ca |
| SQL Server | sql |
| SQL Database | sqldb |
| Log Analytics Workspace | law |
| Application Insights | appi |
| Managed Identity | mi |
| Recovery Services Vault | rsv |

---

# Environment Codes

| Environment | Code |
|------------|------|
| Development | dev |
| Testing | test |
| Staging | stage |
| Production | prod |
| Disaster Recovery | dr |
| Sandbox | sbx |

---

# Examples

## Resource Groups

```
rg-ppst-dev
rg-ppst-test
rg-ppst-prod
```

## Storage Accounts

```
stppstdev001
stppstprod001
```

*(Storage Account names follow Azure naming restrictions and therefore omit hyphens.)*

## Key Vault

```
kv-ppst-dev
kv-ppst-prod
```

## Azure Container Registry

```
acrppstdev
acrppstprod
```

## Container Apps

```
ca-inventory-dev
ca-auth-prod
ca-retrieval-prod
```

## Virtual Networks

```
vnet-ppst-dev
vnet-ppst-prod
```

---

# Naming Principles

Every resource name should be:

- Meaningful
- Predictable
- Consistent
- Environment-aware
- Automation-friendly
- Human-readable whenever Azure allows
- Compliant with Azure naming restrictions

Abbreviations should only be used when they are widely recognized or required by Azure naming rules.

---

# Future Enhancements

Future versions of this standard may include:

- Enterprise tagging strategy
- Global region naming
- Multi-subscription naming
- Multi-tenant conventions
- Infrastructure as Code naming validation
- Automated policy enforcement using Azure Policy

---

**Patel Engineering Standard**

*Consistency begins with naming. Well-named systems are easier to build, operate, secure, and scale.*