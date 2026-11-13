---
id: ASSUME-0003
title: Adhere to WCAG 2.2 AA and GDS design tokens
component: frontend
domain: design
tags:
- gds
- accessibility
- wcag
status: validated
created: '2026-11-13'
updated: '2026-11-13'
depends_on: []
supported_by: []
---

# Design Assumption: WCAG 2.2 AA Compliance and GDS Design Tokens

## Context
The service delivers public sector and enterprise citizen-facing web workflows that must follow statutory accessibility regulations.

## Assumption
The user interface adheres to WCAG 2.2 Level AA accessibility standards, implementing GOV.UK Design System (GDS) tokens, typography, and accessible component patterns.

## Impact If False
Failure to meet accessibility standards could result in non-compliance with public sector digital accessibility regulations and legal challenges.

## Validation Method
Run automated axe-core accessibility checks in Playwright test suites and conduct manual keyboard navigation audits.