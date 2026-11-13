---
id: DD-0001
title: Adopt GOV.UK Design System component macros and tokens
component: frontend
domain: design
tags:
- gds
- design-tokens
- accessibility
status: accepted
created: '2026-11-13'
updated: '2026-11-13'
depends_on:
- ASSUME-0003
- ADR-0003
supported_by: []
---

# DD-0001: Adoption of GOV.UK Design System Component Macros and Design Tokens

## Context
The service delivers citizen and caseworker web journeys. Visual presentation must maintain high contrast, predictable navigation patterns, and strict adherence to public digital design standards.

## Options Considered
1. **Custom CSS / Utility Framework (Tailwind CSS)**: High flexibility, but requires developing and maintaining custom accessibility and focus ring mechanics from scratch.
2. **Official GOV.UK Frontend (GDS) Distribution**: Standard tokens, pre-tested accessible components (buttons, form inputs, error summaries, breadcrumbs), and guaranteed compliance with UK government digital standards.
3. **Third-Party Component Library (Bootstrap)**: Generic appearance that lacks UK public sector familiarity and requires significant tweaking to satisfy WCAG 2.2 focus standards.

## Evaluation
The GOV.UK Design System provides pre-built, thoroughly tested accessible components designed specifically for public sector usability. It natively satisfies WCAG 2.2 AA requirements, including the mandated `#ffdd00` focus ring styling.

## Decision
Adopt official GOV.UK Frontend assets, component markup patterns, and functional colour tokens. Never hardcode custom hex codes or override GDS focus states.

## Consequences
- **Positive**: Direct alignment with government accessibility guidelines and high citizen trust.
- **Positive**: Pre-validated keyboard navigation, screen reader announcements, and error states.
- **Negative**: Visual customisation is intentionally constrained to official token parameters.