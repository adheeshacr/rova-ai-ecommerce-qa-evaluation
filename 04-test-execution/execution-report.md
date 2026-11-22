# Test Execution Report

## 1. Executive summary

Four RovaAI suites were executed against Daraz.lk, covering **42 distinct test goals**. The Negative & Edge Case run contains 12 executions, and the Product Details & Product Selection and Search, Filters & Sorting runs contain 10 each. The Core suite's shared report contains 11 execution records because the category-dropdown scenario appears twice (once passed and once failed).

| Evidence source | Reported executions | Passed | Failed | Pending | Completion |
|---|---:|---:|---:|---:|---:|
| Core Shopping Flow – shared suite report | 11 | 10 | 1 | 0 | 100% |
| Core Shopping Flow – separate run-statistics panel supplied earlier | 10 | 10 | 0 | 0 | 100% |
| Negative & Edge Case Scenarios | 12 | 10 | 2 | 0 | 100% |
| Product Details & Product Selection | 10 | 10 | 0 | 0 | 100% |
| Search, Filters & Sorting | 10 | 10 | 0 | 0 | 100% |

**Data reconciliation note:** The Core run's separate statistics panel showed 10/10 passed, while its subsequently reviewed shared report showed 11 execution records, 10 passed and 1 failed. The shared report lists the Category dropdown scenario twice: a 749.3-second passed execution and an 894.0-second failed execution. The detailed failed execution was reviewed and is documented below. These records cannot safely be collapsed into a single definitive Core pass rate without resolving the discrepancy in RovaAI. For transparency, this report preserves both source summaries rather than silently choosing one.

Across the four suites there are **42 distinct test goals** and **43 visible execution records** when the duplicate Core dropdown execution is counted. Adding the visible RovaAI execution outcomes gives 40 passed and 3 failed records; this is an execution-record count, not a unique-test-goal pass rate. A RovaAI pass status does not by itself establish complete coverage of a goal. Manual verification findings are tracked separately from RovaAI statuses: see the Suite 3 follow-up in section 4 and the Suite 4 follow-up in section 5, where SFS-09 failed manual verification despite a RovaAI pass.

## 2. Core Shopping Flow Validation

- Suite: [Core Shopping Flow run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785)
- Shared report: [Open shared suite report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite)
- Execution date: 21 November 2026.
- Separate run-statistics panel supplied earlier: 10 passed, 0 failed, 0 pending (100%).
- Shared report reviewed: 11 execution records, 10 passed, 1 failed (90.91%).

### Test goals

| ID | Test goal | Expected behaviour |
|---|---|---|
| CSF-01 | Homepage loads correctly | Homepage renders primary content and navigation without a blocking error. |
| CSF-02 | Search keyword and filters | Keyword search returns results and available filters can be applied. |
| CSF-03 | Sort options | Selecting a sort option reorders the displayed results. |
| CSF-04 | Product selection from search opens correct detail page | Selecting a result opens its corresponding product detail page. |
| CSF-05 | Product detail page shows essential information | Product detail view presents key purchase information and product/seller details. |
| CSF-06 | Cart while logged out triggers login modal | Attempting the cart action while logged out requests authentication. |
| CSF-07 | Login modal has authentication options | Login prompt displays the available authentication methods. |
| CSF-08 | Category dropdown | Category navigation can be opened and exposes category choices. |
| CSF-09 | PDP quantity selector | Product detail quantity control allows a valid quantity selection. |
| CSF-10 | Responsive UI across viewports | Key page content remains usable at the tested viewport sizes. |

### CSF-08 – Category dropdown: conflicting executions

The shared report contains two records for the same test goal:

