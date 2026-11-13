---
id: ASSUME-0001
title: Target .NET 8 LTS runtime for core services
component: backend
domain: runtime
tags:
- dotnet8
- csharp
- runtime
status: validated
created: '2026-11-13'
updated: '2026-11-13'
depends_on: []
supported_by: []
---

# Technical Assumption: .NET 8 LTS Target Runtime

## Context
The project repository contains a `.gitignore` tailored for modern .NET Core and ASP.NET solutions. The architecture needs a stable runtime with long-term enterprise support.

## Assumption
The application targets .NET 8 (LTS) using C# 12 for all application services, domain logic, and web endpoints.

## Impact If False
If a different runtime (such as .NET 9 STS or Node.js) is required, project dependencies, Docker base images, and build pipelines must change.

## Validation Method
Confirm runtime version in the solution root directory `.csproj` files and Docker build configuration.