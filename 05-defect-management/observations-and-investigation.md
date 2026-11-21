# Defect and Investigation Log

## Purpose

This log separates confirmed application defects from test observations and checks that could not be completed. It avoids treating every automated test failure as a product defect.

## Current status

**No confirmed application defects have been raised from the two completed suite runs documented in this repository.**

| Reference | Observation | Classification | Evidence / next action |
|---|---|---|---|
| OBS-01 / NEC-03 | Search payload triggered an Alibaba Cloud WAF HTTP 405 interstitial | Inconclusive – security layer/environment | [RovaAI result](https://app.rova.qa/results/10fa028d-0ffa-4b37-8e77-f3a65fd808c1). Reassess only in an authorized test environment where the application response can be observed. |
| OBS-02 / NEC-04 | Slider CAPTCHA prevented automated login form submission | Inconclusive – automation limitation | [RovaAI result](https://app.rova.qa/results/fe708e5f-69e7-4f11-99e3-4192a8f60da4). Perform an approved manual check or use a permitted test configuration. |
| OBS-03 / historical CSF-08 | Category dropdown interaction was not successful in an earlier incomplete run | Historical automation observation; not a current confirmed defect | The later complete Core suite reported 10/10 passed. See [complete run](https://app.rova.qa/suites/runs/40b15ceb-bcee-4873-831a-29606391b785). |

## Defect reporting decision

A defect should be raised only when there is sufficient evidence of repeatable application behaviour that violates an expected result. For each future confirmed defect, capture:

- Unique defect ID and concise title.
- Environment, browser and reproducible preconditions.
- Steps to reproduce.
- Expected and actual results.
- Supporting screenshot, recording, logs or network evidence.
- Severity, priority and affected workflow.
- Re-test result and closure status.

The current two tool-reported failures remain observations requiring follow-up, not confirmed product defects.
