# Test Plan and Strategy

## 1. Test approach

A risk-focused, black-box functional testing approach was used. Test goals were written in natural language and executed through RovaAI against Daraz.lk.

Six suites were planned and created. Suites 1–5 were executed to completion; Suite 6 was stopped partway for safety:

1. **Core Shopping Flow Validation** – positive and primary customer journey coverage.
2. **Negative & Edge Case Scenarios** – invalid input, boundary, authentication and resilience-oriented checks.
3. **Product Details & Product Selection** – product detail page content, variation selection, availability and navigation/refresh behaviour.
4. **Search, Filters & Sorting** – keyword search, search suggestions, no-results handling, category and price filtering, price sorting, combined filters and clearing filters.
5. **Shopping Cart & Wishlist** – adding to cart, cart item details, quantity changes, subtotal, removal, empty-cart state, wishlist authentication and navigation between product, cart and wishlist pages.
6. **Checkout & Order Management** – checkout entry, authentication requirement, delivery address and options, order summary, subtotal and delivery charges, payment methods, required-field validation, navigation back to cart and the final order-submission boundary.

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
| Checkout | Checkout entry, delivery, totals, payment methods, validation and order boundary (logged out; stopped before any submission) |
| Cart and wishlist | Add to cart, quantity and subtotal, removal, empty cart, wishlist access (logged out; authentication boundary) |
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

### Shopping Cart & Wishlist suite
- 10 test goals, sequential execution.
- Chromium; Advanced Configuration enabled with the Desktop Chrome device profile.
- Stop on Failure disabled; retries configured to 0.
- Executed logged out. Suite scope excludes placing orders, making payments, creating accounts and bypassing login.
- Complete run: 10/10 goals reached a terminal result (2 passed, 8 failed in RovaAI).
- Execution status: executed; eight goals were blocked by Daraz.lk's authentication requirement for cart and wishlist access.

### Checkout & Order Management suite
- 10 test goals, sequential execution.
- Chromium; Desktop Chrome device profile active.
- Stop on Failure disabled; retries configured to 1.
- Executed logged out. Suite description prohibits opening login or registration pages, creating accounts, signing in, entering payment details and submitting or confirming orders.
- Execution status: stopped for safety during COM-08. 7 goals completed (5 passed, 2 failed in RovaAI), 1 stopped partway, 2 not run; reported completion 70%.
- Checkout functionality was not reached because checkout requires authentication.

## 4. Test data and safety

- Search terms included ordinary keywords, random strings and special characters.
- Login checks used invalid or empty input; no real account credentials are documented.
- Product quantity checks covered zero, non-numeric input and stock boundaries.
- Logged-out Add to Cart / Buy Now checks stopped at the login prompt or redirect. Checkout and payment were not completed.
- Checkout checks were performed logged out and were designed to stop before any order or payment submission. The Suite 6 run was stopped when the agent breached the no-registration boundary.
- Cart and wishlist checks were performed logged out. No account was created, no credentials were entered, and nothing was left in a cart.
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
| Cart and wishlist require an authenticated account | Record affected goals as blocked by authentication; do not sign in, create accounts or bypass login |
| Automation agent may breach safety boundaries (registration, personal data entry) despite instructions | Monitor live agent reasoning and stop the run immediately if a boundary is breached |
| Automation agent may attempt registration or age confirmation | Review step timelines after each run and add explicit "do not register" constraints to goals where needed |

## 7. Result classification

- **Passed:** RovaAI marked the test goal as passed and the observed behaviour supported the goal.
- **Failed – tool-reported:** RovaAI marked the goal failed. Further analysis may show that the intended application behaviour was not reached.
- **Blocked by authentication:** the goal could not reach the intended behaviour because the application requires a signed-in account. Not a defect.
- **Not run / stopped:** the goal was not completed because the run was stopped or cancelled.
- **Inconclusive:** the run did not provide enough evidence to decide whether the application meets the expected behaviour.
- **Confirmed defect:** use only when repeatable application evidence demonstrates behaviour contrary to a clear requirement. No confirmed product defect is asserted by this report.
