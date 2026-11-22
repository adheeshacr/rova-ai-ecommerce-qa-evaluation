# Evidence Index

This page provides direct access to the completed RovaAI suite runs, individual results and available execution replays.

## Suite-level evidence

| Suite | Evidence | Reported outcome |
|---|---|---|
| Core Shopping Flow Validation | [Run page](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785) · [Shared report](https://app.rova.qa/reports/share/40b15ceb-bcee-4873-831a-29606391b785?type=suite) | Shared report: 11 executions, 10 passed, 1 failed (90.91%). A separate run-statistics panel previously supplied showed 10 passed, 0 failed. See reconciliation note below. |
| Negative & Edge Case Scenarios | [Open RovaAI run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13) | 12 executions, 10 passed, 2 failed, 0 pending; 100% completion. |

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

## Video evidence

- [NEC-01 execution replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-7debea8d-e92c-4794-9617-3b876c87ab9d-1795236023043.webm)
- [CSF-08 failed category-dropdown replay](https://rova-storage.s3.us-west-2.amazonaws.com/rova/web/c7bff371-c60a-4f43-8a07-7ee71e5c3a15/videos/video-4cd7767f-9c0f-4e0c-8c8c-668f25fc6c4f-1795248240611.webm)

## Evidence handling notes

- RovaAI links are external and may require an authenticated session.
- No screenshots have been embedded in this repository yet.
- Evidence should be added only when genuine, relevant and free of credentials, personal information or payment details.
- Test result pages, shared suite reports and recordings are the primary traceability references for this iteration.
