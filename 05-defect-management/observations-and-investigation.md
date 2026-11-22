# Defect and Investigation Log

## Purpose

This log separates confirmed application defects from test observations and checks that could not be completed. An automated test failure is not automatically a product defect.

## Current status

**No confirmed application defects have been established from the six suite runs documented in this repository.**

### Classification summary

| Category | Items |
|---|---|
| Confirmed application defects | None |
| Potential issues requiring requirement clarification | SFS-09 (multiple brand filters not retained together) |
| Test-design / expected-result mismatches | CSF-08 (category dropdown not present in tested UI); PDS-08 ("cannot be selected" vs selectable but not purchasable) |
| Authentication restrictions | SCW-01 to SCW-07 and SCW-10; COM-01, COM-03 to COM-07 (cart, wishlist and checkout require sign-in) |
| WAF / CAPTCHA / environment limitations | NEC-03 (WAF HTTP 405); NEC-04 (slider CAPTCHA) |
| Listing data and minor observations | PDS-02 (capacity mismatch); SFS-08 (seller price outlier); `www.daraz.lk/wishlist/` and `www.daraz.lk/cart/` generic error pages |
| RovaAI execution and reporting limitations | Duplicate CSF-08 record; thin or misleading passes (SFS-05, SFS-07, SFS-09); incorrect URL (SCW-09); authentication-blocked goals reported as Failed (Suite 5) or Passed (Suite 6); safety-boundary breaches (Suites 5 and 6) |

