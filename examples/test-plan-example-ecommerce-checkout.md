# Test Plan (Example) — E-commerce Checkout Release Validation (Web + Mobile Web + API)

> **Document purpose:** Filled example that demonstrates how I plan and execute testing for a conversion-critical eCommerce release.  
> **How to use:** Keep this file in `/examples` and keep a reusable blank template in `/templates`.

---

## 1) Document control
- **Document ID:** TP-ECOM-REL-001
- **Project / Product:** ReMarket (demo eCommerce marketplace)
- **Test level:** Release / Regression (System-level)
- **Version:** v1.0
- **Owner:** Abdul Saboor (QA)
- **Last updated:** 2026-02-19
- **Approvers:** PM/PO, Eng Lead, QA Lead

### 1.1 Change log
| Version | Date | Author | Change summary |
|---|---|---|---|
| v0.1 | 2026-02-13 | Abdul Saboor | Initial draft |
| v0.9 | 2026-02-16 | Abdul Saboor | Updated scope + risk table + compatibility matrices |
| v1.0 | 2026-02-19 | Abdul Saboor | Finalized entry/exit criteria + monitoring/triage cadence |

### 1.2 Distribution / stakeholders
- **Primary:** QA, Eng Lead, PM/PO
- **Secondary:** Support, DevOps/SRE, Analytics, Security (as applicable)

---

## 2) References
Link the sources of truth that define “expected behavior” and constraints:
- PRD / Requirements: `PRD-ReMarket-Checkout-R2026.02 (internal link)`
- User stories / Tickets (Jira/Linear/etc.): `Jira Epic: CHECKOUT-REL-2026-02`
- UX designs (Figma): `Figma: Checkout + Cart Revamp (internal link)`
- API specs (Swagger/Postman collection): `Postman Collection: ReMarket Checkout APIs (internal link)`
- Architecture / integration diagram: `Checkout + Payments Integration Diagram (internal link)`
- Release notes / change list: `Release Notes R-2026.02 (internal link)`
- Past incidents / known issues: `Incident Log: Payment timeouts & duplicate order edge cases (internal link)`
- Compliance/security requirements (if applicable): `PCI considerations (high-level) + Logging/PII rules (internal link)`

---

## 3) Purpose & objectives
### 3.1 Purpose
Validate release readiness for conversion-critical journeys:
**Search → PLP → PDP → Cart → Checkout → Payment → Order confirmation**
across **desktop web + mobile web**, with key **API contract/negative checks**, using risk-based coverage and clear go/no-go criteria.

### 3.2 Test objectives (measurable)
- **P0 execution:** 100% of P0 tests executed on release candidate build(s).
- **Payment reliability:** Validate payment success + failure modes (decline/cancel/timeout) with correct recovery and **no duplicate orders/charges**.
- **Totals integrity:** Cart/checkout/confirmation totals consistent (items, discounts, shipping, taxes—where applicable).
- **Compatibility:** Complete P0 compatibility coverage across defined **browser/device matrix** and capture evidence for P0 journeys.
- **Defect quality:** 100% defects logged with reproducible steps + evidence + environment + severity.

### 3.3 Quality / release goals
- **0 open Blocker/Critical defects** for conversion-critical journeys at sign-off (or explicitly accepted with documented risk).
- **P0 suite execution coverage = 100%**
- **Core journeys pass rate ≥ 95%** (excluding known accepted issues)
- **Mobile web usability:** no layout/input issues that block checkout completion on P0 devices

---

## 4) Scope
### 4.1 In-scope
List features/modules in scope (group by platform):

**Web:**
- Authentication basics (login/session persistence)
- Search & Filters (query, autosuggest, filter combos, sort, pagination)
- PLP/PDP (pricing, images, variants, availability)
- Cart (add/remove/update qty, coupon/discount, totals recalculation)
- Checkout (address, shipping method, order review)
- Payment (sandbox): success + decline + cancel/timeout + retry behaviors
- Post-order (basic): confirmation page + order visible in account

**Mobile (iOS/Android) / Mobile Web :**
- Mobile web parity for P0 journeys (Search → Checkout)
- Touch/keyboard behaviors on key forms (address, phone, coupon fields)
- Responsive layouts on critical screens (PLP/PDP/Cart/Checkout/Confirmation)

