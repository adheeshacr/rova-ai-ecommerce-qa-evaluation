# Test Design – 32 Test Goals

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
| CSF-08 | Category navigation | The user can access category choices through the category-navigation component defined by the current UI requirements. The exact expected component (dropdown, menu or category tiles) must be confirmed before this is used as a stable regression test. |
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

## Suite C – Product Details & Product Selection (10)

Test goal titles and expected outcomes are recorded as configured in RovaAI. The live RovaAI suite has not been changed.

| ID | Test goal | Expected behaviour (as configured in RovaAI) |
|---|---|---|
| PDS-01 | Verify product detail page opens successfully | Selecting a product from a listing opens the correct product detail page without errors. |
| PDS-02 | Verify product title and description are displayed correctly | The product title and description are visible, readable and relevant to the selected product. |
| PDS-03 | Verify product image gallery functionality | Product images load successfully, and users can navigate between available images. |
| PDS-04 | Verify product price and discount information | The current price, original price and discount information are displayed consistently when applicable. |
| PDS-05 | Verify product ratings and customer reviews section | Available ratings, review counts and customer reviews are displayed without broken content. |
| PDS-06 | Verify seller information section | Seller name and available seller information are displayed and accessible. |
| PDS-07 | Verify product variation options | Available options such as size, colour or model are displayed, and users can select an available variation. |
| PDS-08 | Verify unavailable product variations cannot be selected | Out-of-stock or unavailable variations are clearly identified and cannot be selected as available options. |
| PDS-09 | Verify product availability and stock information | Product availability information is displayed clearly and reflects the selected product or variation where applicable. |
| PDS-10 | Verify product detail page navigation and browser refresh behaviour | Refreshing the product page does not cause a broken page, and the selected product remains accessible. |

### PDS-08 – Recommended revised expected result

Manual follow-up showed that Daraz.lk allows an out-of-stock size to be selected and then prevents purchase, rather than blocking selection of the size itself (see the [execution report](../04-test-execution/execution-report.md)). The configured wording "cannot be selected" therefore does not match the observed design. The recommended revised expected result for documentation and any future suite revision is:

> Unavailable variations are clearly identified as out of stock when selected, and cannot be added to the cart or purchased.

This is a documentation recommendation only. The live RovaAI test goal has not been edited.

### PDS-10 – Coverage note

The configured expected outcome covers refresh behaviour only, although the goal title also refers to navigation. Back and Forward navigation were checked manually as a follow-up; consider adding them to the expected result if the goal is revised.

## Coverage and traceability notes

- The earlier historical Core suite run was incomplete (7 passed, 1 failed, 2 pending). The later execution evidence includes a complete run, but its shared report lists the CSF-08 category-navigation goal twice with conflicting outcomes. Refer to the [execution report](../04-test-execution/execution-report.md) for the reconciliation.
- NEC-03 is a UI-level robustness scenario, not a substitute for dedicated security testing.
- NEC-10 is intentionally limited to authentication behaviour. No purchase or payment flow is performed.
- Suite C (PDS-01 to PDS-10) uses live Daraz.lk listings, so the products selected by RovaAI can differ between runs. PDS-08 and PDS-10 required manual follow-up to interpret the expected behaviour and to cover navigation actions the automated run did not perform.
- Test-case expected behaviour should be based on an agreed requirement and the actual interface, not an assumed control label or layout.