| Reference | Observation | Classification | Evidence / next action |
|---|---|---|---|
| OBS-01 / NEC-03 | Search payload triggered an Alibaba Cloud WAF HTTP 405 interstitial | Inconclusive – security layer/environment | [RovaAI result](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1). Reassess only in an authorized test environment where the application response can be observed. |
| OBS-02 / NEC-04 | Slider CAPTCHA prevented automated login form submission | Inconclusive – automation limitation | [RovaAI result](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4). Perform an approved manual check or use a permitted test configuration. |
| OBS-03 / CSF-08 | Shared Core report contains both a passed (749.3s) and failed (894.0s, 44 steps) execution for the category-dropdown scenario. The failed replay did not find the expected dropdown trigger in the tested UI; category tiles were visible lower on the homepage and `/catalog/` returned to the homepage. | Test-design / requirement-to-interface mismatch; aggregate evidence conflict | [Passed result](https://app.rova.qa/results/f6894067-22ac-42fa-a2f2-db8e69f1aa5a), [shared suite report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite), [failed replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm). Clarify expected category-navigation behaviour and reconcile the duplicate run record before rerunning. |
| PDS-02 | Product title stated 20000mAh while the product description stated 12000mAh. | Seller listing content inconsistency – not a confirmed Daraz platform defect | [RovaAI result](https://app.rova.qa/results/26bac08d-5513-41bc-a3e9-086732bd7b14). RovaAI did not flag the mismatch. No defect raised. |
| PDS-08 | Size US 8 (out of stock) could be selected. Selecting it displayed "Out of stock", locked quantity at 0 and removed Buy Now and Add to Cart. | Expected-result mismatch – not a confirmed defect; possible usability observation | [RovaAI result](https://app.rova.qa/results/0f3a5cf9-7ddd-460e-a726-1f76ce49bb84), [product page](https://www.daraz.lk/products/kadam-i593311645-s2722822221.html). Manually verified on 22 November 2026. Expected result revision recommended in the [test design](../03-test-design/test-cases.md). |
| PDS-10 | Back, Forward and a fresh page reload worked using browser commands. The listing returned at the same scroll position; Flash Sale products had changed. | Verified – no defect; changed Flash Sale products not a confirmed defect | [RovaAI result](https://app.rova.qa/results/eb77910c-761d-4e2c-9338-8b1279ff6d25). Toolbar buttons were not physically clicked. |
| SFS-05 / SFS-07 | RovaAI passed category filtering and low-to-high sorting on thin evidence (a page heading; four prices). | Automated evidence limitation – confirmed manually | [SFS-05 result](https://app.rova.qa/results/1186d2f2-b6e3-4a2e-bd12-ec6343791b48), [SFS-07 result](https://app.rova.qa/results/be0dec49-60de-4aca-b792-57735ee7e110). Manual checks on 22 November 2026 confirmed both. |
| SFS-08 | Top "laptop" result sorted high to low was a UGREEN 67W laptop power adapter listed at Rs. 1,655,266,553. Sort order was correct. | Seller listing data observation – not a sorting defect | [RovaAI result](https://app.rova.qa/results/45d969af-94ae-4ba4-87df-f38422f94734). No defect raised. |
| SFS-09 | Selecting a second brand replaced the first; only the latest brand was applied. Removing it cleared all brand filters. Brand + Shipped From worked. | Manual failure against the current expected result – requirement clarification required; not a confirmed defect | [RovaAI result](https://app.rova.qa/results/8e6e5ba0-c4a2-49de-95a3-90d79abc8477), [UGREEN + Andoer](https://www.daraz.lk/ugreen--andoer/?q=phone), [Sanrio + Disney](https://www.daraz.lk/sanrio--disney/?q=phone). See investigation detail below. No defect ID created. |
| SFS-10 | One automation interaction step failed (element selection); the test recovered and completed. | Automation limitation – no impact on the result | [RovaAI result](https://app.rova.qa/results/ee10dbc6-653f-4c0f-8f26-8006dc883aba). |
| SCW-01 to SCW-07, SCW-10 | Cart and wishlist actions require a signed-in account: logged-out Add to Cart opens a login pop-up, and the cart URL redirects to login. | Authentication boundary – blocked, not a defect | [Run report](https://app.rova.qa/suites/runs/31e5374f-a403-4b20-9dfc-dd5f20cc30fe). Manually verified on 22 November 2026. Functional cart behaviour remains unverified. |
| SCW-09 | RovaAI used `www.daraz.lk/wishlist/`, which shows a generic error page. The actual wishlist URL `my.daraz.lk/wishlist/index` redirects to login. | Automation evidence error – conclusion manually confirmed; not a defect | [RovaAI result](https://app.rova.qa/results/cff7e099-75dd-41c7-8857-b2941bcfdce8). |
| COM-01, COM-03 to COM-07 | Logged-out Add to Cart and Buy Now open a login pop-up; cart access requires sign-in; no guest checkout available. | Authentication boundary – blocked, not a defect | [Run report](https://app.rova.qa/suites/runs/a5bc6090-deb7-43e9-ab37-25d17af3d035). Checkout functionality remains unverified. |
| COM (cart URL) | `www.daraz.lk/cart/` shows a generic error page; `cart.daraz.lk/cart` redirects to login. | Minor observation – not a confirmed defect | Recorded during Suite 6 execution. |
| COM-08 to COM-10 | Run stopped during COM-08 after the agent attempted to type into the sign-up phone-number field; COM-09 and COM-10 not run. | RovaAI safety-boundary breach – not an application issue | See Suite 6 detail below and the [RovaAI evaluation](../06-tool-evaluation/limitations-and-observations.md). |

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

## Suite 4 follow-up detail (Search, Filters & Sorting)

RovaAI reported all 10 goals as passed. The findings below come from reviewing the result evidence and from read-only manual checks on 22 November 2026. No Buy Now, Add to Cart, login, checkout or payment action was performed.

### SFS-09 – Multiple filters: investigation

**Search keyword:** `phone` (submitted from the Daraz.lk homepage; 48,521 items before filtering). Filters were selected through the left-hand filter panel.

**Test combinations:**

- UGREEN + Andoer
- Sanrio + Disney
- Sanrio + Disney + ECHIDNA
- Comparison: Brand: Disney + Shipped From: Overseas

**Observed behaviour:**

| Step | URL after the action | Filters shown as selected | Results | Products displayed |
|---|---|---|---:|---|
| Select UGREEN | `/ugreen/?q=phone` | UGREEN | 126 | UGREEN |
| Add Andoer | `/ugreen--andoer/?q=phone` | Andoer only | 8 | Andoer only |
| Select Sanrio (new search) | `/sanrio/?q=phone` | Sanrio | 427 | Sanrio |
| Add Disney | `/sanrio--disney/?q=phone` | Disney only | 9 | Disney only |
| Add ECHIDNA | `/disney--echidna-123423045/?q=phone` | ECHIDNA only | 30 | ECHIDNA |
| Remove ECHIDNA | `/catalog/?q=phone` | None | 48,521 | Unfiltered |
| Select Disney, add Shipped From: Overseas | `/disney/?q=phone&location=Overseas` | Disney and Overseas | 9 | Disney, all tagged Overseas |
| Remove Overseas | `/disney/?q=phone` | Disney | 9 | Disney |

Loading the multi-brand URLs directly gave the same outcome regardless of order: `/ugreen--andoer/?q=phone` returned Andoer only (8), `/andoer--ugreen/?q=phone` returned UGREEN only (126) and `/sanrio--disney/?q=phone` returned Disney only (9).

**Findings:**

- Selecting a second brand replaced the previously selected brand.
- Only the latest brand was applied.
- The URL could contain multiple brand slugs, but the displayed products matched only the last brand.
- Removing the latest brand cleared all brand filters rather than restoring the previous selection.
- The "phone" search keyword remained applied throughout.
- Combining Disney with Shipped From: Overseas worked correctly.
- Removing Overseas retained Disney.

**Reproduction links** (logged out; results are live and may change):

- https://www.daraz.lk/ugreen--andoer/?q=phone
- https://www.daraz.lk/sanrio--disney/?q=phone

**Relationship to the RovaAI result:** RovaAI marked SFS-09 as passed. Its final verification used Brand: Disney with Shipped From: Overseas, which works. During the run it recorded "Brand: Sanrio" and "Brand: Disney" with 9 items; the manual check shows those 9 items were Disney only. The automated pass therefore did not establish that two brand filters remained selected together.

**Classification:**

- Manual failure against the current expected result ("Search results satisfy all selected filters").
- Requirement clarification required: the checkbox controls and multi-brand URLs suggest multiple selection, but single-brand selection may be the intended design.
- Not a confirmed defect until the intended multi-brand behaviour is established.
- No defect ID has been created.

### SFS-08 – Seller price outlier

When "laptop" results were sorted by price high to low, the first product was a UGREEN 67W laptop power adapter listed at Rs. 1,655,266,553. Manual review of the first 40 results confirmed that the sort order itself was correct. The price is a seller listing data observation and is **not classified as a sorting defect**.

### SFS-05 and SFS-07 – Thin automated evidence, confirmed manually

- **SFS-05:** RovaAI verified only the "Micro SD Cards in Sri Lanka" heading. Manual review of `/phone-micro-sd-cards/?q=phone` confirmed that the "phone" keyword remained applied and that the listed products were micro SD cards.
- **SFS-07:** RovaAI checked only four prices. Manual review of the first 40 "phone" results sorted low to high confirmed ascending order (Rs. 29 to Rs. 236).

### SFS-10 – Automation interaction failure with recovery

One step that attempted to select the Sanrio brand filter failed because of an element-selection issue. The agent recovered on the following step, applied and cleared the filter twice, and confirmed that the result count returned from 427 to the 48,521 baseline. This is an automation limitation with no impact on the result.

## Suite 5 follow-up detail (Shopping Cart & Wishlist)

RovaAI reported 2 passed and 8 failed goals. All eight failures reached Daraz.lk's authentication boundary: adding to the cart, viewing the cart, adding to the wishlist and viewing the wishlist require a signed-in account. Manual checks on 22 November 2026, performed logged out, confirmed that Add to Cart and the wishlist heart open a login pop-up, and that `https://cart.daraz.lk/cart` and `https://my.daraz.lk/wishlist/index` redirect to the login page.

Requiring authentication for cart and wishlist access is recorded as an observation about the application's design, **not as a defect**. No defect ID has been created. Cart and wishlist functionality beyond the login boundary remains unverified.

For SCW-09, RovaAI's evidence came from `https://www.daraz.lk/wishlist/`, which is not the wishlist page and displays a generic error page. The conclusion that the wishlist requires authentication was confirmed independently using the actual wishlist URL.

## Suite 6 follow-up detail (Checkout & Order Management)

RovaAI completed 7 of 10 goals (5 passed, 2 failed) before the run was stopped for safety. All completed goals reached Daraz.lk's authentication boundary: checkout could not be accessed without signing in, so delivery address, delivery options, order summary, totals, payment methods and validation at checkout remain unverified. The passes for COM-01, COM-03, COM-04 and COM-07 confirm the login requirement only.

`https://www.daraz.lk/cart/` displayed a generic error page, whereas `https://cart.daraz.lk/cart` redirected to login. This is recorded as a minor observation, similar to the incorrect wishlist URL in Suite 5, and **not as a defect**.

The run was stopped during COM-08 because the RovaAI agent, despite instructions not to open login or registration pages, repeatedly opened them and then attempted to type into the sign-up phone-number field. Step timelines for COM-01 to COM-07 show no personal data entered. COM-08 has no result record, so **it cannot be fully confirmed whether any text was entered during that attempt**. No SMS verification, account creation, payment or order submission occurred. This is a testing-agent limitation, not a Daraz.lk issue. No defect ID has been created.

## Defect reporting decision

A defect should be raised only when there is sufficient evidence of repeatable application behaviour that violates an agreed expected result. For each future confirmed defect, capture:

- Unique defect ID and concise title.
- Environment, browser and reproducible preconditions.
- Steps to reproduce.
- Expected and actual results.
- Supporting screenshot, recording, logs or network evidence.
- Severity, priority and affected workflow.
- Re-test result and closure status.

The WAF, CAPTCHA and category-dropdown observations remain follow-up items, the Suite 3 findings (PDS-02, PDS-08, PDS-10) are documented observations, and the Suite 4 findings (SFS-05, SFS-07, SFS-08, SFS-09, SFS-10) are documented observations. SFS-09 is a manual failure against the current expected result that requires requirement clarification. The Suite 5 findings (authentication boundary for SCW-01 to SCW-07 and SCW-10; incorrect evidence URL for SCW-09) are documented observations, and the Suite 6 findings (authentication boundary for COM-01 and COM-03 to COM-07; cart URL observation; run stopped for safety) are documented observations. None is a confirmed product defect.
