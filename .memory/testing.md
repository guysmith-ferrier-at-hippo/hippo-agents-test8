# Hippo Digital Service Platform — Test Strategy

## Overview

This test strategy defines the automated and manual quality verification standards for the Hippo Digital Service Platform (HDSP). The strategy enforces quality across all delivery phases, ensuring continuous compliance with accessibility mandates, security baselines, and performance targets.

## Test Environments & Access

- **Environments:**  
  - `Local`: Developer workstation running .NET 8 SDK and Docker Compose for local PostgreSQL instances.
  - `CI (GitHub Actions)`: Automated ephemeral test runners executing unit, integration, and static security checks on every pull request.
  - `Staging`: Cloud-hosted preview environment mirroring production configurations for automated end-to-end regression, performance benchmarks, and user acceptance testing.
  - `Production`: Live environment hosting validated releases, monitored with continuous synthetic canary transactions and OpenTelemetry telemetry.
- **Access Needs:** Ephemeral test credentials, isolated database schemas, and mock external API gateway endpoints.
- **Data Management:** Test data is generated deterministically through builder classes. Database integration tests use Testcontainers to spin up isolated disposable PostgreSQL instances per test run.
- **CI/CD Integration:** Every pull request runs the full unit, integration, accessibility, and SAST security suites before merge approval is granted.

## Testing Approach

| Level | Scope / Objective | Tools / Frameworks | Success Criteria | Responsibilities |
|---|---|---|---|---|
| **Unit** | Verify domain logic, value objects, and application command/query handlers in isolation. | xUnit, FluentAssertions, NSubstitute | Minimum 85% code coverage on Domain and Application layers. | Developers |
| **Component (Web)** | Test Razor components, partials, and isolated UI elements against user inputs and error states. | bUnit, Playwright (.NET) | All core form components render valid GDS markup and accessible states. | Developers |
| **Contract** | Verify consumer-driven API contracts between service modules and downstream consumer teams. | PactNet | 100% contract verification pass rate before downstream release. | Developers, QA |
| **Integration (Mocked)** | Test application workflows and HTTP endpoints with external dependencies mocked. | WebApplicationFactory, WireMock.Net | All external HTTP integrations mock fault states and succeed deterministically. | Developers, QA |
| **Integration (API / Events)** | Test database transactions, EF Core migrations, and live repository queries against real database engines. | Testcontainers for .NET, PostgreSQL 16 | Zero migration failures; all transactional rollbacks execute safely. | Developers, QA |
| **Acceptance (Functional)** | Validate business requirements against executable specifications and acceptance criteria. | Reqnroll (Cucumber for .NET), Playwright | 100% acceptance criteria pass for all committed user stories. | QA, Developers, Product Owner |
| **End-to-End (E2E)** | Verify complete critical citizen and caseworker journeys from browser to database. | Playwright (.NET) | Zero journey regressions in CI across Chromium, Firefox, and WebKit engines. | QA, Developers |
| **Performance (API)** | Measure throughput, error rates, and response latency under expected and peak request volumes. | k6, NBomber | 95th percentile latency < 200 ms at 1,000 requests per second with 0% error rate. | QA, DevOps, Developers |
| **Performance (Web)** | Validate Core Web Vitals, page weight, and rendering efficiency for mobile and desktop viewports. | Lighthouse CLI, Web Vitals | Lighthouse Performance score >= 90; Largest Contentful Paint (LCP) < 2.5s; Total Blocking Time (TBT) < 200ms. | Developers, QA |
| **Security** | Static Application Security Testing (SAST), Software Composition Analysis (SCA), and Dynamic Analysis (DAST). | GitHub CodeQL, Snyk, OWASP ZAP | Zero critical or high severity vulnerabilities in code or third-party dependencies. | Security Lead, Developers |
| **Accessibility** | Verify keyboard navigation, colour contrast, screen reader compatibility, and WCAG rules. | axe-core, Playwright axe integration, manual NVDA/VoiceOver audits | 100% automated pass rate for WCAG 2.2 Level AA; zero barrier issues in manual reviews. | QA, UX Lead, Developers |

## Risk & Mitigation

| Risk | Mitigation |
|---|---|
| E2E test flakiness (async state) | Use state-based waits (e.g., `WaitForSelectorAsync`, `WaitForURLAsync`); strictly ban arbitrary thread sleeps. |
| Third-party API availability | Use PactNet contract tests and WireMock server stubs for reliable offline CI execution. |
| Test data contamination | Use Testcontainers with isolated PostgreSQL instances per test class and deterministic teardown logic. |
| Browser rendering variations across platforms | Execute Playwright multi-browser test matrices inside standardized Linux container images in CI. |
| Late discovery of accessibility barriers | Run axe-core assertions as part of the local unit/component test loop before pull request submission. |

## Reviewed by

| Name | Role | Approved | Date |
|---|---|---|---|
| Quality Lead | Test Lead | [x] | 2026-11-13 |
| Guy Smith-Ferrier | Tech Lead | [x] | 2026-11-13 |
| Product Director | Product Manager | [x] | 2026-11-13 |
