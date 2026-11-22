# Project Overview

## 1. Background

This project evaluates RovaAI, an AI-powered browser testing platform, through selected customer-facing workflows on Daraz.lk. The exercise uses an e-commerce application to examine how well AI-driven execution can support functional, negative and edge-case testing.

## 2. Objectives

- Validate important shopping journeys from homepage discovery through product selection and cart authentication.
- Assess selected search, login, product quantity and navigation behaviours.
- Explore how RovaAI interprets natural-language test goals and executes browser actions.
- Review execution evidence and identify where a reported failure is caused by the application, test environment or automation constraints.
- Produce traceable, transparent QA documentation.

## 3. Systems and environment

| Component | Value |
|---|---|
| Application | [Daraz.lk](https://www.daraz.lk/) |
| Test platform | [RovaAI](https://app.rova.qa/) |
| RovaAI project | Ecommerce WebApp |
| Environment selected in RovaAI | Staging Env |
| Browser | Chromium (as configured for the Negative & Edge run) |

The application was tested as a black box. Internal source code, service implementation and database behaviour were not inspected.

## 4. Scope

### In scope
- Homepage and navigation checks.
- Search, filtering and sorting.
- Product search-result navigation and product detail information.
- Logged-out cart/purchase action authentication prompt.
- Shopping cart and wishlist behaviour up to the authentication boundary (logged out).
- Login form validation and incorrect-credential feedback.
- Product quantity boundaries and stock constraints.
- Invalid product URL handling.
- Rapid repeated login submission behaviour.
- RovaAI execution outcomes and automation limitations.

### Out of scope
- Completing checkout or making a payment.
- Full end-to-end order placement.
- Signing in, creating accounts or testing cart and wishlist functionality that requires authentication.
- Backend/API security verification or proof of SQL injection resistance.
- Load, stress or performance testing.
- Full cross-browser, device-lab or accessibility certification.
- Exhaustive coverage of all Daraz.lk features and user roles.

## 5. Deliverables

The repository documents the project approach, 52 test goals across five executed suites (5 of 6 planned suites), execution results, evidence links, and an evaluation of the testing platform's observed limitations.

## 6. Success criteria

- All selected test goals are represented in the test design.
- All five executed suites reach 100% execution completion.
- Raw tool statuses are preserved.
- Inconclusive outcomes are clearly separated from confirmed product defects.
- Evidence links and run-level summaries are provided for review.
