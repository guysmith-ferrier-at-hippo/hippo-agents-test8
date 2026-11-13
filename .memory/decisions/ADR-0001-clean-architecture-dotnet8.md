---
id: ADR-0001
title: Adopt Clean Architecture pattern with .NET 8
component: backend
domain: architecture
tags:
- architecture
- clean-architecture
- dotnet8
status: accepted
created: '2026-11-13'
updated: '2026-11-13'
depends_on:
- ASSUME-0001
supported_by: []
---

# ADR-0001: Clean Architecture Pattern with .NET 8

## Context
The Hippo Digital Service Platform requires maintainable domain logic, high automated testability, and decoupled technology dependencies. Monolithic architectures with direct database access from UI layers create brittle codebases that are difficult to refactor and test.

## Options Considered
1. **Vertical Slice Architecture**: Feature-centric organisation. Good for small services, but can lead to code duplication across complex domain models.
2. **Traditional 3-Tier Layered Architecture**: Presentation, Business Logic, Data Access. Tightly couples the domain model to database schema abstractions.
3. **Clean Architecture (Onion / Hexagonal)**: Domain entities and rules at the core, Application layer coordinating business logic, Infrastructure and Presentation as external adapters.

## Decision
We adopt Clean Architecture with .NET 8 and C# 12. The project contains four primary layers:
- `Domain`: Enterprise entities, value objects, domain events, and repository interfaces. No external dependencies.
- `Application`: Command and Query handlers (CQRS), business validation, and interface definitions.
- `Infrastructure`: Database persistence (EF Core), external API clients, file storage, and system time services.
- `Presentation / Web`: ASP.NET Core Razor Pages and Web API controllers, view models, and HTTP pipeline configuration.

## Consequences
- **Positive**: Core domain logic is completely isolated from database engines and web frameworks.
- **Positive**: Unit testing domain and application rules does not require database or web server mocks.
- **Negative**: Requires additional boilerplate mapping and interface definitions between layers.
- **Negative**: Developers must maintain strict dependency boundaries pointing inwards towards the Domain.