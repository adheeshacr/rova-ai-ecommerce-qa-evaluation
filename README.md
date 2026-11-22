# RovaAI – AI-Powered QA Platform Evaluation

A practical QA portfolio project evaluating **RovaAI** using real e-commerce workflows on **Daraz.lk**. The project demonstrates test planning, test design, AI-assisted test execution, result analysis, and evidence-based reporting.

## Project at a glance

| Item | Details |
|---|---|
| Application under test | [Daraz.lk](https://www.daraz.lk/) |
| QA platform | [RovaAI](https://app.rova.qa/) |
| Test environment | Staging Env (RovaAI project: Ecommerce WebApp) |
| Scope | 2 suites, 22 distinct test goals |
| Visible execution records | 23 (includes a duplicate Core category-dropdown execution) |
| Portfolio focus | Functional, negative, edge-case and workflow validation |
| Execution window | 20–21 November 2026 |

## Execution summary and reporting note

| Suite | Distinct test goals | Visible execution records | Reported result |
|---|---:|---:|---|
| Core Shopping Flow Validation | 10 | 11 | Shared report: 10 passed, 1 failed (90.91%); separate run-statistics panel: 10 passed, 0 failed |
| Negative & Edge Case Scenarios | 12 | 12 | 10 passed, 2 failed; 100% completion |

The Core suite's shared report lists the category-dropdown scenario twice, once passed (749.3s) and once failed (894.0s). The separate statistics panel supplied earlier showed 10/10 passed. This conflict is documented in the [execution report](04-test-execution/execution-report.md) rather than hidden or averaged away. Counting visible records across both suites gives 20 passed and 3 failed; because one Core goal is duplicated and its sources conflict, this is not presented as a unique-goal pass rate.

The two Negative & Edge Case failures were blocked by an Alibaba Cloud WAF interstitial and a slider CAPTCHA. The failed Core dropdown replay did not find the control expected by the test in the tested UI. These are recorded as inconclusive/environment, automation or test-design observations—not confirmed application defects.

## Repository guide

- [Project overview](01-project-overview/project-overview.md): context, objectives, scope and approach.
- [Test plan](02-test-planning/test-plan.md): strategy, environment, execution approach and risks.
- [Test cases](03-test-design/test-cases.md): the 22 documented test goals and expected behaviours.
- [Execution report](04-test-execution/execution-report.md): run references, results and analysis.
- [Defect and investigation log](05-defect-management/observations-and-investigation.md): observations distinguished from confirmed defects.
- [RovaAI evaluation](06-tool-evaluation/limitations-and-observations.md): platform observations and automation constraints.
- [Evidence index](evidence/evidence-index.md): suite runs, individual results and replays.

## Main execution evidence

- [Core Shopping Flow – run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785)
- [Core Shopping Flow – shared report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite)
- [Negative & Edge Case – run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)

## Skills demonstrated

- Translating e-commerce user journeys into testable scenarios.
- Designing positive, negative, boundary and edge-condition coverage.
- Reviewing AI-driven browser execution and test evidence.
- Distinguishing application behaviour from environment and automation limitations.
- Reconciling inconsistent test reports and documenting evidence limitations.
- Reporting results transparently without overstating defects or coverage.

## Scope boundaries

This is a black-box evaluation of selected Daraz.lk user-facing workflows, not a full security, API, performance, accessibility or production-readiness assessment. No checkout or payment was completed. Logged-out Add to Cart / Buy Now checks were limited to verifying the authentication prompt or redirect.

Results are specific to the recorded test sessions and environment; they are not a guarantee of overall application quality. No screenshots have been embedded yet; available RovaAI reports and replay links are indexed in the evidence file.

---
*Prepared as a hands-on QA portfolio project. Test outcomes and reporting limitations are stated against the linked RovaAI evidence.*
