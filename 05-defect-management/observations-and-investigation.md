# Defect and Investigation Log

## Purpose

This log separates confirmed application defects from test observations and checks that could not be completed. An automated test failure is not automatically a product defect.

## Current status

**No confirmed application defects have been established from the three suite runs documented in this repository.**

| Reference | Observation | Classification | Evidence / next action |
|---|---|---|---|
| OBS-01 / NEC-03 | Search payload triggered an Alibaba Cloud WAF HTTP 405 interstitial | Inconclusive – security layer/environment | [RovaAI result](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1). Reassess only in an authorized test environment where the application response can be observed. |
| OBS-02 / NEC-04 | Slider CAPTCHA prevented automated login form submission | Inconclusive – automation limitation | [RovaAI result](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4). Perform an approved manual check or use a permitted test configuration. |
| OBS-03 / CSF-08 | Shared Core report contains both a passed (749.3s) and failed (894.0s, 44 steps) execution for the category-dropdown scenario. The failed replay did not find the expected dropdown trigger in the tested UI; category tiles were visible lower on the homepage and `/catalog/` returned to the homepage. | Test-design / requirement-to-interface mismatch; aggregate evidence conflict | [Passed result](https://app.rova.qa/results/f6894067-22ac-42fa-a2f2-db8e69f1aa5a), [shared suite report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite), [failed replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm). Clarify expected category-navigation behaviour and reconcile the duplicate run record before rerunning. |
| PDS-02 | Product title stated 20000mAh while the product description stated 12000mAh. | Seller listing content inconsistency – not a confirmed Daraz platform defect | [RovaAI result](https://app.rova.qa/results/26bac08d-5513-41bc-a3e9-086732bd7b14). RovaAI did not flag the mismatch. No defect raised. |
| PDS-08 | Size US 8 (out of stock) could be selected. Selecting it displayed "Out of stock", locked quantity at 0 and removed Buy Now and Add to Cart. | Expected-result mismatch – not a confirmed defect; possible usability observation | [RovaAI result](https://app.rova.qa/results/0f3a5cf9-7ddd-460e-a726-1f76ce49bb84), [product page](https://www.daraz.lk/products/kadam-i593311645-s2722822221.html). Manually verified on 22 November 2026. Expected result revision recommended in the [test design](../03-test-design/test-cases.md). |
| PDS-10 | Back, Forward and a fresh page reload worked using browser commands. The listing returned at the same scroll position; Flash Sale products had changed. | Verified – no defect; changed Flash Sale products not a confirmed defect | [RovaAI result](https://app.rova.qa/results/eb77910c-761d-4e2c-9338-8b1279ff6d25). Toolbar buttons were not physically clicked. |

## CSF-08 investigation detail

The failed execution lasted 894.0 seconds and contained 44 steps. It attempted multiple interaction paths and viewport sizes. The desktop header exposed the logo, search box and cart, but no dropdown trigger, hamburger control or “All Categories” selector in the interactive element map. A category tile grid was present further down the homepage. Navigation to `/catalog/` resolved back to the homepage.

The evidence supports a mismatch between the test's assumed control and the interface observed in that execution. It does **not** establish that a working dropdown is defective or that category navigation is unavailable. The shared report also contains a separate passed execution for the same test title, so the final unique-goal outcome remains unresolved.

**Recommended disposition:** retain both executions as evidence; do not create a defect ticket yet. Confirm the product requirement and intended UI component, then update the test case to match the approved behaviour. Only rerun after that clarification and only if a new execution is explicitly approved.

## Suite 3 follow-up detail (Product Details & Product Selection)

RovaAI reported all 10 goals as passed. The findings below come from reviewing the result evidence and from manual follow-up checks on 22 November 2026. No Buy Now, Add to Cart, login, checkout or purchase action was performed during the manual checks.

### PDS-02 – Title and description capacity mismatch

The tested Aspor A396 power bank listing stated 20000mAh in the product title, while the product description stated a rated capacity of 12000mAh. RovaAI judged the title and description as visible, readable and relevant, and did not flag the inconsistency. This is seller-provided listing content and is **not classified as a confirmed Daraz platform defect**.

### PDS-08 – Unavailable variation behaviour

Product: [Kadam water proof fully ruber office - school shoe](https://www.daraz.lk/products/kadam-i593311645-s2722822221.html), colour Black, sizes US 7 and US 8.

- Size US 8 was selectable.
- Selecting it displayed "Out of stock".
- Quantity was locked at zero.
- Buy Now and Add to Cart were unavailable; only Add to Wishlist remained.
- Re-selecting size US 7 restored quantity 1 and the purchase buttons (observed in the RovaAI execution).

The behaviour is "selectable, but purchase prevented". The configured expected result states that unavailable variations "cannot be selected", so this is an **expected-result mismatch, not a confirmed defect**.

**Possible usability observation:** stock status was not visible before the size was selected. Size US 8 was displayed in the same style as the in-stock size until it was clicked. This is recorded for consideration only.

**Not independently verified:** during RovaAI's first attempt, the agent's live reasoning referred to a struck-through kids' size 2T that appeared to become selected. That attempt has no separate result record and the product could not be identified, so the observation could not be independently verified.

### PDS-10 – Navigation and refresh

- Back, Forward and a fresh page reload were successfully verified using browser commands.
- The homepage listing returned at the same scroll position after Back.
- The Flash Sale products shown had changed after returning. Flash Sale content is dynamic, so this is **not a confirmed defect**.
- The browser toolbar Back and Reload buttons were not physically clicked.

## Defect reporting decision

A defect should be raised only when there is sufficient evidence of repeatable application behaviour that violates an agreed expected result. For each future confirmed defect, capture:

- Unique defect ID and concise title.
- Environment, browser and reproducible preconditions.
- Steps to reproduce.
- Expected and actual results.
- Supporting screenshot, recording, logs or network evidence.
- Severity, priority and affected workflow.
- Re-test result and closure status.

The WAF, CAPTCHA and category-dropdown observations remain follow-up items, and the Suite 3 findings (PDS-02, PDS-08, PDS-10) are documented observations. None is a confirmed product defect.
