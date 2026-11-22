# Test Plan and Strategy

## 1. Test approach

A risk-focused, black-box functional testing approach was used. Test goals were written in natural language and executed through RovaAI against Daraz.lk.

Three complementary suites were selected:

1. **Core Shopping Flow Validation** – positive and primary customer journey coverage.
2. **Negative & Edge Case Scenarios** – invalid input, boundary, authentication and resilience-oriented checks.
3. **Product Details & Product Selection** – product detail page content, variation selection, availability and navigation/refresh behaviour.

## 2. Coverage model

| Coverage area | Examples |
|---|---|
| Core navigation | Homepage, category navigation, product selection |
| Search and discovery | Keyword search, filters, sorting |
| Product information | Product detail content and quantity selector |
| Authentication | Login options, empty form, invalid credentials |
| Input robustness | Empty, malformed and special-character search/input |
| Boundary conditions | Quantity zero, non-numeric quantity, stock limit |
| Navigation errors | Non-existent product URL |
| Repeated actions | Rapid repeated login submissions |

## 3. Execution configuration

### Negative & Edge Case suite
- 12 test goals, sequential execution.
- Chromium.
- Continuity Mode enabled.
- Stop on Failure disabled for the complete run.
- Retries configured to 0.
- Complete run: 12/12 goals reached a terminal result.

### Core Shopping Flow suite
- 10 test goals, sequential execution.
- Stop on Failure was disabled before the complete execution.
- Historical suite configuration showed Continuity Mode disabled and one retry configured.
- Complete run: 10/10 goals reached a terminal result.

The Core suite's retry setting was retained as configured. This report does not assume that a retry occurred unless indicated in the run evidence.

## 4. Test data and safety

- Search terms included ordinary keywords, random strings and special characters.
- Login checks used invalid or empty input; no real account credentials are documented.
- Product quantity checks covered zero, non-numeric input and stock boundaries.
- Logged-out Add to Cart / Buy Now checks stopped at the login prompt or redirect. Checkout and payment were not completed.
- No passwords, personal account data or payment details are included in this repository.

## 5. Entry and exit criteria

**Entry:** application and RovaAI project/environment were accessible; the relevant test goals were configured.

**Exit:** every goal in each suite had a terminal status and the completed run summary was available. A suite can meet the execution-completion criterion while still containing failed or inconclusive goals.

## 6. Risks and constraints

| Risk / constraint | Handling |
|---|---|
| CAPTCHA blocks automated form interaction | Preserve the tool result; classify application behaviour as unverified |
| WAF blocks unusual search payloads | Do not infer a vulnerability or successful sanitization from the interstitial |
| Dynamic e-commerce content | Record observed behaviour in the execution report |
| Sequential run stops early | Disable Stop on Failure when a full suite result is required |
| Scope does not include backend inspection | Avoid claims about backend security or data integrity |

## 7. Result classification

- **Passed:** RovaAI marked the test goal as passed and the observed behaviour supported the goal.
- **Failed – tool-reported:** RovaAI marked the goal failed. Further analysis may show that the intended application behaviour was not reached.
- **Inconclusive:** the run did not provide enough evidence to decide whether the application meets the expected behaviour.
- **Confirmed defect:** use only when repeatable application evidence demonstrates behaviour contrary to a clear requirement. No confirmed product defect is asserted by this report.
