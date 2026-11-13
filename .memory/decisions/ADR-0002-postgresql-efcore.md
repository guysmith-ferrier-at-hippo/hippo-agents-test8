---
id: ADR-0002
title: Use PostgreSQL with Entity Framework Core for data persistence
component: database
domain: persistence
tags:
- postgresql
- efcore
- persistence
status: accepted
created: '2026-11-13'
updated: '2026-11-13'
depends_on:
- ASSUME-0002
- ADR-0001
supported_by: []
---

# ADR-0002: PostgreSQL and Entity Framework Core for Data Persistence

## Context
The platform manages transactional application submissions, case audit data, and state transitions. The data store must provide ACID transactions, relational referential integrity, strong indexing, and seamless integration with .NET 8.

## Options Considered
1. **PostgreSQL with Entity Framework Core**: Robust open-source relational database with first-class .NET driver (`Npgsql.EntityFrameworkCore.PostgreSQL`), strong JSON support, and cloud portability.
2. **Microsoft SQL Server with EF Core**: Proven enterprise database, but carries licensing costs and lower portability across generic Linux container hosting.
3. **Document Database (MongoDB / Cosmos DB)**: Highly flexible document schema, but lacks relational integrity constraints needed for regulatory casework and audit logs.

## Decision
We select PostgreSQL 16 as the relational database engine and Entity Framework Core (EF Core 8) as the Object-Relational Mapper (ORM). Database schema changes are managed via code-first EF Core Migrations checked into version control.

## Consequences
- **Positive**: Full ACID transactional guarantees with zero proprietary licensing cost.
- **Positive**: Code-first migrations provide automated, traceable schema evolutions.
- **Positive**: First-class JSONB column support allows structured audit metadata when needed.
- **Negative**: Complex query optimization requires profiling generated SQL statements.
- **Negative**: Local development environments require PostgreSQL running locally or in Docker.