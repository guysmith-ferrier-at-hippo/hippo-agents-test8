---
id: ADR-0003
title: Use GOV.UK Design System with ASP.NET Core Razor Pages
component: frontend
domain: frontend
tags:
- gds
- razor-pages
- ui
- accessibility
status: accepted
created: '2026-11-13'
updated: '2026-11-13'
depends_on:
- ASSUME-0003
- ADR-0001
supported_by: []
---

# ADR-0003: GOV.UK Design System (GDS) with ASP.NET Core Razor Pages

## Context
The service delivers user-facing transactional and informational workflows. The user interface must comply with UK public sector design guidelines, pass WCAG 2.2 Level AA accessibility mandates, and provide fast server-rendered performance across mobile and desktop devices.

## Options Considered
1. **Single Page Application (SPA) with React/Vue and GDS React**: High client-side interactivity, but increases JavaScript bundle size, adds build tool complexity, and complicates initial server rendering for accessibility.
2. **ASP.NET Core Razor Pages with GDS Assets**: Server-rendered HTML pages using GOV.UK Frontend compiled CSS/JS and semantic HTML. Lightweight, highly performant, accessible by default, and seamlessly integrated into the .NET pipeline.
3. **Blazor WebAssembly**: Rich C# client-side interactivity, but incurs substantial initial WebAssembly download latency.

## Decision
We select ASP.NET Core Razor Pages combined with official GOV.UK Frontend distribution assets (styles, markup macros, accessible JavaScript components) for all user-facing web interfaces.

## Consequences
- **Positive**: Strict conformance to GDS design patterns and WCAG 2.2 AA accessibility out of the box.
- **Positive**: Fast server-side rendering with zero client-side JavaScript framework bloat.
- **Positive**: Standard form validation and CSRF protection built into ASP.NET Core.
- **Negative**: Dynamic client-side asynchronous interactions require targeted vanilla JavaScript or progressive enhancement fetch calls rather than rich reactive state frameworks.