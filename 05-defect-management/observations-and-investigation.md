# Defect and Investigation Log

## Purpose

This log separates confirmed application defects from test observations and checks that could not be completed. An automated test failure is not automatically a product defect.

## Current status

**No confirmed application defects have been established from the two suite runs documented in this repository.**

| Reference | Observation | Classification | Evidence / next action |
|---|---|---|---|
| OBS-01 / NEC-03 | Search payload triggered an Alibaba Cloud WAF HTTP 405 interstitial | Inconclusive – security layer/environment | [RovaAI result](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1). Reassess only in an authorized test environment where the application response can be observed. |
| OBS-02 / NEC-04 | Slider CAPTCHA prevented automated login form submission | Inconclusive – automation limitation | [RovaAI result](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4). Perform an approved manual check or use a permitted test configuration. |
| OBS-03 / CSF-08 | Shared Core report contains both a passed (749.3s) and failed (894.0s, 44 steps) execution for the category-dropdown scenario. The failed replay did not find the expected dropdown trigger in the tested UI; category tiles were visible lower on the homepage and `/catalog/` returned to the homepage. | Test-design / requirement-to-interface mismatch; aggregate evidence conflict | [Passed result](https://app.rova.qa/results/f6894067-22ac-42fa-a2f2-db8e69f1aa5a), [shared suite report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite), [failed replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm). Clarify expected category-navigation behaviour and reconcile the duplicate run record before rerunning. |

## CSF-08 investigation detail

The failed execution lasted 894.0 seconds and contained 44 steps. It attempted multiple interaction paths and viewport sizes. The desktop header exposed the logo, search box and cart, but no dropdown trigger, hamburger control or “All Categories” selector in the interactive element map. A category tile grid was present further down the homepage. Navigation to `/catalog/` resolved back to the homepage.

The evidence supports a mismatch between the test's assumed control and the interface observed in that execution. It does **not** establish that a working dropdown is defective or that category navigation is unavailable. The shared report also contains a separate passed execution for the same test title, so the final unique-goal outcome remains unresolved.

**Recommended disposition:** retain both executions as evidence; do not create a defect ticket yet. Confirm the product requirement and intended UI component, then update the test case to match the approved behaviour. Only rerun after that clarification and only if a new execution is explicitly approved.

## Defect reporting decision

A defect should be raised only when there is sufficient evidence of repeatable application behaviour that violates an agreed expected result. For each future confirmed defect, capture:

- Unique defect ID and concise title.
- Environment, browser and reproducible preconditions.
- Steps to reproduce.
- Expected and actual results.
- Supporting screenshot, recording, logs or network evidence.
- Severity, priority and affected workflow.
- Re-test result and closure status.

The WAF, CAPTCHA and category-dropdown observations remain follow-up items, not confirmed product defects.
