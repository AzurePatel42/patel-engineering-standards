# Azure Container Registry (ACR)

## Overview

Azure Container Registry (ACR) is Microsoft's private container image registry service.

It provides a secure, scalable, and highly available repository for storing, managing, and distributing container images used by Azure services.

Azure Container Registry integrates seamlessly with Azure Container Apps, Azure Kubernetes Service (AKS), Azure App Service, and other Azure compute services.

---

# Engineering Objectives

Azure Container Registry should provide:

- Secure image storage
- Private container repositories
- Version control for container images
- High availability
- Integration with Azure services
- Image lifecycle management

---

# What is a Container Registry?

A container registry stores Docker and OCI-compatible container images.

Development workflow:

Developer

↓

Docker Build

↓

Docker Image

↓

Azure Container Registry

↓

Azure Container Apps

↓

Running Application

---

# Container Images

A container image packages everything an application needs to run.

Typical contents include:

- Application code
- Runtime
- Libraries
- Dependencies
- Configuration
- Startup commands

Example:

```
patel-data-ingestion:v1.0.0
```

---

# Repository Organization

A single Azure Container Registry can contain multiple repositories.

Example:

```
Azure Container Registry

├── ppst
├── inventory-api
├── data-ingestion
├── retrieval-service
├── auth-service
└── cost-intelligence
```

Each repository can contain multiple versions.

---

# Image Tagging Strategy

Use semantic versioning.

Examples:

```
v1.0.0
v1.1.0
v1.2.3
latest
```

Avoid using only the **latest** tag in production environments.

---

# Authentication

Azure Container Registry supports:

- Microsoft Entra ID
- Managed Identity
- Azure RBAC
- Service Principals
- Admin User (development only)

Preferred authentication:

```
Managed Identity

↓

Azure RBAC

↓

Azure Container Registry
```

---

# Azure RBAC

Common roles include:

- AcrPull
- AcrPush
- AcrDelete
- Owner

Follow the Principle of Least Privilege.

---

# Security Best Practices

- Disable Admin User in production
- Use Managed Identity
- Enable Azure RBAC
- Restrict network access
- Enable image scanning
- Use signed images
- Remove unused images regularly

---

# Networking

Protect Azure Container Registry using:

- Private Endpoints
- Virtual Networks
- Firewall Rules

Restrict public access whenever possible.

---

# Image Lifecycle Management

Regularly maintain the registry by:

- Removing unused images
- Cleaning old versions
- Applying retention policies
- Organizing repositories

Lifecycle management reduces storage costs.

---

# Integration with Azure Container Apps

Deployment workflow:

```
Developer

↓

GitHub

↓

Docker Build

↓

Azure Container Registry

↓

Azure Container Apps

↓

Production
```

Azure Container Apps pulls images directly from Azure Container Registry.

---

# PPST Container Registry Standard

Every PPST-based project should:

- Build Docker images
- Store images in Azure Container Registry
- Follow semantic versioning
- Authenticate using Managed Identity
- Use Azure RBAC
- Remove obsolete images
- Keep repositories organized

Example repositories:

- ppst
- inventory-api
- data-ingestion
- retrieval-service
- auth-service
- cost-intelligence

---

# Engineering Checklist

- Azure Container Registry created
- Naming standard followed
- Repository created
- Image pushed successfully
- Azure RBAC configured
- Managed Identity configured
- Image versioned
- Old images cleaned
- Network security configured