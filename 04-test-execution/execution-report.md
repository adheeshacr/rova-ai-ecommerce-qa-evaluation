# Test Execution Report

## 1. Summary

Two RovaAI suites were executed against Daraz.lk. Both runs reached 100% completion, covering 22 test goals in total.

| Suite | Run date | Completed | Passed | Failed | Pending | Completion |
|---|---|---:|---:|---:|---:|---:|
| Core Shopping Flow Validation | 21 Nov 2026 | 10 | 10 | 0 | 0 | 100% |
| Negative & Edge Case Scenarios | 20 Nov 2026 | 12 | 10 | 2 | 0 | 100% |
| **Total** | | **22** | **20** | **2** | **0** | **100%** |

The combined pass count is 20/22 (90.9%). The two tool-reported failures require qualification: the intended application behaviour could not be fully assessed because of a WAF interstitial and a CAPTCHA challenge.

## 2. Core Shopping Flow Validation

**Run:** [Open complete RovaAI run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785)

- Execution date: 21 November 2026.
- Duration: 58 minutes 11 seconds.
- Completion: 100%.
- Result: 10 passed, 0 failed, 0 pending.
- Pass rate: 100%.

| ID | Test goal | Result | Observation |
|---|---|---|---|
| CSF-01 | Homepage loads correctly | Passed | Homepage content, banners, navigation, search and icons were visible and usable. |
| CSF-02 | Search keyword and filters | Passed | Search results and filter interaction worked in the observed run. |
| CSF-03 | Sort options | Passed | Results reordered for selected sort options such as price and rating. |
| CSF-04 | Product selection from search opens correct detail page | Passed | Selecting a search result opened its product detail page. |
| CSF-05 | Product detail page shows essential information | Passed | Price, ratings, seller metrics, delivery/warranty and installment information were observed. |
| CSF-06 | Cart while logged out triggers login modal | Passed | Logged-out cart action prompted authentication. |
| CSF-07 | Login modal has authentication options | Passed | Phone/email and Google/Facebook sign-in options were displayed. |
| CSF-08 | Category dropdown | Passed | Included in the complete run and marked passed by RovaAI. |
| CSF-09 | PDP quantity selector | Passed | Included in the complete run and marked passed by RovaAI. |
| CSF-10 | Responsive UI across viewports | Passed | Included in the complete run and marked passed by RovaAI. |

### Individual result references

- [CSF-01](https://app.rova.qa/results/a84722bb-8a89-4c0c-b21f-896b2897e139)
- [CSF-02](https://app.rova.qa/results/6e12eb71-e442-48cb-8018-67857f29ab3c)
- [CSF-03](https://app.rova.qa/results/f6c502ed-014d-4b17-83a0-eb6ea372e41c)
- [CSF-04](https://app.rova.qa/results/fb70191e-7a69-470e-ad50-a2a20742a0b8)
- [CSF-05](https://app.rova.qa/results/04847d0b-356c-43a0-8860-676d5e23922b)
- [CSF-06](https://app.rova.qa/results/f63e4e0c-51fd-4ea5-8013-5cc9b1d50b47)
- [CSF-07](https://app.rova.qa/results/4597b396-7991-405c-be51-2f857c7857d0)

The earlier historical run was incomplete (7 passed, 1 failed, 2 pending). The table above reports the later complete run, not the historical result.

## 3. Negative & Edge Case Scenarios

**Run:** [Open complete RovaAI run](https://app.rova.qa/suites/runs/02b1a04f-71b3-4cdf-ac8b-0e67f5620b13)

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

## 4. Analysis and follow-up

### NEC-03 – WAF interstitial
**Classification:** Inconclusive application check / environment or security-layer interference.

The WAF intercepted the test input before the intended application response could be evaluated. A separate controlled security test, with authorization and an appropriate test environment, would be needed to assess backend injection resistance.

### NEC-04 – CAPTCHA challenge
**Classification:** Inconclusive application check / automation limitation.

The CAPTCHA prevented the automated browser from submitting the malformed identifier. The result does not establish that application-side input validation is absent or defective. A permitted manual validation check or test environment with CAPTCHA handling configured would be needed.

### Historical CSF-08 result
An earlier incomplete run marked category dropdown interaction as failed because the headless browser could not interact with the control. The later complete run marked CSF-08 passed. The latest complete run is the reported suite result; the earlier history is retained here for context.

## 5. Overall conclusion

The Core Shopping Flow suite completed with 10/10 passed. The Negative & Edge Case suite completed with 10/12 passed and two automation/environment-blocked outcomes. Across both suites, 22/22 goals reached a terminal status, with 20 marked passed by RovaAI.

The results demonstrate meaningful workflow coverage and also show why test-result interpretation must go beyond the pass/fail label. No confirmed application defect is asserted from the two blocked checks.
