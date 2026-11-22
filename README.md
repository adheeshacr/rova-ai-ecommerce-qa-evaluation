# RovaAI QA Evaluation – Daraz.lk E-commerce Workflows

A hands-on QA portfolio project that evaluates **RovaAI**, an AI-assisted browser testing platform, against real customer-facing workflows on **Daraz.lk**. It covers test planning, test design, AI-assisted execution, manual verification, investigation of failed and inconsistent results, and evidence-based reporting.

## Project context

This project was carried out as part of the **Testers Connect** cohort. The test suites, executions and findings were produced through cohort collaboration; this repository documents my portfolio write-up, analysis and evidence review of that work. It is not presented as an independently completed project.

## Project at a glance

| Item | Details |
|---|---|
| Application under test | [Daraz.lk](https://www.daraz.lk/) (public, logged-out customer journeys) |
| Testing platform | [RovaAI](https://app.rova.qa/) – natural-language test goals executed by an AI browser agent |
| RovaAI project / environment | Ecommerce WebApp / Staging Env |
| Test suites | 6 planned and created; 5 run to completion, Suite 6 stopped partway for safety |
| Test goals | 62 designed; 59 produced a RovaAI result; 3 Suite 6 goals not completed |
| Execution window | 20–22 November 2026 |
| Testing approach | Black-box functional, negative and edge-case testing; manual follow-up on questionable results |
| Constraints | No sign-in, account creation, checkout, payment or order placement |

## Objectives

- Translate e-commerce user journeys into clear, testable goals.
- Execute those goals with an AI testing agent and review the evidence it produces.
- Investigate failed, blocked and inconsistent results rather than accepting tool statuses at face value.
- Distinguish application defects from authentication restrictions, test-design issues, environment controls and automation limitations.
- Evaluate RovaAI's practical strengths and limitations as a QA tool.

## Scope

**In scope:** homepage and navigation, search, filters and sorting, product detail pages and variations, logged-out cart, wishlist and checkout entry points, login form validation, quantity boundaries, invalid URLs and repeated actions.

**Out of scope:** signing in, creating accounts, checkout completion, payment, order placement, backend/API security, performance and accessibility certification. Because Daraz.lk requires a signed-in account for the cart, wishlist and checkout, **this project does not validate end-to-end checkout**.

## The six test suites

| # | Suite | Goals | Focus |
|---|---|---:|---|
| 1 | Core Shopping Flow Validation (CSF) | 10 | Homepage, search, sorting, product selection, login prompt, category navigation, responsive layout |
| 2 | Negative & Edge Case Scenarios (NEC) | 12 | Invalid and special-character input, login validation, quantity boundaries, invalid URLs, repeated submissions |
| 3 | Product Details & Product Selection (PDS) | 10 | Product page content, images, price, ratings, seller, variations, stock, navigation and refresh |
| 4 | Search, Filters & Sorting (SFS) | 10 | Keyword search, suggestions, no results, category and price filters, sorting, combined and cleared filters |
| 5 | Shopping Cart & Wishlist (SCW) | 10 | Add to cart, cart details, quantity, subtotal, removal, empty cart, wishlist access, navigation |
| 6 | Checkout & Order Management (COM) | 10 | Checkout entry, authentication, address, delivery, order summary, totals, payment methods, validation, order boundary |

## Execution summary

RovaAI statuses and manual review are reported **separately**. A RovaAI "pass" sometimes only confirmed that a login prompt appeared, and some RovaAI failures were caused by authentication or security controls rather than defects, so no single combined pass rate is published.

| Suite | RovaAI-reported result | Completion | Duration | QA interpretation |
|---|---|---:|---:|---|
| 1. Core Shopping Flow | Conflicting sources: run statistics 10/10 passed; shared report 11 records (10 passed, 1 failed) | 100% | – | Category-dropdown goal duplicated with one pass and one fail. The failed replay found no dropdown trigger; this is a test-design / requirement-to-interface mismatch. No definitive pass rate is claimed. |
| 2. Negative & Edge Cases | 10 passed, 2 failed (12 executions) | 100% | 27m 54s | Both failures were blocked by security controls (WAF HTTP 405; slider CAPTCHA). Not application defects. |
| 3. Product Details & Selection | 10 passed, 0 failed | 100% | 33m 12s | Passes qualified: PDS-02 seller listing inconsistency; PDS-08 expected result needs refinement; PDS-10 checked with browser commands. |
| 4. Search, Filters & Sorting | 10 passed, 0 failed | 100% | 9m 11s | SFS-09 (multiple brands) **failed manual verification** despite the RovaAI pass; requirement clarification needed. SFS-05/07/08 confirmed manually. |
| 5. Shopping Cart & Wishlist | 2 passed, 8 failed | 100% | 15m 59s | All 8 failures were blocked by login. Cart and wishlist functionality beyond login remains unverified. |
| 6. Checkout & Order Management | 5 passed, 2 failed (7 completed); 1 stopped partway; 2 not run | 70% (reported) | Stopped at ~24m 35s | Run stopped for safety. Only the login requirement was confirmed; **no checkout functionality was verified**. |

Across Suites 1–6 there are **60 visible RovaAI execution records** (including the duplicated Suite 1 record): **47 passed and 13 failed**, with **3 Suite 6 goals not completed**. This is a record count, not a quality score.

## Key findings

- **No confirmed Daraz.lk application defects** were established. Every failure and anomaly was investigated and classified.
- **Authentication boundary:** logged-out users cannot add to cart, view the cart, use the wishlist or reach checkout. There was no guest checkout during testing. This blocked most of Suites 5 and 6.
- **Requirement clarification needed – multi-brand filtering (SFS-09):** selecting a second brand replaced the first, and only the last brand was applied, although the URL contained both. Brand combined with another filter type worked.
- **Test-design mismatches:** the Suite 1 category-dropdown goal assumed a control that was not present in the tested interface; PDS-08's expected result ("cannot be selected") did not match Daraz's "selectable but not purchasable" design.
- **Security and environment controls:** a WAF interstitial and a slider CAPTCHA prevented two negative tests from reaching the application.
- **Data observations:** a product title/description capacity mismatch (PDS-02) and an extreme seller price outlier (SFS-08) – listing data, not platform defects.
- **Minor observations:** `www.daraz.lk/wishlist/` and `www.daraz.lk/cart/` show a generic error page, while the working routes (`my.daraz.lk/wishlist/index`, `cart.daraz.lk/cart`) redirect to login.

## RovaAI evaluation – summary

**Strengths**

- Executes natural-language goals in a real browser without writing automation code.
- Produces per-goal step timelines, agent reasoning, video recordings, network data and suite-level reports.
- Handled straightforward search, product, filtering and sorting checks quickly (Suite 4 in 9 minutes 11 seconds).

**Limitations**

- Status labels need human review: some passes were misleading (SFS-09) or based on thin evidence (SFS-05, SFS-07); authentication-blocked goals were reported as failures (Suite 5) or as passes (Suite 6).
- Could not proceed past WAF and CAPTCHA controls.
- Repetitive behaviour when the login pop-up loaded blank, adding long, looping steps.
- One report listed a duplicated execution with conflicting outcomes (Suite 1).
- **Safety-boundary concerns:** in Suites 5 and 6 the agent opened registration and login flows despite instructions not to; in Suite 5 it selected an adult product and clicked an age confirmation; in Suite 6 it attempted to type into a sign-up phone-number field, and the run was stopped. No account was created and no SMS verification, payment or order occurred, but whether any text was entered in that final attempt could not be fully confirmed.

Full detail: [RovaAI evaluation](06-tool-evaluation/limitations-and-observations.md).

## Evidence

- [Evidence index](evidence/evidence-index.md) – all suite run reports, individual result links, replays, manual reproduction links and screenshots.
- Suite run reports:
  - [Core Shopping Flow – run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785) · [shared report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite)
  - [Negative & Edge Case – run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)
  - [Product Details & Product Selection – run](https://app.rova.qa/suites/runs/48f0f4d5-be13-46e5-8057-1512967b0ba9)
  - [Search, Filters & Sorting – run](https://app.rova.qa/suites/runs/8d8e3e97-4286-4e44-80d3-6f2d2c360092)
  - [Shopping Cart & Wishlist – run](https://app.rova.qa/suites/runs/31e5374f-a403-4b20-9dfc-dd5f20cc30fe)
  - [Checkout & Order Management – run (stopped)](https://app.rova.qa/suites/runs/a5bc6090-deb7-43e9-ab37-25d17af3d035)
- Manual verification screenshots for Suites 3, 4 and 5 are stored in the [evidence folder](evidence/evidence-index.md).

RovaAI links are external and may require an authenticated RovaAI session.

## Repository guide

| Document | Contents |
|---|---|
| [Project overview](01-project-overview/project-overview.md) | Context, objectives, environment, scope and success criteria |
| [Test plan](02-test-planning/test-plan.md) | Strategy, coverage model, suite configuration, safety rules, risks and result classification |
| [Test cases](03-test-design/test-cases.md) | All 62 test goals with expected behaviour and coverage notes |
| [Execution report](04-test-execution/execution-report.md) | RovaAI results, manual verification and QA interpretation for each suite |
| [Defect and investigation log](05-defect-management/observations-and-investigation.md) | Observations and investigations, separated from confirmed defects |
| [RovaAI evaluation](06-tool-evaluation/limitations-and-observations.md) | Tool strengths, limitations and safety observations |
| [Evidence index](evidence/evidence-index.md) | Run reports, result links, replays and screenshots |

## Conclusion and learning outcomes

The project shows that an AI testing agent can execute and document browser-based test goals quickly, but its results need disciplined human review. Several tool-reported outcomes changed meaning after investigation: a pass that did not test the stated behaviour, failures caused by security controls or login requirements, and a duplicated report record. Coverage of cart, wishlist and checkout was limited by the authentication boundary, and that limitation is stated rather than hidden.

Key learning outcomes:

- Writing test goals with precise, verifiable expected results – and splitting ambiguous scenarios.
- Treating automated statuses as evidence to be reviewed, not as conclusions.
- Classifying outcomes accurately: confirmed defect, requirement clarification, test-design mismatch, authentication restriction, environment control or tool limitation.
- Setting and enforcing safety boundaries for autonomous testing agents, including stopping a run when they are breached.
- Reporting coverage gaps and uncertainty honestly.

---
*QA portfolio project completed with the Testers Connect cohort. Results are specific to the recorded test sessions and environment and are not a guarantee of overall application quality.*
