# RovaAI – AI-Powered QA Platform Evaluation

A practical QA portfolio project evaluating **RovaAI** using real e-commerce workflows on **Daraz.lk**. The project demonstrates test planning, test design, AI-assisted test execution, result analysis, and evidence-based reporting.

## Project at a glance

| Item | Details |
|---|---|
| Application under test | [Daraz.lk](https://www.daraz.lk/) |
| QA platform | [RovaAI](https://app.rova.qa/) |
| Test environment | Staging Env (RovaAI project: Ecommerce WebApp) |
| Execution scope documented | 2 suites, 22 test goals |
| Portfolio focus | Functional, negative, edge-case and workflow validation |
| Execution window | 20–21 November 2026 |

## Execution summary

| Suite | Test goals | Passed | Failed | Pending | Completion |
|---|---:|---:|---:|---:|---:|
| Core Shopping Flow Validation | 10 | 10 | 0 | 0 | 100% |
| Negative & Edge Case Scenarios | 12 | 10 | 2 | 0 | 100% |
| **Total** | **22** | **20** | **2** | **0** | **100%** |

**Interpretation matters:** the two goals marked Failed in the Negative & Edge Case suite were blocked by an Alibaba Cloud WAF interstitial and a slider CAPTCHA. They are recorded as tool-reported failures, but neither establishes a confirmed application defect. See the [execution report](04-test-execution/execution-report.md) and [limitations analysis](06-tool-evaluation/limitations-and-observations.md).

## Repository guide

- [Project overview](01-project-overview/project-overview.md): context, objectives, scope and approach.
- [Test plan](02-test-planning/test-plan.md): strategy, environment, execution approach and risks.
- [Test cases](03-test-design/test-cases.md): the 22 documented test goals and expected behaviours.
- [Execution report](04-test-execution/execution-report.md): run references, results and detailed observations.
- [RovaAI evaluation](06-tool-evaluation/limitations-and-observations.md): platform observations and automation constraints.

## Main execution evidence

- [Core Shopping Flow – complete run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785)
- [Negative & Edge Case – complete run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)

Individual RovaAI result links are included in the execution report.

## Skills demonstrated

- Translating e-commerce user journeys into testable scenarios.
- Designing positive, negative, boundary and edge-condition coverage.
- Reviewing AI-driven browser execution and test evidence.
- Distinguishing application behaviour from environment and automation limitations.
- Reporting results transparently without overstating defects or coverage.

## Scope boundaries

This is a black-box evaluation of selected Daraz.lk user-facing workflows, not a full security, API, performance, accessibility or production-readiness assessment. No checkout or payment was completed. Logged-out Add to Cart / Buy Now checks were limited to verifying the authentication prompt or redirect.

Results are specific to the recorded test sessions and environment; they are not a guarantee of overall application quality.

---
*Prepared as a hands-on QA portfolio project. Test outcomes are reported as observed in the linked RovaAI runs.*
