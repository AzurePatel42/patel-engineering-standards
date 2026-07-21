# Azure Container Apps (ACA)

## Overview

Azure Container Apps (ACA) is a fully managed serverless container platform for running modern applications and microservices without managing Kubernetes infrastructure.

It allows developers to deploy containerized applications with automatic scaling, built-in networking, and seamless integration with Azure services.

Azure Container Apps is the preferred hosting platform for PPST-based services.

---

# Engineering Objectives

Azure Container Apps should provide:

- Fully managed container hosting
- Automatic scaling
- High availability
- Secure application deployment
- Simplified operations
- Seamless Azure integration

---

# Core Architecture

A typical Azure Container Apps deployment consists of:

- Azure Container Registry (ACR)
- Azure Container Apps Environment
- Azure Container App
- Managed Identity
- Azure Key Vault
- Azure Storage
- Azure Monitor

Architecture:

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

Managed Identity

↓

Key Vault

↓

Azure Storage

---

# Container Apps Environment

Every Container App runs inside a Container Apps Environment.

The environment provides:

- Networking
- Scaling
- Logging
- Service discovery
- Shared infrastructure

Multiple applications can share one environment.

Example:

```
Container Apps Environment

├── inventory-api
├── data-ingestion
├── retrieval-service
├── auth-service
└── cost-intelligence
```

---

# Scaling

Azure Container Apps automatically scales applications.

Scaling can be based on:

- HTTP requests
- CPU utilization
- Memory usage
- Queue length
- Custom events

Container Apps can scale down to zero when idle.

---

# Revisions

Every deployment creates a new revision.

Benefits:

- Safe deployments
- Rollbacks
- Blue/Green deployments
- Traffic splitting

Production deployments should use revisions rather than replacing running containers.

---

# Networking

Azure Container Apps supports:

- Internal environments
- External ingress
- Virtual Networks
- Private Endpoints
- Custom Domains
- HTTPS

Only expose services that require public access.

---

# Authentication

Applications should authenticate using:

- Managed Identity
- Microsoft Entra ID
- Azure RBAC

Avoid storing credentials inside containers.

---

# Secrets

Secrets should be retrieved from Azure Key Vault.

Examples:

- OpenAI API Key
- PostgreSQL password
- Redis password
- Storage credentials
- JWT signing key

Applications should never contain hardcoded secrets.

---

# Monitoring

Azure Container Apps integrates with:

- Azure Monitor
- Log Analytics
- Application Insights

Monitor:

- CPU
- Memory
- Requests
- Response time
- Errors
- Container restarts

---

# Security Best Practices

- Use Managed Identity
- Store secrets in Key Vault
- Use Azure RBAC
- Pull images from Azure Container Registry
- Minimize public ingress
- Enable HTTPS
- Monitor application health

---

# PPST Azure Container Apps Standard

Every PPST service should:

- Build a Docker image
- Push the image to Azure Container Registry
- Deploy to Azure Container Apps
- Authenticate using Managed Identity
- Retrieve secrets from Key Vault
- Store files in Azure Storage
- Enable monitoring and logging
- Follow semantic versioning

Typical deployment flow:

PPST Service

↓

Docker Build

↓

Azure Container Registry

↓

Azure Container Apps

↓

Managed Identity

↓

Key Vault

↓

Azure Storage

---

# Engineering Checklist

- Docker image built
- Image pushed to Azure Container Registry
- Container App created
- Managed Identity enabled
- Key Vault connected
- Azure Storage configured
- HTTPS enabled
- Monitoring configured
- Scaling configured
- Deployment tested