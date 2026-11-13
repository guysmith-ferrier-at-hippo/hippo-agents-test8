---
id: KB-0001
title: Clean Architecture layer boundaries and dependency rules
component: all
domain: architecture
tags:
- dotnet8
- clean-architecture
- dependency-injection
status: validated
created: '2026-11-13'
updated: '2026-11-13'
depends_on:
- ADR-0001
supported_by: []
---

# .NET 8 Clean Architecture Layer Boundaries and Dependency Rules

## Context & Key Insights
When implementing Clean Architecture in .NET 8 solutions, dependency management must strictly point inwards. Violating layer boundaries causes coupling between database logic, HTTP handling, and domain business rules.

## Architectural Layer Rules
1. **Domain Layer (`Hippo.Platform.Domain`)**:
   - Contains core entities, value objects, domain exceptions, and domain repository interfaces.
   - Must have **zero** dependencies on external packages, database libraries (no EF Core references), or ASP.NET Core libraries.
2. **Application Layer (`Hippo.Platform.Application`)**:
   - Contains business logic use cases, CQRS commands/queries, MediatR or direct handlers, DTOs, and interface contracts.
   - Depends only on the `Domain` layer.
3. **Infrastructure Layer (`Hippo.Platform.Infrastructure`)**:
   - Implements interfaces defined in Application/Domain (e.g., `ApplicationDbContext`, repository implementations, email sender, clock).
   - Depends on `Application` and `Domain`.
4. **Presentation / Web Layer (`Hippo.Platform.Web`)**:
   - Entry point containing Razor Pages, Controllers, middleware configuration, and GDS assets.
   - Depends on `Application` and `Infrastructure` for dependency injection wiring at startup.

## Testing Strategy by Layer
- **Domain & Application**: High-speed unit tests using xUnit, FluentAssertions, and NSubstitute.
- **Infrastructure**: Integration tests using WebApplicationFactory and Testcontainers for PostgreSQL.
- **Web**: Playwright tests verifying complete user journeys and accessibility checks.