**APIs / Services:**
- Auth/session endpoints (contract + negative)
- Search/catalog endpoints (basic contract + query parameter validation)
- Cart/checkout endpoints (contract + negative + state correctness)
- Order creation/payment intent endpoints (as applicable)

### 4.2 Out-of-scope
- Admin/merchant/back-office portals (not required for release sign-off)
- Deep security penetration testing (security-aware checks only)
- Full localization sweep (smoke only for primary locale)
- Full performance/load testing (only performance smoke / observational checks)
- Third-party analytics dashboards validation (events sanity only, if requested)

### 4.3 Assumptions & dependencies
- **Assumptions:** Staging environment mirrors production configuration as much as possible; release notes are accurate; required feature flags are documented.
- **Dependencies:** Payments provider sandbox, OTP/email/SMS, CDN/cache, analytics events, third-party SDKs, fraud/3DS flows (if applicable).

---

## 5) Test items
What is being tested (builds/services/environments):
- **Web URL(s):** `https://staging.remarket.example` (placeholder)
- **Mobile builds:** N/A (mobile web focus for this release)
- **API base URL(s):** `https://api-staging.remarket.example` (placeholder)
- **Build identifiers:** `web@R-2026.02-rc3`, `api@R-2026.02-rc3` (placeholder)

---

## 6) Test strategy (risk-based)
A test plan documents scope/approach/resources/schedule and includes items such as techniques, environment, entry/exit criteria, and risks/contingencies.

### 6.1 Risk assessment
| Risk | Impact | Likelihood | Coverage / mitigation |
|---|---|---:|---|
| Incorrect totals/discounts (cart vs checkout) | Revenue loss + trust | High | Totals validation checkpoints at cart/checkout/confirmation; boundary tests for qty/coupons |
| Duplicate orders/charges on retry/refresh | Financial + support cost | High | Retry/refresh/back tests; order state verification; idempotency-like validation (no duplicate order IDs) |
| Payment failure handling (decline/timeout/cancel) | Conversion drop | High | Negative tests + recovery flows; consistent user messaging; safe re-try |
| Mobile web layout/input breaks checkout | High drop-off | Medium | Device matrix + responsive checkpoints; form usability checks |
| Session expiry mid-checkout | Abandoned carts | Medium | Token/session expiry simulation; re-auth behavior; cart persistence |
| Search/filter incorrect or unstable | Discovery issues | Medium | Filter combos + pagination; sort correctness; empty/no-result states |
| Third-party dependency instability | Blocks testing | Medium | Timeboxing + fallback routes; early smoke; clear suspension criteria |

### 6.2 Test types included
Tick what applies and define the minimum “done” for each:
- **Smoke:** 15–25 checks; 1 successful sandbox order on Chrome + 1 on mobile web
- **Sanity:** targeted checks after fixes (checkout/payment/search)
- **Functional (P0/P1):** core modules + negative/edge cases
- **Regression (change-based + risk-based):** focus on checkout + affected surfaces
- **Exploratory (session-based):** money-flow + interruption + error-message tours
- **Compatibility:** cross-browser + cross-device + cross-OS (mobile web)
- **Accessibility sweep (basic):** focus order, labels, keyboard nav on checkout forms
- **API contract + negative tests:** auth/cart/checkout/order endpoints
- **Security-aware checks (basic):** PII exposure in UI/logs, auth/session basics
- **Performance smoke:** key pages responsiveness; basic Web Vitals sanity (if available)

### 6.3 Test design techniques
- Equivalence partitioning (coupon types, shipping rules buckets, payment outcomes)
- Boundary value analysis (qty limits, coupon length, address fields, phone formats)
- Decision tables (coupon eligibility, shipping method rules)
- State transitions (cart empty → filled → checkout → payment success/failure)
- Pairwise testing (browser/device combinations)
- Exploratory testing “tours”:
  - Money-flow tour
  - Interruption tour (refresh/back/tab close/app switch)
  - Error-handling tour (timeouts, no internet, decline)

### 6.4 Traceability approach (lightweight but professional)
Choose one:
- **User journeys → Scenario sets → Defects** ✅ (selected for this release)

Traceability location (tool/link):
- `Jira Epic CHECKOUT-REL-2026-02 → Scenario Set IDs (Sheet/TestRail) → Defects`

