# Test Design – 22 Test Goals

The following test goals were configured in RovaAI. Expected behaviours below describe the intended validation; actual outcomes are recorded separately in the [execution report](../04-test-execution/execution-report.md).

## Suite A – Core Shopping Flow Validation (10)

| ID | Test goal | Expected behaviour |
|---|---|---|
| CSF-01 | Homepage loads correctly | Homepage renders its primary content and navigation without a blocking error. |
| CSF-02 | Search keyword and filters | A keyword search returns relevant results and available filters can be applied. |
| CSF-03 | Sort options | Selecting a sort option reorders the displayed results accordingly. |
| CSF-04 | Product selection from search opens correct detail page | Selecting a result opens the corresponding product detail page. |
| CSF-05 | Product detail page shows essential information | Product detail view presents key purchase information such as price and product/seller details. |
| CSF-06 | Cart while logged out triggers login modal | Attempting the cart action while logged out requests authentication. |
| CSF-07 | Login modal has authentication options | Login prompt displays the available authentication methods. |
| CSF-08 | Category dropdown | Category navigation can be opened and exposes category choices. |
| CSF-09 | PDP quantity selector | Product detail quantity control allows a valid quantity selection. |
| CSF-10 | Responsive UI across viewports | Key page content remains usable at the tested viewport sizes. |

## Suite B – Negative & Edge Case Scenarios (12)

| ID | Test goal | Expected behaviour |
|---|---|---|
| NEC-01 | Searching with random strings returns a “no results found” message | An unmatched query produces a clear no-results state rather than a broken page. |
| NEC-02 | Submitting an empty search query does not crash the page | The page remains stable and handles an empty search safely. |
| NEC-03 | Searching with special characters or SQL-injection-style strings is safely handled | The input is handled without an unsafe or broken application state; this UI test alone cannot prove backend SQL injection protection. |
| NEC-04 | Login attempts with malformed email/phone strings trigger validation | Malformed identifiers are rejected with appropriate validation feedback. |
| NEC-05 | Login attempts with incorrect credentials return appropriate error | Invalid credentials produce an appropriate error message. |
| NEC-06 | Submitting empty login form is blocked | Required-field validation prevents an empty submission. |
| NEC-07 | Product quantity field rejects 0 | Quantity cannot be set below the minimum permitted value. |
| NEC-08 | Product quantity field rejects non-numeric input | Quantity control retains or restores a valid numeric value. |
| NEC-09 | Quantity selection does not exceed available stock | The application prevents selection beyond available stock and communicates the limit. |
| NEC-10 | Add to Cart or Buy Now while logged out | The user is prompted to authenticate; test stops before checkout or payment. |
| NEC-11 | Navigation to non-existent product URL | An invalid product URL produces an appropriate not-found experience. |
| NEC-12 | Rapid repeated login submissions | Repeated rapid actions do not cause duplicate submission errors or an unstable page. |

## Coverage notes

- CSF-08, CSF-09 and CSF-10 were not completed in the earlier historical Core suite run, but were included in the later complete run.
- NEC-03 is a UI-level robustness scenario, not a substitute for dedicated security testing.
- NEC-10 is intentionally limited to authentication behaviour. No purchase or payment flow is performed.