- **Passed record:** 749.3 seconds. [View passed result](https://app.rova.qa/results/f6894067-22ac-42fa-a2f2-db8e69f1aa5a)
- **Failed record:** 894.0 seconds, 44 steps. Its detailed replay was reviewed from the exported result evidence: [Open failed execution replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm)

The failed execution tried multiple interaction paths and viewport sizes. The desktop header exposed the logo, search box and cart, but no category dropdown trigger, hamburger control or “All Categories” selector in the interactive element map. A category tile grid was visible further down the homepage. Navigating to `/catalog/` resolved back to the homepage. The agent therefore could not verify the requested dropdown behaviour and marked the execution failed.

**Assessment:** This is best classified as a test-design / requirement-to-interface mismatch or an environment/build difference, not a confirmed application defect. The evidence does not prove that a broken dropdown exists; it indicates that the specific control described by the test was not discoverable in the tested interface. The separate passed record conflicts with this observation and remains part of the evidence set. The requirement should be clarified (for example, whether the homepage category tiles satisfy the intended category-navigation requirement) before treating the scenario as a stable regression test.

## 3. Negative & Edge Case Scenarios

- Suite: [Open complete RovaAI run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)
- Execution date: 20 November 2026 (RovaAI report display: 11:40 PM).
- Duration: 27 minutes 54 seconds.
- Completion: 100%.
- Result: 10 passed, 2 failed, 0 pending.
- Tool-reported pass rate: 83.3%.

| ID | Test goal | RovaAI result | Observed result / analysis |
|---|---|---|---|
| NEC-01 | Random search string returns no-results message | Passed | Clear no-results message displayed; no blank or error page observed. |
| NEC-02 | Empty search does not crash page | Passed | Page remained stable. |
| NEC-03 | Special characters / SQL-injection-style search | Failed | Alibaba Cloud WAF returned an HTTP 405 malicious-traffic interstitial. Intended application search handling could not be verified. This is not evidence of a SQL injection vulnerability. |
| NEC-04 | Malformed email/phone login validation | Failed | Slider CAPTCHA blocked form submission; headless automation could not complete the slider interaction. Inline validation was therefore not verified. |
| NEC-05 | Incorrect credentials show appropriate error | Passed | “Invalid credentials” feedback appeared. |
| NEC-06 | Empty login form is blocked | Passed | Validation prompt appeared. |
| NEC-07 | Quantity rejects zero | Passed | Quantity remained at the minimum value of 1. |
| NEC-08 | Quantity rejects non-numeric input | Passed | Control reverted to a valid minimum quantity. |
| NEC-09 | Quantity does not exceed available stock | Passed | Stock-limit warning appeared and invalid order quantity was prevented. |
| NEC-10 | Logged-out Add to Cart / Buy Now | Passed | Login prompt/redirect appeared. No checkout or payment was completed. |
| NEC-11 | Non-existent product URL | Passed | Appropriate page-not-found experience appeared. |
| NEC-12 | Rapid repeated login submissions | Passed | Repeated clicks were ignored without duplicate-request errors in the observed run. |

### Individual result references

- [NEC-01](https://app.rova.qa/results/7debea8d-e92c-4794-9617-3b876c87ab9d)
- [NEC-02](https://app.rova.qa/results/213030e9-7606-4927-a9e1-86dd4a4d0ac7)
- [NEC-03](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1)
- [NEC-04](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4)
- [NEC-05](https://app.rova.qa/results/7f4324be-a916-413c-a23e-b2e5c81f4d50)
- [NEC-06](https://app.rova.qa/results/ad17b51b-c015-4bad-9e4e-be8224092181)
- [NEC-07](https://app.rova.qa/results/d4c038cd-850b-4858-b977-a88199a01776)
- [NEC-08](https://app.rova.qa/results/33eceaba-f906-4bf1-a87e-cec0a0ecd58b)
- [NEC-09](https://app.rova.qa/results/f7ad6e75-6761-472f-aa2b-8001f699b0ae)
- [NEC-10](https://app.rova.qa/results/081a3c5d-16e8-4b44-bf81-4cba2c042c72)
- [NEC-11](https://app.rova.qa/results/8004e787-b318-4371-acd5-33313ce8da89)
- [NEC-12](https://app.rova.qa/results/92bb44fc-a57b-43ff-900d-91a88f956b3f)

## 4. Product Details & Product Selection

### 4.1 RovaAI automated execution

- Suite: Daraz.lk – Product Details & Product Selection
- Run report: [Open RovaAI run](https://app.rova.qa/suites/runs/48f0f4d5-be13-46e5-8057-1512967b0ba9)
- Project / environment: Ecommerce WebApp / Staging Env. Application under test: https://www.daraz.lk/
- Execution date: 22 November 2026.
- Runtime configuration: sequential, Chromium, 1 retry, Stop on Failure disabled.
- Goals: 10.
- Result: 10 passed, 0 failed, 0 pending.
- Execution completion: 100%.
- Total execution time: 33 minutes 12 seconds.

| ID | Test goal | RovaAI result | Duration | Result report | RovaAI summary |
|---|---|---|---:|---|---|
| PDS-01 | Verify product detail page opens successfully | Passed | 16.6s | [View result](https://app.rova.qa/results/d6a64272-5db4-4877-836c-a11fcddfc011) | Flash Sale product opened its matching product detail page with no visible error. |
| PDS-02 | Verify product title and description are displayed correctly | Passed | 39.3s | [View result](https://app.rova.qa/results/26bac08d-5513-41bc-a3e9-086732bd7b14) | Title and description visible and readable. See observation on capacity wording in 4.3. |
| PDS-03 | Verify product image gallery functionality | Passed | 46.1s | [View result](https://app.rova.qa/results/c4491d49-9bee-4fd4-bdfb-ffb3a1bda296) | Selecting thumbnails changed the main gallery image. |
| PDS-04 | Verify product price and discount information | Passed | 30.9s | [View result](https://app.rova.qa/results/20c8228d-b29c-401b-90e9-7ad0839a2119) | Current price, struck-through original price and discount percentage displayed consistently. |
| PDS-05 | Verify product ratings and customer reviews section | Passed | 164.1s | [View result](https://app.rova.qa/results/95a11997-64c1-4c62-be24-5ee433b8eb03) | Average rating, rating count, star distribution and reviews rendered without broken content. |
| PDS-06 | Verify seller information section | Passed | 39.4s | [View result](https://app.rova.qa/results/f92d7223-75ff-41b5-b618-dc31bc869077) | Seller name and seller metrics displayed on the seller store page. |
| PDS-07 | Verify product variation options | Passed | 46.0s | [View result](https://app.rova.qa/results/10e1af60-fc2f-4d32-8c6a-f9a2d3c24367) | Colour and size options displayed; an available size could be selected. |
| PDS-08 | Verify unavailable product variations cannot be selected | Passed after one retry | 290.8s (final attempt) | [View result](https://app.rova.qa/results/0f3a5cf9-7ddd-460e-a726-1f76ce49bb84) | Out-of-stock size showed an "Out of stock" label, quantity 0 and no purchase buttons. Pass required interpretation of the expected result; see 4.2. |
| PDS-09 | Verify product availability and stock information | Passed | 73.3s | [View result](https://app.rova.qa/results/66c1f7ee-d705-4119-8ff1-e9a74066e4a2) | Availability message shown for the selected variation. |
| PDS-10 | Verify product detail page navigation and browser refresh behaviour | Passed | 37.4s | [View result](https://app.rova.qa/results/eb77910c-761d-4e2c-9338-8b1279ff6d25) | Product page re-rendered correctly after the same URL was loaded again. Back/Forward not exercised; see 4.2. |

Individual durations are taken from the RovaAI run timeline. The PDS-08 duration reflects the final (retry) attempt only; the first attempt is not shown as a separate result record, which accounts for most of the difference between the summed durations and the total execution time.

### 4.2 Manual follow-up verification

Two goals were re-checked manually on Daraz.lk on 22 November 2026 because their automated pass status did not fully answer the test question. No Buy Now, Add to Cart, login, checkout or purchase action was performed during the manual checks.

**PDS-08 – Unavailable product variations**

- Product used by RovaAI (identified from the result's network evidence): [Kadam water proof fully ruber office - school shoe](https://www.daraz.lk/products/kadam-i593311645-s2722822221.html), colour Black.
- Variation tested: size US 8.
- Before selection, size 8 was presented in the same style as the in-stock size 7 (not disabled, greyed or struck through).
- Size 8 could be selected; the page URL changed to the size 8 SKU.
- After selection the page showed "Out of stock", the quantity was locked at 0, and Buy Now and Add to Cart were not available (only Add to Wishlist was shown).
- **Actual behaviour:** the unavailable variation can be selected, but purchasing is prevented.
- **Classification:** expected-result mismatch, not a confirmed defect. The configured expected result ("cannot be selected") does not match the observed design. A revised expected result is recorded in the [test design](../03-test-design/test-cases.md).

**PDS-10 – Product page navigation and refresh**

- Listing: Daraz.lk homepage Flash Sale section. Product: [Aspor A396 20000mAh Power Bank](https://www.daraz.lk/products/aspor-a396-20000mah-power-bank-with-pd-charging-capacity-20000-mah-225w-lcd-digital-display-iq-output-i1771175744-s12960787380.html) (the product used by RovaAI).

| Step | Method | Result |
|---|---|---|
| Listing to product page | Clicked the product card in Flash Sale | Product page opened in the same tab with correct title, price and breadcrumb. |
| Back | Browser history-back command | Homepage returned at the same scroll position with the Flash Sale section displayed. The Flash Sale products shown had changed. |
| Forward | Browser history-forward command | Same product page and URL restored with title, price and purchase buttons present. |
| Reload | Programmatic page reload (browser navigation type recorded as "reload") | Product page loaded again fully: title, price, gallery images, breadcrumb and purchase buttons present. |

- **Result:** navigation and reload behaviour verified.
- **Not tested:** the browser toolbar Back and Reload buttons were not physically clicked; equivalent browser commands were used. Keyboard shortcuts blocked by the automation environment were not used.

### 4.3 Coverage limitations and observations

- **Automated pass status is not complete coverage.** RovaAI reported 10/10 passed, but PDS-08 required human interpretation of the expected behaviour and PDS-10's automated run used a repeated URL load instead of a refresh and did not exercise Back/Forward navigation.
- **PDS-08 retry:** the goal passed on its second attempt. During the first attempt, the live agent reasoning referred to a struck-through kids' size (2T) that appeared to become selected. That attempt is not available as a separate result record and the product could not be identified, so this could not be independently verified.
- **PDS-02 content observation:** the product title stated 20000mAh while the description stated 12000mAh. This is a seller listing content inconsistency and was not flagged by RovaAI. It is not classified as a Daraz platform defect.
- **PDS-08 usability observation:** stock status was not visible before the out-of-stock size was selected. This is recorded as a possible usability point, not a defect.
- **Live data:** products were chosen by the agent from live listings, so the specific products tested may differ on a rerun.
- Detailed observations are recorded in the [observations and investigation log](../05-defect-management/observations-and-investigation.md).

## 5. Search, Filters & Sorting

### 5.1 RovaAI automated execution

- Suite: Daraz.lk – Search, Filters & Sorting
- Run report: [Open RovaAI run](https://app.rova.qa/suites/runs/8d8e3e97-4286-4e44-80d3-6f2d2c360092)
- Project / environment: Ecommerce WebApp / Staging Env. Application under test: https://www.daraz.lk/
- Execution date: 22 November 2026.
- Runtime configuration: sequential, Chromium, 0 retries, Stop on Failure off.
- Goals: 10.
- RovaAI result: 10 passed, 0 failed, 0 pending.
- Execution completion: 100%.
- Total execution time: 9 minutes 11 seconds.

| ID | Test goal | RovaAI result | Duration | Steps | Result report | RovaAI summary |
|---|---|---|---:|---:|---|---|
| SFS-01 | Search by valid product keyword | Passed | 24.6s | 4 | [View result](https://app.rova.qa/results/09f4eb5d-51a1-4f91-828e-0439d45c6db1) | "headphones" returned 54,157 results with relevant product titles and refinements. |
| SFS-02 | Show search suggestions while typing | Passed | 32.2s | 6 | [View result](https://app.rova.qa/results/f0a2c75d-c7c3-40e7-9650-991f223a48a0) | Typing "phone" displayed suggestions; selecting "phone holder" opened its results page. |
| SFS-03 | Handle searches with no matching products | Passed | 18.0s | 3 | [View result](https://app.rova.qa/results/230ebebb-8b0b-4622-9d41-847175855c12) | A random string returned 0 items with a clear "Search No Result" message and no errors. |
| SFS-04 | Search using multiple keywords | Passed | 18.8s | 2 | [View result](https://app.rova.qa/results/12293fc9-40ab-4f5b-8b3c-07a72b4d27f1) | "wireless bluetooth headphones" returned 41,563 results relevant to all terms. |
| SFS-05 | Filter search results by category | Passed | 20.9s | 3 | [View result](https://app.rova.qa/results/1186d2f2-b6e3-4a2e-bd12-ec6343791b48) | "phone" search filtered to Micro SD Cards; RovaAI verified only the page heading. Confirmed manually (4.2). |
| SFS-06 | Filter products by minimum and maximum price | Passed | 193.4s | 12 | [View result](https://app.rova.qa/results/d2a1a1cf-4147-4995-b8e3-8c94ae3aa3a1) | Rs. 1,000–3,000 filter on "headphones"; visible prices checked across several scrolls. |
| SFS-07 | Sort products by price low to high | Passed | 27.6s | 5 | [View result](https://app.rova.qa/results/be0dec49-60de-4aca-b792-57735ee7e110) | RovaAI checked only four prices (Rs. 29, 64, 92, 100). Confirmed manually (4.2). |
| SFS-08 | Sort products by price high to low | Passed | 50.5s | 10 | [View result](https://app.rova.qa/results/45d969af-94ae-4ba4-87df-f38422f94734) | "laptop" results in descending order with sort=pricedesc. See price outlier observation (4.3). |
| SFS-09 | Apply multiple filters together | Passed | 111.5s | 16 | [View result](https://app.rova.qa/results/8e6e5ba0-c4a2-49de-95a3-90d79abc8477) | Final check used Brand: Disney plus Shipped From: Overseas. Two brands together were not established. Manual failure (4.2). |
| SFS-10 | Clear applied search filters | Passed | 51.5s | 9 | [View result](https://app.rova.qa/results/ee10dbc6-653f-4c0f-8f26-8006dc883aba) | Count changed 48,521 → 427 (Brand: Sanrio) → 48,521 after Clear All. One interaction step failed and the test recovered. |

Individual durations sum to approximately the total execution time, consistent with no retries.

### 5.2 Manual follow-up verification

Manual checks were performed on Daraz.lk on 22 November 2026, read-only and logged out. No Buy Now, Add to Cart, login, checkout or payment action was performed. These results are recorded separately from the RovaAI status above.

| Goal | Manual check | Manual result |
|---|---|---|
| SFS-05 | Opened the filtered page [phone + Micro SD Cards](https://www.daraz.lk/phone-micro-sd-cards/?q=phone). The search keyword remained applied and the listed products were micro SD cards. | Confirmed |
| SFS-07 | Opened [phone sorted by price low to high](https://www.daraz.lk/catalog/?q=phone&sort=priceasc). All 40 products on page 1 were in ascending price order (Rs. 29 to Rs. 236). | Confirmed |
| SFS-08 | Opened [laptop sorted by price high to low](https://www.daraz.lk/catalog/?q=laptop&sort=pricedesc). All 40 products on page 1 were in descending price order. | Sorting confirmed; seller price outlier noted (5.3) |
| SFS-09 | Search keyword "phone". Applied two brands (UGREEN + Andoer; Sanrio + Disney), then a third brand (ECHIDNA), then removed the third brand. Compared with Brand: Disney + Shipped From: Overseas. | **Failed against the current expected result** |

**SFS-09 summary.** Selecting a second brand replaced the previously selected brand, and only the latest brand was applied. The URL could contain multiple brand slugs (for example `/sanrio--disney/?q=phone`), but the displayed products matched only the last brand. Removing the latest brand cleared all brand filters instead of restoring the previous selection. The "phone" keyword remained applied throughout. Combining Disney with Shipped From: Overseas worked correctly, and removing Overseas retained Disney. Full detail is in the [observations and investigation log](../05-defect-management/observations-and-investigation.md).

**Classification:** manual failure against the current expected result; requirement clarification needed on whether brand filters are intended to support multiple selections. This is not a confirmed defect, and no defect ID has been created.

### 5.3 Coverage limitations and observations

- **SFS-09 – insufficient automated pass.** RovaAI marked SFS-09 as passed, but its final verification combined a brand with a shipping-location filter. It did not establish that two brand filters remained selected together. During the automated run, RovaAI recorded "Brand: Sanrio" and "Brand: Disney" with 9 items; manual verification showed that those 9 items matched Disney only.
- **SFS-05 and SFS-07 – thin automated evidence.** RovaAI passed these goals on limited evidence (a page heading; four prices). Both were confirmed by the manual checks in 5.2.
- **SFS-08 – seller listing data observation.** The top "laptop" result sorted high to low was a UGREEN 67W laptop power adapter listed at Rs. 1,655,266,553. The sort order itself was correct; this is a seller listing data observation, not a sorting defect.
- **SFS-10 – automation recovery.** One interaction step failed because of an element-selection issue; the agent recovered on the next step and completed the check.
- **Configuration:** the suite ran with 0 retries. All ten goals showed Draft status before execution and were executable.
- **No confirmed application defects** were established from Suite 4.

## 6. Failure analysis and follow-up

### NEC-03 – WAF interstitial
**Classification:** Inconclusive application check / environment or security-layer interference.

The WAF intercepted the test input before the intended application response could be evaluated. A separate controlled security test, with authorization and an appropriate test environment, would be needed to assess backend injection resistance.

### NEC-04 – CAPTCHA challenge
**Classification:** Inconclusive application check / automation limitation.

The CAPTCHA prevented the automated browser from submitting the malformed identifier. The result does not establish that application-side input validation is absent or defective. A permitted manual validation check or test environment with CAPTCHA handling configured would be needed.

### CSF-08 – Category dropdown
**Classification:** Test-design / interface mismatch requiring requirement clarification.

The failed replay did not identify the dropdown control expected by the test. Clarify the intended navigation component and align the test steps with the current UI before rerunning. Do not log this as a confirmed defect based on the available evidence.

## 7. Overall conclusion

The four suites cover 42 distinct test goals and reached 100% execution completion. The Negative & Edge Case suite has a clear result of 10 passed and 2 blocked/failed checks. The Core suite has conflicting aggregate evidence: a separate statistics panel reports 10/10 passed, while the shared report shows 11 execution records with 10 passed and 1 failed due to a duplicate category-dropdown scenario.

This discrepancy is explicitly retained for auditability. The Product Details & Product Selection suite was reported by RovaAI as 10/10 passed; manual follow-up confirmed the PDS-10 navigation and reload behaviour and reclassified PDS-08 as an expected-result mismatch rather than a clean pass against the configured wording. The Search, Filters & Sorting suite was also reported by RovaAI as 10/10 passed; manual checks confirmed SFS-05, SFS-07 and SFS-08 sorting, but SFS-09 failed manual verification because two brand filters could not be kept applied together, pending requirement clarification. The observed failures and follow-up findings are not, on current evidence, confirmed application defects. The project demonstrates test planning, scenario design, review of AI-assisted execution, evidence interpretation and transparent reporting. No checkout or payment was completed.