### 6.5 Compatibility testing (MANDATORY)
Define how you’ll validate consistent behavior across browsers/devices.

**Web (cross-browser):**
- Primary browsers: **Chrome (latest, n-1), Safari (latest)**
- Secondary browsers: **Edge (latest), Firefox (latest)**
- Validate: rendering/layout, forms/validation, cookies/session, payment redirects/returns, file uploads (if any), basic accessibility behaviors.

**Mobile (cross-device / cross-OS) — Mobile Web focus:**
- Device tiers: **mid/latest iPhone**, **mid-range Android**, **low-end Android (P1)**
- OS coverage: **iOS N/N-1**, **Android 10–latest (prioritize 12–14)**
- Validate: responsive layout, touch targets, keyboard/autofill behaviors, input masking, address forms, coupon entry, payment return flow.

**Responsive breakpoints (web/mobile web):**
- Validate key screens at:
  - 360×800 (small Android)
  - 390×844 (iPhone)
  - 768×1024 (tablet)
  - 1366×768 (laptop)
  - 1920×1080 (desktop)

**Network conditions (if relevant):**
- Offline / airplane mode (mobile)
- Flaky network mindset (timeouts/retries)
- Slow 3G mindset for checkout steps (especially payment redirects)

### 6.6 Regression strategy
- What is P0 regression:
  - Search → PDP → Cart → Checkout → Payment → Confirmation
  - Coupon apply/remove + totals verification
  - Payment decline → recovery → success
  - Timeout/cancel → recover without duplicate orders
- Selection method: **change-based** (touched modules) + **risk-based** (money flow)
- Frequency: **per release candidate build** + retest after fix batches
- Automation contribution (if any):
  - Optional: **Cypress/Playwright** smoke for P0 journey on Chrome
  - Optional: **Newman** run for key API contract checks (auth/cart/checkout)

---

## 7) Test environment & data
### 7.1 Environments
| Environment | Purpose | URL/Build | Notes |
|---|---|---|---|
| QA/Staging | full validation | `staging.remarket.example` | mirrors prod (as much as possible) |
| Prod (sanity) | post-release | `remarket.example` | low-risk checks only |

### 7.2 Test data strategy
- Accounts/roles:
  - Guest (if supported)
  - Registered user (standard)
  - User with saved address + prior orders
- Catalog/products:
  - In-stock vs low-stock
  - Variants (size/color)
  - Discounted + coupon-eligible items
- Payments sandbox methods:
  - “Success” payment method
  - “Decline” payment method
  - “Cancel/timeout” simulation (if provider supports)
- Data reset/cleanup:
  - Dedicated “QA orders” tag OR daily cleanup of test orders in staging
- Data privacy rules (masking/anonymization if needed):
  - Do not use real PII; use synthetic names/emails/phones
  - No screenshots containing full payment details; redact where needed

### 7.3 Tools (choose per project)
Examples (adapt as needed):
- Tracking: **Jira / Linear**
- API: **Postman**
- Automation: **Selenium / Cypress / Playwright / Appium**
- API automation: **RestAssured (Java)**
- Performance: **k6 / JMeter**
- Evidence: screen recordings, logs
- CI: **GitHub Actions**

---

## 8) Test configuration matrix
### 8.1 Browser matrix (Web)
| Browser | Version(s) | Priority | Notes |
|---|---|---:|---|
| Chrome | latest, n-1 | P0 | primary |
| Safari | latest | P0 | mac/iOS |
| Edge | latest | P1 | checkout smoke + key pages |
| Firefox | latest | P1 | search + checkout smoke |

### 8.2 Device/OS matrix (Mobile / Mobile web)
| Platform | Tier | OS versions | Priority | Notes |
|---|---|---|---:|---|
| iOS | mid/latest | N, N-1 | P0 | Safari (mobile web) |
| Android | mid-range | 12–14 | P0 | Chrome (mobile web) |
| Android | low-end | 10–12 | P1 | Chrome (smoke + key pages) |

---

## 9) Entry / exit / suspension criteria
### 9.1 Entry criteria
- Environment stable + build deployed
- Release notes/change list available
- Test data ready (accounts/catalog/payment sandbox)
- Dependencies reachable (payments, email/OTP, etc.)
- Smoke suite passes OR known issues documented and accepted for start

