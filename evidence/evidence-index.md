# Evidence Index

This page provides direct access to the completed RovaAI suite runs, individual results and available execution replays.

## Suite-level evidence

| Suite | Evidence | Reported outcome |
|---|---|---|
| Core Shopping Flow Validation | [Run page](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785) · [Shared report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite) | Shared report: 11 executions, 10 passed, 1 failed (90.91%). A separate run-statistics panel previously supplied showed 10 passed, 0 failed. See reconciliation note below. |
| Negative & Edge Case Scenarios | [Open RovaAI run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13) | 12 executions, 10 passed, 2 failed, 0 pending; 100% completion. |
| Product Details & Product Selection | [Open RovaAI run](https://app.rova.qa/suites/runs/48f0f4d5-be13-46e5-8057-1512967b0ba9) | 10 executions, 10 passed, 0 failed, 0 pending; 100% completion; 33 minutes 12 seconds. RovaAI pass status only; see manual follow-up below. |

### Core report reconciliation

The shared Core report contains 11 execution records, although the suite contains 10 distinct test goals. The category-dropdown test appears twice: one passed result (749.3 seconds) and one failed result (894.0 seconds, 44 steps). A separate run-statistics panel supplied earlier showed 10/10 passed. Both source summaries are retained rather than silently selecting one. The detailed failed replay did not find the dropdown trigger expected by the test in the tested UI; this is treated as a test-design / requirement mismatch pending clarification, not a confirmed application defect.

- [Passed category-dropdown result](https://app.rova.qa/results/f6894067-22ac-42fa-a2f2-db8e69f1aa5a)
- [Failed category-dropdown execution replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm)

## Negative & Edge Case – individual results

| Test ID | RovaAI result |
|---|---|
| NEC-01 | [View result](https://app.rova.qa/results/7debea8d-e92c-4794-9617-3b876c87ab9d) |
| NEC-02 | [View result](https://app.rova.qa/results/213030e9-7606-4927-a9e1-86dd4a4d0ac7) |
| NEC-03 | [View result – WAF blocked test](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1) |
| NEC-04 | [View result – CAPTCHA blocked test](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4) |
| NEC-05 | [View result](https://app.rova.qa/results/7f4324be-a916-413c-a23e-b2e5c81f4d50) |
| NEC-06 | [View result](https://app.rova.qa/results/ad17b51b-c015-4bad-9e4e-be8224092181) |
| NEC-07 | [View result](https://app.rova.qa/results/d4c038cd-850b-4858-b977-a88199a01776) |
| NEC-08 | [View result](https://app.rova.qa/results/33eceaba-f906-4bf1-a87e-cec0a0ecd58b) |
| NEC-09 | [View result](https://app.rova.qa/results/f7ad6e75-6761-472f-aa2b-8001f699b0ae) |
| NEC-10 | [View result](https://app.rova.qa/results/081a3c5d-16e8-4b44-bf81-4cba2c042c72) |
| NEC-11 | [View result](https://app.rova.qa/results/8004e787-b318-4371-acd5-33313ce8da89) |
| NEC-12 | [View result](https://app.rova.qa/results/92bb44fc-a57b-43ff-900d-91a88f956b3f) |

## Product Details & Product Selection – individual results

| Test ID | RovaAI result |
|---|---|
| PDS-01 | [View result](https://app.rova.qa/results/d6a64272-5db4-4877-836c-a11fcddfc011) |
| PDS-02 | [View result – listing capacity mismatch observed](https://app.rova.qa/results/26bac08d-5513-41bc-a3e9-086732bd7b14) |
| PDS-03 | [View result](https://app.rova.qa/results/c4491d49-9bee-4fd4-bdfb-ffb3a1bda296) |
| PDS-04 | [View result](https://app.rova.qa/results/20c8228d-b29c-401b-90e9-7ad0839a2119) |
| PDS-05 | [View result](https://app.rova.qa/results/95a11997-64c1-4c62-be24-5ee433b8eb03) |
| PDS-06 | [View result](https://app.rova.qa/results/f92d7223-75ff-41b5-b618-dc31bc869077) |
| PDS-07 | [View result](https://app.rova.qa/results/10e1af60-fc2f-4d32-8c6a-f9a2d3c24367) |
| PDS-08 | [View result – passed after one retry; manual follow-up](https://app.rova.qa/results/0f3a5cf9-7ddd-460e-a726-1f76ce49bb84) |
| PDS-09 | [View result](https://app.rova.qa/results/66c1f7ee-d705-4119-8ff1-e9a74066e4a2) |
| PDS-10 | [View result – manual follow-up](https://app.rova.qa/results/eb77910c-761d-4e2c-9338-8b1279ff6d25) |

Each Suite 3 result page includes the agent's step timeline and a video recording within RovaAI.

### Suite 3 manual follow-up references (22 November 2026)

| Goal | Page checked | Outcome |
|---|---|---|
| PDS-08 | [Kadam school shoe – Daraz.lk](https://www.daraz.lk/products/kadam-i593311645-s2722822221.html) (size US 8) | Selectable; "Out of stock" shown, quantity locked at 0, Buy Now and Add to Cart unavailable. |
| PDS-10 | Daraz.lk homepage Flash Sale → [Aspor A396 power bank – Daraz.lk](https://www.daraz.lk/products/aspor-a396-20000mah-power-bank-with-pd-charging-capacity-20000-mah-225w-lcd-digital-display-iq-output-i1771175744-s12960787380.html) | Back, Forward and page reload verified using browser commands. |

Manual verification screenshots:

- [PDS-08 – size US 7 default, in stock](G08-1-size7-default-in-stock.jpg)
- [PDS-08 – size US 8 selected, out of stock](G08-2-size8-selected-out-of-stock.jpg)
- [PDS-10 – homepage Flash Sale before opening product](G10-1-homepage-flash-sale-before.jpg)
- [PDS-10 – listing after Back](G10-2-after-back-listing-restored.jpg)
- [PDS-10 – product page after Forward and reload](G10-3-product-after-forward-and-reload.jpg

-   Daraz.lk pages are live and may change after the verification date. Findings are documented in the [execution report](../04-test-execution/execution-report.md) and the [observations log](../05-defect-management/observations-and-investigation.md).

## Video evidence

- [NEC-01 execution replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-7debea8d-e92c-4794-9617-3b876c87ab9d-1795236023043.webm)
- [CSF-08 failed category-dropdown replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm)

## Evidence handling notes

- RovaAI links are external and may require an authenticated session.
- Suite 3 manual verification screenshots are stored in the evidence folder.
- Evidence should be added only when genuine, relevant and free of credentials, personal information or payment details.
- Test result pages, shared suite reports and recordings are the primary traceability references for this iteration.
