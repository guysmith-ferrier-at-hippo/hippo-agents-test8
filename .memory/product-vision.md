# 🧭 Product Vision Document

## 1. Product Overview

**Product Name:**  
Hippo Digital Service Platform (HDSP)

**Author / Owner:**  
Hippo Digital Product & Architecture Team (`guysmith-ferrier-at-hippo`)

---

## 2. Vision Statement

Empower multidisciplinary public service delivery teams to build, validate, and operate secure, accessible, and compliant citizen services through modern cloud technology and verified delivery patterns.

---

## 3. Problem Statement

Public and enterprise organizations must build compliant digital services that meet strict accessibility, performance, and security standards.

- **Who experiences the problem?**  
  Service owners, digital delivery teams, and citizens who use digital government services.
- **What is the impact of the problem today?**  
  Teams repeat boilerplate setup, risk regulatory non-compliance with WCAG standards, and experience slow delivery cycles.
- **Why does solving this matter?**  
  A unified platform baseline reduces delivery cost, prevents accessibility failures, and provides consistent citizen outcomes.

---

## 4. Target Users / Audiences

| Persona | Description | Key Needs / Goals |
|---|---|---|
| **Citizen User** | End user submitting requests or accessing digital public services. | Simple, accessible, fast, and secure user journey on any device. |
| **Service Operator** | Internal staff processing applications and reviewing casework data. | Clear data views, reliable state transitions, and responsive administrative tools. |
| **Delivery Engineer** | Software developer creating features and maintaining service components. | Robust .NET architecture, clear domain boundaries, and fast automated test suites. |
| **Assurance Lead** | Governance and quality manager auditing security and accessibility. | Automated compliance verification, audit logs, and clear traceability. |

---

## 5. Product Goals & Outcomes

| Goal | Metric / KPI | Desired Outcome |
|---|---|---|
| **High Accessibility** | WCAG 2.2 AA automated and manual audit pass rate | 100% compliance with zero high or critical accessibility defects. |
| **Rapid Feature Delivery** | Time to deploy new verified workflows | Reduce deployment cycle time to under 15 minutes via CI/CD. |
| **High Reliability** | Service uptime and API error rate | 99.9% uptime with API latency under 200 ms for 95% of requests. |
| **Data Integrity** | Transaction failure and data corruption events | Zero data loss through ACID transactional persistence. |

---

## 6. Key Features / Capabilities

- **Accessible Service Frontend**: Responsive user interface built with GOV.UK Design System patterns and validated WCAG 2.2 AA components.
- **Clean Architecture Core**: Decoupled domain model, command/query handlers, and business validation layers in .NET 8.
- **Secure Transaction Processing**: Encrypted data persistence with PostgreSQL and Entity Framework Core.
- **Automated Verification Pipeline**: Complete automated test coverage including unit, integration, end-to-end, and accessibility test suites.
- **Operational Audit Log**: Traceable logging of critical service operations and configuration changes.

---

## 7. Value Proposition

| For (user type) | Who want to (need) | Our product (solution) | Unlike (alternative) |
|---|---|---|---|
| Public Sector Delivery Teams | Deliver compliant citizen services quickly | Provides a validated .NET 8 Clean Architecture baseline | Disjointed custom boilerplates without built-in compliance |
| Citizens & Service Users | Complete digital requests without friction | Provides an accessible, mobile-responsive GDS interface | Inconsistent, inaccessible legacy portals |
| Engineering Teams | Maintain clean code and high automated test coverage | Provides modular layers and comprehensive test strategy | Monolithic legacy architectures with low testability |

---

## 8. Constraints / Assumptions

- **ASSUME-0001**: Target .NET 8 LTS runtime for core services ([ASSUME-0001](.memory/assumptions/ASSUME-0001-dotnet8-target-runtime.md)).
- **ASSUME-0002**: Use PostgreSQL as primary relational database ([ASSUME-0002](.memory/assumptions/ASSUME-0002-postgresql-database.md)).
- **ASSUME-0003**: Adhere to WCAG 2.2 AA and GDS design tokens ([ASSUME-0003](.memory/assumptions/ASSUME-0003-gds-wcag-accessibility.md)).
- **ASSUME-0004**: Use GitHub Actions for continuous integration and delivery ([ASSUME-0004](.memory/assumptions/ASSUME-0004-github-actions-cicd.md)).
- **Technical Constraint**: All service components must run in Linux container environments.
- **Policy Constraint**: Code and documentation must adhere to ASD-STE100 Simplified Technical English standards.

---

## 9. Success Metrics

- **Primary metric(s):**  
  - 100% pass rate on WCAG 2.2 AA automated axe-core accessibility suites.  
  - 85%+ test code coverage across core domain and application layers.
- **Secondary metric(s):**  
  - Zero critical security vulnerabilities in SAST and dependency audits.  
  - Mean time to recovery (MTTR) under 30 minutes in staging and production.
- **Qualitative indicators:**  
  - Clear user feedback praising clarity, speed, and ease of use.  
  - Seamless developer onboarding through comprehensive specification conventions.

---

## 10. Stakeholders

| Role | Name / Team | Interest / Contribution |
|---|---|---|
| **Product Owner** | Hippo Digital Product Leadership | Service vision, roadmap prioritization, and business value. |
| **Technical Lead** | Guy Smith-Ferrier (`guysmith-ferrier-at-hippo`) | Architecture standards, technical decisions, and code governance. |
| **Quality & Test Lead** | Quality Assurance Engineering Team | Test strategy enforcement, defect prevention, and test automation. |
| **User Experience Lead** | Design & Accessibility Specialists | User research, design tokens, and GDS design compliance. |

---

## 11. Risks & Open Questions

- **Risk 1**: E2E test execution flakiness in CI pipelines due to asynchronous browser state.  
  *Mitigation*: Enforce deterministic state-based waits in Playwright test suites.
- **Risk 2**: Evolving accessibility criteria and screen reader variations across devices.  
  *Mitigation*: Combine automated axe-core CI assertions with periodic manual assistive tech audits.
- **Open Question**: Will future integrations require event streaming (such as Apache Kafka or RabbitMQ) for cross-service events?  
  *Path to Validate*: Monitor transaction volumes and define ADR if asynchronous integration is needed.

---

## 12. References

- [GDS Design System Documentation](https://design-system.service.gov.uk)
- [.NET 8 Enterprise Architecture Guidance](https://learn.microsoft.com/en-us/dotnet/architecture/)
- [Project Assumptions Index](.memory/assumptions/)
- [Specification Conventions](.memory/specification-conventions.md)
