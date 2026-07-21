# Azure Key Vault

## Overview

Azure Key Vault is a managed Azure service for securely storing and controlling access to secrets, cryptographic keys, and certificates.

Instead of embedding sensitive information in source code or configuration files, applications retrieve secrets securely from Azure Key Vault at runtime.

Key Vault is a foundational security service for production Azure environments.

---

# Engineering Objectives

Azure Key Vault should provide:

- Secure secret management
- Centralized credential storage
- Certificate management
- Cryptographic key management
- Access control
- Auditing and monitoring

---

# What Can Be Stored?

Azure Key Vault stores three types of objects.

| Object | Purpose |
|---------|---------|
| Secrets | Passwords, API keys, connection strings, tokens |
| Keys | Cryptographic keys for encryption and signing |
| Certificates | SSL/TLS certificates |

---

# Secrets

Typical secrets include:

- Database connection strings
- Azure Storage connection strings
- OpenAI API Keys
- Redis passwords
- JWT signing secrets
- SMTP credentials

Example:

```
Azure Key Vault

├── OpenAI-Api-Key
├── Redis-Password
├── Database-Connection
├── Jwt-Secret
└── Storage-Connection
```

---

# Authentication

Applications should authenticate to Key Vault using:

1. Managed Identity (Preferred)
2. Microsoft Entra ID
3. Service Principals (when required)

Avoid hardcoding credentials.

---

# Authorization

Access should be controlled using Azure RBAC.

Example roles:

- Key Vault Administrator
- Key Vault Secrets Officer
- Key Vault Secrets User

Follow the Principle of Least Privilege.

---

# Managed Identity

Managed Identity allows Azure resources to securely access Key Vault without storing credentials.

Example:

```
Azure Container App
        │
Managed Identity
        │
Azure RBAC
        │
Azure Key Vault
```

This is the recommended authentication pattern for production workloads.

---

# Certificates

Azure Key Vault can manage:

- SSL Certificates
- TLS Certificates
- Certificate renewal
- Certificate rotation

Certificates can be integrated with Azure services.

---

# Networking

Protect Key Vault using:

- Private Endpoints
- Virtual Networks
- Firewall Rules

Disable unnecessary public access.

---

# Monitoring

Monitor Key Vault using:

- Azure Monitor
- Diagnostic Logs
- Azure Activity Logs
- Alerts

Monitor events such as:

- Secret retrieval
- Failed authentication
- Permission changes
- Key operations

---

# Security Best Practices

- Never commit secrets to Git
- Use Managed Identity
- Use Azure RBAC
- Rotate secrets regularly
- Enable logging
- Restrict network access
- Use Private Endpoints for production

---

# PPST Key Vault Standard

Every PPST-based service should:

- Store secrets in Azure Key Vault
- Authenticate using Managed Identity
- Retrieve secrets at runtime
- Avoid hardcoded credentials
- Protect Key Vault with RBAC
- Enable monitoring and auditing

Examples:

- OpenAI API Key
- PostgreSQL password
- Redis password
- Storage credentials
- JWT signing key

---

# Engineering Checklist

- Key Vault created
- Naming standard followed
- Secrets stored securely
- Managed Identity configured
- RBAC assigned
- Private Endpoint configured (production)
- Monitoring enabled
- Secret rotation documented