### 9.2 Exit criteria (release recommendation)
- **100% of P0 tests executed**
- **0 open Blocker/Critical defects** (or explicitly accepted with documented risk)
- **Compatibility checks complete** for P0 screens/flows (per matrix)
- Test summary report produced (go/no-go + key risks + known issues)

### 9.3 Suspension & resumption
Suspend if:
- Environment instability blocks execution > 2 hours
- P0 flow blocked for all users
- Payment sandbox outage blocks all payment validation

Resume when:
- Fix deployed + smoke passes + blocked tests re-run
- Dependencies recovered (payments/email/OTP)

---

## 10) Test monitoring, control & communication
Test management includes monitoring and control: track progress/results/deviations, take corrective actions, and report status to stakeholders.

### 10.1 Execution tracking
- Source of truth (TestRail/Jira/Sheet): `Test Execution Sheet (internal link)` / `Jira Test cycles` (placeholder)
- Progress tracking method:
  - % executed (P0/P1)
  - Pass/Fail/Blocked counts
  - Compatibility coverage checklist completion
  - Defects by severity + aging

### 10.2 Daily QA status update (template)
- Build tested: `web@____ / api@____`
- Scope executed today: `P0 checkout + payments / search regression / etc.`
- Pass/Fail/Blocked: `__ / __ / __`
- New defects (by severity): `Blocker:__ Critical:__ Major:__ Minor:__`
- Key risks / concerns: `____`
- Next focus (24h): `____`

### 10.3 Bug triage
- Cadence: **Daily during release window** (or on-demand for P0 blockers)
- Attendees: QA Lead, Eng Lead, PM/PO (Support/DevOps optional)
- SLA for retest:
  - Blocker/Critical: same day (when new build available)
  - Major: within 24–48h depending on release timeline

---

## 11) Defect management & quality bar
### 11.1 Severity definitions
- **Blocker:** core journey unusable / blocks testing
- **Critical:** major revenue/security/data integrity impact (incorrect charges, duplicate orders, broken payment)
- **Major:** significant feature broken with workaround
- **Minor:** low impact / UI / usability
- **Trivial:** polish/typos

### 11.2 Bug quality bar (minimum)
Every defect includes:
- Summary + user impact (conversion/revenue angle where relevant)
- Environment/build
- Repro steps + test data used
- Expected vs actual
- Evidence (screenshots/video/logs/HAR as needed)
- Frequency + scope (browsers/devices affected)

---

## 12) Deliverables
- Test plan (this document)
- Test scenarios/cases + traceability (if required)
- Execution evidence
- Defect reports
- Test summary report (release recommendation)
- (Optional) automation + CI reports (Cypress/Playwright/Newman)

---

## 13) Roles & responsibilities
| Role | Name | Responsibilities |
|---|---|---|
| QA Lead | (Name) | strategy, reporting, sign-off |
| QA | (Name) | design, execution, defects |
| Eng Lead | (Name) | fixes, clarifications |
| PM/PO | (Name) | scope, acceptance decisions |

---

## 14) Schedule & milestones
| Activity | Owner | Start | End | Output |
|---|---|---|---|---|
| Planning | QA Lead | 2026-02-15 | 2026-02-15 | Approved plan |
| Test design updates | QA | 2026-02-15 | 2026-02-16 | P0/P1 suite ready |
| Execution (cycle 1) | QA | 2026-02-16 | 2026-02-18 | Runs + defects |
| Fix verification + regression | QA | 2026-02-18 | 2026-02-19 | Retest + regression notes |
| Reporting | QA Lead | 2026-02-19 | 2026-02-19 | Summary report + recommendation |

---

## 15) Risks & contingencies
| Risk | Impact | Mitigation | Contingency |
|---|---|---|---|
| Env instability | delays | early smoke, timebox | backup env / extend window |
| Payment sandbox outage | blocks validation | validate non-payment flows first | partial sign-off + rerun when restored |
| Limited device access | coverage gaps | pairwise + prioritize P0 | device farm / borrow devices |
| Late scope changes | churn | freeze daily scope | re-baseline plan + risk callout |

---

## 16) Approvals
| Name | Role | Approval | Date |
|---|---|---|---|
|  | PM/PO | ✅/❌ |  |
|  | Eng Lead | ✅/❌ |  |
|  | QA Lead | ✅/❌ |  |
