# RovaAI – AI-Powered QA Platform Evaluation

A practical QA portfolio project evaluating **RovaAI** using real e-commerce workflows on **Daraz.lk**. The project demonstrates test planning, test design, AI-assisted test execution, result analysis, and evidence-based reporting.

## Project at a glance

| Item | Details |
|---|---|
| Application under test | [Daraz.lk](https://www.daraz.lk/) |
| QA platform | [RovaAI](https://app.rova.qa/) |
| Test environment | Staging Env (RovaAI project: Ecommerce WebApp) |
| Project progress | 5 of 6 planned suites executed and documented |
| Scope (completed suites) | 5 suites, 52 distinct test goals |
| Visible execution records | 53 (includes a duplicate Core category-dropdown execution) |
| Portfolio focus | Functional, negative, edge-case and workflow validation |
| Execution window | 20–22 November 2026 |

## Execution summary and reporting note

| Suite | Distinct test goals | Visible execution records | Reported result |
|---|---:|---:|---|
| Core Shopping Flow Validation | 10 | 11 | Shared report: 10 passed, 1 failed (90.91%); separate run-statistics panel: 10 passed, 0 failed |
| Negative & Edge Case Scenarios | 12 | 12 | 10 passed, 2 failed; 100% completion |
| Product Details & Product Selection | 10 | 10 | 10 passed, 0 failed; 100% completion. PDS-08 and PDS-10 needed manual follow-up; see execution report |
| Search, Filters & Sorting | 10 | 10 | 10 passed, 0 failed; 100% completion. SFS-09 failed manual verification; SFS-05 and SFS-07 confirmed manually; see execution report |
| Shopping Cart & Wishlist | 10 | 10 | 2 passed, 8 failed; 100% completion. The 8 failures were blocked by Daraz.lk's login requirement, not confirmed defects; cart functionality beyond login unverified; see execution report |

The Core suite's shared report lists the category-dropdown scenario twice, once passed (749.3s) and once failed (894.0s). The separate statistics panel supplied earlier showed 10/10 passed. This conflict is documented in the [execution report](04-test-execution/execution-report.md) rather than hidden or averaged away. Counting visible RovaAI records across all five suites gives 42 passed and 11 failed; because one Core goal is duplicated and its sources conflict, this is not presented as a unique-goal pass rate.

**Automated results and manual verification are tracked separately.** The "Reported result" column above shows RovaAI statuses. Manual follow-up can change how a RovaAI pass should be interpreted: for example, SFS-09 (multiple filters) was passed by RovaAI but failed manual verification because two brand filters could not be kept applied together, PDS-08 was reclassified as an expected-result mismatch, and the eight Suite 5 failures were classified as blocked by authentication rather than application defects. For this reason no single combined pass rate is published; see the [execution report](04-test-execution/execution-report.md) for both views.

The two Negative & Edge Case failures were blocked by an Alibaba Cloud WAF interstitial and a slider CAPTCHA. The failed Core dropdown replay did not find the control expected by the test in the tested UI. These are recorded as inconclusive/environment, automation or test-design observations—not confirmed application defects. The SFS-09 manual failure is pending requirement clarification and is also not a confirmed defect. Suite 5 did not test cart or wishlist functionality beyond the authentication boundary.

## Repository guide

- [Project overview](01-project-overview/project-overview.md): context, objectives, scope and approach.
- [Test plan](02-test-planning/test-plan.md): strategy, environment, execution approach and risks.
- [Test cases](03-test-design/test-cases.md): the 52 documented test goals and expected behaviours.
- [Execution report](04-test-execution/execution-report.md): run references, results and analysis.
- [Defect and investigation log](05-defect-management/observations-and-investigation.md): observations distinguished from confirmed defects.
- [RovaAI evaluation](06-tool-evaluation/limitations-and-observations.md): platform observations and automation constraints.
- [Evidence index](evidence/evidence-index.md): suite runs, individual results and replays.

## Main execution evidence

- [Core Shopping Flow – run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785)
- [Core Shopping Flow – shared report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite)
- [Negative & Edge Case – run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)
- [Product Details & Product Selection – run](https://app.rova.qa/suites/runs/48f0f4d5-be13-46e5-8057-1512967b0ba9)
- [Search, Filters & Sorting – run](https://app.rova.qa/suites/runs/8d8e3e97-4286-4e44-80d3-6f2d2c360092)
- [Shopping Cart & Wishlist – run](https://app.rova.qa/suites/runs/31e5374f-a403-4b20-9dfc-dd5f20cc30fe)

## Skills demonstrated

- Translating e-commerce user journeys into testable scenarios.
- Designing positive, negative, boundary and edge-condition coverage.
- Reviewing AI-driven browser execution and test evidence.
- Distinguishing application behaviour from environment and automation limitations.
- Reconciling inconsistent test reports and documenting evidence limitations.
- Reporting results transparently without overstating defects or coverage.

## Scope boundaries

This is a black-box evaluation of selected Daraz.lk user-facing workflows, not a full security, API, performance, accessibility or production-readiness assessment. No checkout or payment was completed. Logged-out Add to Cart / Buy Now checks were limited to verifying the authentication prompt or redirect.

Results are specific to the recorded test sessions and environment; they are not a guarantee of overall application quality. Manual verification screenshots for Suites 3, 4 and 5 are stored in the evidence folder; RovaAI reports, replay links and manual reproduction links are indexed in the evidence file.

---
*Prepared as a hands-on QA portfolio project. Test outcomes and reporting limitations are stated against the linked RovaAI evidence.*
