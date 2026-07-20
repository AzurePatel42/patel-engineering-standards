# Azure Engineering Standards

## Identity

## Overview

Identity is the security foundation of every Azure environment. Before Azure can determine what actions are allowed, it must first verify who or what is requesting access.

Patel Engineering follows the principle:

Authenticate first. Authorize second.

Authentication establishes trust. Authorization determines permissions.

## Purpose

The Identity Standard defines how Patel Engineering authenticates:

Engineers
Applications
Services
Automation
CI/CD pipelines

This standard promotes secure, scalable, and maintainable identity management across all Azure environments.

## Design Principles

Patel Engineering follows these identity principles:

Every identity is unique.
Authentication always precedes authorization.
Human identities and workload identities remain separate.
Prefer identity-based authentication over shared secrets.
Grant the minimum access necessary.
All privileged actions must be auditable.
Identity Architecture
                    Microsoft Entra ID
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
     Engineers        Azure Services      Automation
        │                  │                  │
     User Account     Managed Identity   Service Principal
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                    Azure Resource Manager
                           │
                    Azure Resources
Identity Types
User Identity

Represents an individual engineer or administrator.

## Usage

Azure Portal
Azure CLI
Azure PowerShell
Visual Studio Code
Administrative operations
Standard
One identity per engineer
No shared administrator accounts
MFA required
Activity must be auditable

## Group Identity

Groups simplify permission management.

Instead of assigning permissions directly to users:

Users
      ↓
Groups
      ↓
Azure RBAC
      ↓
Resources
Standard

Assign permissions to groups whenever practical.

Avoid assigning permissions directly to individual users unless required.

## Managed Identity

Managed Identity is the preferred authentication method for Azure-hosted workloads.

Examples:

Azure Container Apps
Azure Functions
Virtual Machines
Logic Apps
Benefits
No passwords
No client secrets
Automatic credential rotation
Native Azure integration
Reduced attack surface
Patel Engineering Standard

Managed Identity is the default authentication mechanism for Azure services.

## Service Principal

Service Principals represent applications outside normal Azure-hosted identity scenarios.

Examples:

GitHub Actions
Terraform
Azure DevOps
Third-party integrations
Standard

Use Service Principals only when Managed Identity is unavailable or unsuitable.

## Authentication Standards

Patel Engineering requires:

Microsoft Entra ID authentication
Multi-Factor Authentication (MFA) for administrative accounts
Conditional Access where appropriate
Passwordless authentication when feasible
Secure credential lifecycle management
Human vs Workload Identity
Human Identity	Workload Identity
Engineer	Container App
Administrator	Function App
Operator	Automation
Developer	API
Support	Background Worker

These identity types must remain separate.

PPST Identity Strategy

All PPST-based services follow these rules:

Azure Container Apps authenticate using Managed Identity.
Azure Key Vault grants access through Managed Identity.
Azure Storage uses identity-based authentication whenever supported.
Azure SQL uses Microsoft Entra ID authentication where supported.
Services never contain embedded credentials.
Security Requirements

Patel Engineering requires:

No shared accounts
No credentials stored in source code
No hardcoded secrets
Least Privilege access
Identity-first authentication
Full auditability
Credential rotation when secrets cannot be avoided
Future Direction

As the platform matures, Patel Engineering may adopt:

Privileged Identity Management (PIM)
Identity Governance
Workload Identity Federation
Passwordless authentication
Just-In-Time Administration
Continuous Access Evaluation
Engineering Principles

✔ Every engineer has a unique identity.

✔ Every application has its own identity.

✔ Authentication comes before authorization.

✔ Managed Identity is preferred over secrets.

✔ Human and workload identities remain separate.

✔ Every privileged action must be traceable.

Key Takeaway

Identity establishes trust. Secure Azure environments begin by verifying who or what is requesting access before determining what that identity is allowed to do.