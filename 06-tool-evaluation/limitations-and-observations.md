# RovaAI Evaluation – Observations and Limitations

## 1. Evaluation context

RovaAI was used to execute 42 distinct natural-language test goals across four e-commerce suites on Daraz.lk. The evaluation considered workflow coverage, browser interaction, result reporting and the interpretation of failed or blocked executions.

## 2. Observed strengths

- Supported execution of a 10-goal core shopping suite, a 12-goal negative and edge-case suite, a 10-goal product details and selection suite and a 10-goal search, filters and sorting suite.
- Produced individual result pages, suite-level run summaries and a shareable suite report.
- Supported browser-based checks of search, product discovery, authentication and quantity controls.
- Made it possible to inspect execution steps and retain run-specific evidence links.
- Result pages included step-by-step agent reasoning, a video recording and network data. The network data made it possible to identify the exact products used in the Suite 3 run for manual follow-up.
- Provided a useful starting point for AI-assisted test execution without first building a coded browser automation framework for these scenarios.

These are observations from this project, not a general benchmark of RovaAI against other test automation products.

## 3. Observed limitations

| Observation | Impact on testing | Practical response |
|---|---|---|
| WAF interstitial on unusual search input | Prevented the intended application response from being assessed | Record as blocked/inconclusive; use an approved test environment or manual follow-up |
| Slider CAPTCHA on login | Headless automation could not complete the challenge | Do not treat the failure as proof that validation is missing; arrange a permitted test path |
| Category-dropdown scenario appears twice in the shared Core report, with one passed and one failed record | Creates conflicting evidence for one of the 10 distinct test goals; the failed replay did not locate the expected dropdown control | Preserve both records, clarify the requirement and reconcile the source records before using a definitive Core pass rate |
| Long-running sequential suite | Progress appeared to pause and later continued; user observed 40%, then a Failed label, then progress resumed to 70% and 100% | Verify the final run summary before recording results; avoid starting duplicate runs while status is unclear |
| All ten Suite 3 goals showed Draft status before execution | The goals were still executable; status alone did not indicate readiness | Confirm goal status and suite configuration before running; do not assume Draft goals are blocked |
| One retry occurred for Suite 3 goal PDS-08 | The first attempt is not shown as a separate result record, so its observations cannot be reviewed afterwards | Note retries when monitoring; record any notable live agent reasoning at the time |
| PDS-08 required manual interpretation of the expected behaviour | RovaAI passed a goal whose configured wording ("cannot be selected") did not match the observed design (selectable, but purchase prevented) | Manually verify ambiguous passes and revise the expected result |
| PDS-10 could not use browser toolbar or refresh shortcuts | The automated run reloaded by navigating to the same URL and did not test Back/Forward | Follow up manually; the manual check also used browser commands because toolbar interaction was unavailable |
| SFS-09 passed although two brand filters were not verified together | An automated pass can be misleading when the test does not validate the full expected behaviour; RovaAI's final check used Brand plus Shipped From, which works, while manual checks showed a second brand replaces the first | Verify each combination named or implied by the goal; split brand + brand and brand + other filter into separate scenarios |
| SFS-05 and SFS-07 passed with thin automated evidence | A page heading and four prices were enough for RovaAI to report a pass | Confirm thin passes manually; both were confirmed |
| SFS-10 had an automation interaction failure followed by recovery | One step failed on element selection; the agent recovered and completed the check | Review step timelines, not only the final status |
| Suite 4 used zero retries | No retry attempts were available; all ten goals completed on the first attempt | Record the retry setting with each run, as it differed from Suite 3 (one retry) |
| All ten Suite 4 goals showed Draft status before execution | The goals were still executable | As for Suite 3, do not treat Draft status as blocking |
| Advanced Configuration showed optional device emulation | No device profile was shown as active; the run used a desktop layout | Record the active device or viewport setting with each run |

## 4. Quality of evidence and interpretation

A platform's status label is one part of the evidence, not the whole conclusion. For NEC-03 and NEC-04, RovaAI marked the goals failed, but the intended application behaviour was not reached. These are therefore preserved as tool-reported failures and classified as inconclusive for application quality.

The Core suite also has a reporting discrepancy. A separate run-statistics panel showed 10 passed and 0 failed, while the shared report contains 11 execution records (10 passed, 1 failed). The category-dropdown scenario is duplicated in that shared report: one 749.3-second passed record and one 894.0-second failed record. The failed replay did not locate the dropdown trigger expected by the test in the tested interface. This may indicate a test-design / interface mismatch or a difference between executions; the available evidence does not resolve the discrepancy.

A UI-level test using SQL-injection-style text cannot establish backend security. Dedicated security testing requires suitable authorization, test design and evidence.

### Suite 3 execution context

Suite 3 was monitored and its evidence reviewed using a separate built-in browser, because the Chrome browser extension was not connected at the time. This did not affect the RovaAI execution itself, which ran in RovaAI's own Chromium environment.

RovaAI reported all ten Suite 3 goals as passed. Automated pass status alone did not establish complete coverage: PDS-08 needed human interpretation of the expected result, and PDS-10's automated run did not exercise Back/Forward navigation or a true browser refresh. Both were followed up manually, as recorded in the [execution report](../04-test-execution/execution-report.md).

### Suite 4 execution context

RovaAI reported all ten Suite 4 goals as passed in 9 minutes 11 seconds with zero retries. SFS-09 shows how an automated pass can be misleading when the test does not validate the full expected behaviour: RovaAI tested a brand plus a shipping-location filter, but did not adequately verify two brands together. Manual verification of that combination failed against the current expected result. SFS-05 and SFS-07 passed with thin automated evidence and required manual checks to confirm them. Details are in the [execution report](../04-test-execution/execution-report.md).

## 5. Overall assessment

For this limited project, RovaAI enabled execution and reporting of selected browser-based workflows. The exercise also demonstrated that AI-generated browser actions and status labels require human review, especially when CAPTCHA, WAF responses, dynamic controls, duplicate execution records, retries, ambiguous expected results or long-running sessions are involved.

This evaluation does not claim that RovaAI replaces all manual or code-based testing. A balanced QA approach should combine AI-assisted execution with human review, targeted exploratory testing and specialist security/API/performance testing where required.

## 6. Recommended next evaluation steps

- Clarify the expected category-navigation behaviour and reconcile the duplicate Core execution record before assigning a definitive unique-goal result.
- Repeat the two blocked Negative & Edge checks through an approved test path that does not bypass production security controls.
- Capture and review evidence for responsive viewports and category navigation.
- Add dedicated API tests only after identifying supported endpoints and authorization.
- Plan a separate performance-testing exercise with defined workloads and measurable service-level expectations.
- Split SFS-09 into separate brand + brand and brand + other-filter scenarios, and clarify whether multi-brand selection is required, before any future Suite 4 rerun.
- Revise the PDS-08 expected result and consider adding Back/Forward navigation to PDS-10 before any future Suite 3 rerun.
- Expand regression coverage after the initial functional baseline is stable.
