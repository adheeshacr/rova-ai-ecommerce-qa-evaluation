# RovaAI Evaluation – Observations and Limitations

## 1. Evaluation context

RovaAI was used to execute 22 natural-language test goals across two e-commerce suites. The evaluation considered workflow coverage, browser interaction, result reporting and the ability to interpret failures.

## 2. Observed strengths

- Supported execution of a complete 10-goal core shopping suite.
- Supported a 12-goal negative and edge-case suite.
- Produced individual result pages and suite-level run summaries.
- Covered several user-facing workflows without requiring a manually coded browser automation framework for these test goals.
- Made it possible to inspect the outcome of each goal and retain run-specific evidence links.

These are observations from this project, not a general benchmark of RovaAI against other test automation products.

## 3. Observed limitations

| Observation | Impact on testing | Practical response |
|---|---|---|
| WAF interstitial on unusual search input | Prevented the intended application response from being assessed | Record as blocked/inconclusive; use an approved test environment or manual follow-up |
| Slider CAPTCHA on login | Headless automation could not complete the challenge | Do not treat the failure as proof that validation is missing; arrange a permitted test path |
| Category dropdown interaction issue in an earlier run | One historical run could not interact with the control | Compare with the later complete run, which marked the goal passed |
| Long-running sequential suite | Progress appeared to pause and later continued; user observed 40%, then a Failed label, then progress resumed to 70% and 100% | Verify the final run summary before recording results; avoid starting duplicate runs while status is unclear |

## 4. Quality of evidence and interpretation

A platform's status label is one part of the evidence, not the whole conclusion. For NEC-03 and NEC-04, RovaAI marked the goals failed, but the intended application behaviour was not reached. These are therefore preserved as tool-reported failures and classified as inconclusive for application quality.

Likewise, a UI-level test using SQL-injection-style text cannot establish backend security. Dedicated security testing requires suitable authorization, test design and evidence.

## 5. Overall assessment

For this limited project, RovaAI enabled execution and reporting of the selected browser-based workflows. The exercise also exposed the importance of handling CAPTCHA, WAF responses, dynamic controls and long-running test sessions carefully.

This evaluation does not claim that RovaAI replaces all manual or code-based testing. A balanced QA approach should combine AI-assisted execution with human review, targeted exploratory testing and specialist security/API/performance testing where required.

## 6. Recommended next evaluation steps

- Repeat the two blocked checks through an approved test path that does not bypass production security controls.
- Capture and review evidence for responsive viewports and category navigation.
- Add dedicated API tests only after identifying supported endpoints and authorization.
- Plan a separate performance-testing exercise with defined workloads and measurable service-level expectations.
- Expand regression coverage after the initial functional baseline is stable.
