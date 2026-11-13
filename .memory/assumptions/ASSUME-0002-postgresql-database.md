---
id: ASSUME-0002
title: Use PostgreSQL as primary relational database
component: database
domain: persistence
tags:
- postgresql
- efcore
- database
status: validated
created: '2026-11-13'
updated: '2026-11-13'
depends_on: []
supported_by: []
---

# Architecture Assumption: PostgreSQL Relational Database

## Context
The service requires ACID compliance, relational integrity, strong indexing capabilities, and open-source licensing.

## Assumption
PostgreSQL 16 is the primary relational database system, accessed through Entity Framework Core (EF Core) with Npgsql provider.

## Impact If False
If a proprietary database such as Microsoft SQL Server or Oracle is required, connection drivers, migrations, and docker-compose configurations must be updated.

## Validation Method
Verify database connection string configuration, migration snapshot classes, and container orchestration files.