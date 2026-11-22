# Test Design – 62 Test Goals

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

## Suite D – Search, Filters & Sorting (10)

Test goal titles and expected outcomes are recorded as configured in RovaAI. The live RovaAI suite has not been changed.

| ID | Test goal | Expected behaviour (as configured in RovaAI) |
|---|---|---|
| SFS-01 | Search by valid product keyword | Relevant products are displayed for the entered keyword. |
| SFS-02 | Show search suggestions while typing | Relevant search suggestions are displayed and can be selected. |
| SFS-03 | Handle searches with no matching products | A clear no-results message or appropriate alternative suggestions are displayed without errors. |
| SFS-04 | Search using multiple keywords | Search results reflect the entered product terms and display relevant products. |
| SFS-05 | Filter search results by category | Selecting a category filter updates the results to show products belonging to that category. |
| SFS-06 | Filter products by minimum and maximum price | Products displayed fall within the selected price range, where matching products are available. |
| SFS-07 | Sort products by price low to high | Search results are ordered by ascending product price. |
| SFS-08 | Sort products by price high to low | Search results are ordered by descending product price. |
| SFS-09 | Apply multiple filters together | Search results satisfy all selected filters where matching products are available. |
| SFS-10 | Clear applied search filters | Clearing selected filters removes their restrictions and restores the unfiltered search results. |

### SFS-09 – Coverage clarification

The original goal and expected outcome are preserved above. The scenario did not distinguish between:

- combining two or more brand filters (multiple values within the same filter type); and
- combining a brand filter with a different filter type (for example, Brand plus Shipped From).

These combinations behaved differently during manual verification (see the [execution report](../04-test-execution/execution-report.md)). In a future test-design revision, separate them into distinct test scenarios, each with its own expected result, so that a pass for one combination cannot be read as coverage of the other. This is a documentation recommendation only; the live RovaAI test goal has not been edited.

## Suite E – Shopping Cart & Wishlist (10)

Test goal titles and expected outcomes are recorded as configured in RovaAI. The suite scope excludes placing orders, making payments, creating accounts and bypassing login requirements. The live RovaAI suite has not been changed.

| ID | Test goal | Expected behaviour (as configured in RovaAI) |
|---|---|---|
| SCW-01 | Add available product to cart | The available product is successfully added to the cart and appears as a cart line item. |
| SCW-02 | Display correct cart item details | The cart displays the correct product name, image, selected variation, and price for the added item. |
| SCW-03 | Increase cart item quantity | The cart item quantity increases by the expected amount and the line item remains present. |
| SCW-04 | Decrease cart item quantity | The cart item quantity decreases by the expected amount, respecting any minimum quantity. |
| SCW-05 | Update cart subtotal on quantity change | The cart subtotal recalculates correctly to reflect the changed quantity. |
| SCW-06 | Remove product from cart | The product is removed from the cart and no longer appears as a cart line item. |
| SCW-07 | Show empty-cart state after removal | The cart displays the appropriate empty-cart state after all products are removed. |
| SCW-08 | Check wishlist action authentication requirement | The wishlist action is attempted without signing in; if authentication is required, it is recorded as blocked by the authentication requirement rather than bypassed. |
| SCW-09 | View and remove wishlist product if unauthenticated | If the wishlist is accessible without signing in, the product can be viewed and removed; otherwise the attempt is recorded as blocked by authentication. |
| SCW-10 | Navigate between product and cart pages | The user can navigate among product listings, product details, shopping cart, and wishlist without errors. |

### Suite E – Authentication boundary

On Daraz.lk, adding to the cart, viewing the cart, adding to the wishlist and viewing the wishlist all require a signed-in account. Because this project does not sign in or create accounts, SCW-02 to SCW-07 and the cart and wishlist parts of SCW-09 and SCW-10 cannot be fully exercised. Functional cart and wishlist behaviour beyond the login boundary would require an approved test account and a separate test design.

## Suite F – Checkout & Order Management (10)

Test goal titles and expected outcomes are recorded as configured in RovaAI. The suite description instructs the agent not to open login or registration pages, create accounts, sign in, enter payment details, submit orders or confirm purchases, and to stop before any irreversible checkout action.

| ID | Test goal | Expected behaviour (as configured in RovaAI) |
|---|---|---|
| COM-01 | Verify checkout navigation from shopping cart | The checkout action navigates to the appropriate checkout page or displays the authentication requirement. |
| COM-02 | Verify authentication requirement for checkout access | If authentication is required, the application clearly displays the login requirement without creating an account or signing in. |
| COM-03 | Verify delivery address section during checkout | The delivery address section displays the appropriate fields or clearly indicates that authentication is required. |
| COM-04 | Verify available delivery options during checkout | Available delivery methods and their relevant information are displayed correctly, or access restrictions are identified. |
| COM-05 | Verify checkout order summary product information | The order summary displays the correct product name, image, selected variation and quantity. |
| COM-06 | Verify checkout subtotal and delivery charges | The subtotal, delivery charges and total amount are displayed consistently with the cart information. |
| COM-07 | Verify available payment methods during checkout | Available payment methods are displayed clearly, or authentication restrictions are recorded. |
| COM-08 | Verify required-field validation in checkout form | Required delivery fields display appropriate validation messages when left empty. Do not submit an order. |
| COM-09 | Verify navigation from checkout back to shopping cart | The user can return to the cart without unexpected errors or broken navigation. |
| COM-10 | Verify no final order submission without explicit confirmation | The final order submission control is identifiable, and the test stops before clicking any Place Order, Confirm Order or payment submission button. |

### Suite F – Coverage note

Several Suite F expected outcomes accept either the functional result or a recorded authentication restriction ("…or authentication is required"). A RovaAI pass for those goals therefore confirms the login requirement, not the checkout feature. In a future revision, separate the authentication check (COM-02) from functional checkout checks, which require an approved authenticated test account. COM-08 to COM-10 were not completed because the run was stopped for safety.

## Coverage and traceability notes

- The earlier historical Core suite run was incomplete (7 passed, 1 failed, 2 pending). The later execution evidence includes a complete run, but its shared report lists the CSF-08 category-navigation goal twice with conflicting outcomes. Refer to the [execution report](../04-test-execution/execution-report.md) for the reconciliation.
- NEC-03 is a UI-level robustness scenario, not a substitute for dedicated security testing.
- NEC-10 is intentionally limited to authentication behaviour. No purchase or payment flow is performed.
- Suite C (PDS-01 to PDS-10) uses live Daraz.lk listings, so the products selected by RovaAI can differ between runs. PDS-08 and PDS-10 required manual follow-up to interpret the expected behaviour and to cover navigation actions the automated run did not perform.
- Suite D (SFS-01 to SFS-10) also uses live Daraz.lk listings and filter values. SFS-05 and SFS-07 were confirmed manually because the automated evidence was limited, and SFS-09 required manual verification of multi-brand filtering.
- Suite E (SCW-01 to SCW-10) was executed logged out. Most goals reached the authentication boundary; see the [execution report](../04-test-execution/execution-report.md) for the classification of each goal.
- Suite F (COM-01 to COM-10) was executed logged out and stopped partway for safety; no checkout functionality was verified. See the [execution report](../04-test-execution/execution-report.md).
- Test-case expected behaviour should be based on an agreed requirement and the actual interface, not an assumed control label or layout.
