# Test Plan Template (Web + Mobile + API)

> **Document purpose:** Reusable test plan template for client projects (Web, Mobile, API).  
> **How to use:** Copy this file, fill placeholders, and keep a filled example in `/examples`.

---

## About this template (standards + practical usage)
This template is designed to be **generic and reusable**, while still matching **real-world test planning** expectations.

- **ISTQB-aligned:** A *test plan* documents the **scope, approach, resources, and schedule** of intended test activities, and identifies items such as **test items**, **features to be tested**, **test tasks**, **test environment**, **test design techniques**, **entry/exit criteria**, and **risks/contingencies**. :contentReference[oaicite:3]{index=3}  
- **IEEE 829-style structure:** Includes common elements such as **test items**, **features to be tested/not tested**, **approach**, **pass/fail criteria**, **suspension/resumption**, **deliverables**, **environmental needs**, **responsibilities**, **schedule**, **risks**, and **approvals**. :contentReference[oaicite:4]{index=4}  
- **Optional ISO/IEC/IEEE 29119 alignment:** The ISO 29119-3 standard provides templates/examples for test documentation; this template is compatible with that style if your client prefers ISO framing. :contentReference[oaicite:5]{index=5}  

> **Experience note:**  
> This template reflects my practical test planning approach across multiple client projects and domains, using risk-based execution and clear go/no-go criteria while remaining lightweight enough for Agile delivery.

---

## 0) Document control
- **Document ID:** TP-______
- **Project / Product:** ______
- **Test level:** System / Integration / UAT / Release / Regression
- **Version:** v0.__
- **Owner:** ______
- **Last updated:** YYYY-MM-DD
- **Approvers:** (PM/PO, Eng Lead, QA Lead)

### 0.1 Change log
| Version | Date | Author | Change summary |
|---|---|---|---|
| v0.1 | YYYY-MM-DD | ____ | Initial draft |
| v0.2 | YYYY-MM-DD | ____ | Updated scope / matrices / exit criteria |

### 0.2 Distribution / stakeholders
- **Primary:** QA, Eng Lead, PM/PO
- **Secondary:** Support, DevOps, Security, Analytics (as applicable)

---

## 1) References
Link the sources of truth that define “expected behavior” and constraints:
- PRD / Requirements: ______
- User stories / Tickets (Jira/Linear/etc.): ______
- UX designs (Figma): ______
- API specs (Swagger/Postman collection): ______
- Architecture / integration diagram: ______
- Release notes / change list: ______
- Past incidents / known issues: ______
- Compliance/security requirements (if applicable): ______

---

## 2) Purpose & objectives
### 2.1 Purpose
Describe why this plan exists (e.g., release validation for checkout changes, regression, new feature verification).

### 2.2 Test objectives (measurable)
- Objective 1: ______
- Objective 2: ______
- Objective 3: ______

### 2.3 Quality / release goals
Examples:
- **0 open Blocker/Critical defects** for conversion-critical journeys
- P0 suite execution coverage = **100%**
- Core journeys pass rate ≥ **X%**
- Crash-free sessions ≥ **X%** (mobile)

---

## 3) Scope
### 3.1 In-scope
List features/modules in scope (group by platform):

**Web:**
- ______

**Mobile (iOS/Android) / Mobile Web (if applicable):**
- ______

**APIs / Services:**
- ______

### 3.2 Out-of-scope
- ______ (and why)

### 3.3 Assumptions & dependencies
- **Assumptions:** ______
- **Dependencies:** payments provider, OTP/email/SMS, analytics, CDN, third-party SDKs, app stores, etc.

---

## 4) Test items
What is being tested (builds/services/environments):
- **Web URL(s):** ______
- **Mobile builds:** iOS (____), Android (____)
- **API base URL(s):** ______
- **Build identifiers:** commit hash / tag / version: ______

---

## 5) Test strategy (risk-based)
A test plan documents scope/approach/resources/schedule and includes items such as techniques, environment, entry/exit criteria, and risks/contingencies. :contentReference[oaicite:6]{index=6}

### 5.1 Risk assessment
| Risk | Impact | Likelihood | Coverage / mitigation |
|---|---|---:|---|
| Example: Payment failure handling | Revenue + trust | High | Negative tests + recovery + logs |
| Example: Mobile layout breaks | Conversion drop | Medium | Responsive/device matrix + smoke |

### 5.2 Test types included
Tick what applies and define the minimum “done” for each:
- Smoke
- Sanity
- Functional (P0/P1)
- Regression (change-based + risk-based)
- Exploratory (session-based)
- Compatibility (cross-browser / cross-device / cross-OS)
- Accessibility sweep (basic)
- API contract + negative tests
- Security-aware checks (basic)
- Performance smoke / load (if applicable)

### 5.3 Test design techniques
- Equivalence partitioning
- Boundary value analysis
- Decision tables
- State transitions
- Pairwise testing (configs)
- Exploratory testing “tours” (money-flow, interruption, error handling)

### 5.4 Traceability approach (lightweight but professional)
Choose one:
- **Stories → Scenarios → Defects**
- **Requirements → Test cases → Automation → Defects**
- **User journeys → Scenario sets → Defects**

Traceability location (tool/link): ______

### 5.5 Compatibility testing (MANDATORY)
Define how you’ll validate consistent behavior across browsers/devices.

**Web (cross-browser):**
- Primary browsers: ______
- Secondary browsers: ______
- Validate: rendering, forms, cookies/session, file uploads, payments flows, accessibility basics.

**Mobile (cross-device / cross-OS):**
- Device tiers (low/mid/high), OS coverage (N, N-1)
- Validate: UI scaling, touch targets, keyboard behaviors, permissions, deep links, notifications.

**Responsive breakpoints (web/mobile web):**
- Validate key screens at: 360×800, 390×844, 768×1024, 1366×768, 1920×1080 (adjust according to project needs).

**Network conditions (if relevant):**
- Offline, flaky network, slow 3G mindset for critical flows.

### 5.6 Regression strategy
- What is P0 regression: ______
- Selection method: change-based + risk-based
- Frequency: per PR / nightly / release candidate
- Automation contribution (if any): ______

---

## 6) Test environment & data
### 6.1 Environments
| Environment | Purpose | URL/Build | Notes |
|---|---|---|---|
| QA/Staging | full validation |  | mirrors prod (as much as possible) |
| Prod (sanity) | post-release |  | low-risk checks only |

### 6.2 Test data strategy
- Accounts/roles: ______
- Catalog/products: ______
- Payments sandbox methods: ______
- Data reset/cleanup: ______
- Data privacy rules (masking/anonymization if needed): ______

### 6.3 Tools (choose per project)
Examples (adapt as needed):
- Tracking: Jira / Linear
- API: Postman / Newman
- Automation: Selenium / Cypress / Playwright / Appium
- API automation: RestAssured (Java)
- Performance: k6 / JMeter
- Evidence: screen recordings, HAR, logs
- CI: GitHub Actions / Jenkins

---

## 7) Test configuration matrix
### 7.1 Browser matrix (Web)
| Browser | Version(s) | Priority | Notes |
|---|---|---:|---|
| Chrome | latest, n-1 | P0 | primary |
| Safari | latest | P0 | mac/iOS |
| Edge | latest | P1 | |
| Firefox | latest | P1 | |

### 7.2 Device/OS matrix (Mobile / Mobile web)
| Platform | Tier | OS versions | Priority | Notes |
|---|---|---|---:|---|
| iOS | mid/latest | N, N-1 | P0 | Safari / native |
| Android | low/mid/high | 10–latest | P0/P1 | Chrome |

---

## 8) Entry / exit / suspension criteria
### 8.1 Entry criteria
- Environment stable + build deployed
- Release notes/change list available
- Test data ready
- Dependencies reachable (payments, OTP/email, etc.)

### 8.2 Exit criteria (release recommendation)
- 100% of P0 tests executed
- 0 open Blocker/Critical defects (or explicitly accepted with risk)
- Compatibility checks complete for P0 screens/flows
- Test summary report produced

### 8.3 Suspension & resumption
Suspend if:
- Environment instability blocks execution > X hours
- P0 flow blocked for all users

Resume when:
- Fix deployed + smoke passes + blocked tests re-run

---

## 9) Test monitoring, control & communication
Test management includes **monitoring and control**: track progress/results/deviations, take corrective actions, and report status to stakeholders. :contentReference[oaicite:7]{index=7}

### 9.1 Execution tracking
- Source of truth (TestRail/Jira/Sheet): ______
- Progress tracking method: % executed, pass/fail/blocked, risk coverage: ______

### 9.2 Daily QA status update (template)
- Build tested: ______
- Scope executed today: ______
- Pass/Fail/Blocked: ___ / ___ / ___
- New defects (by severity): ______
- Key risks / concerns: ______
- Next focus (24h): ______

### 9.3 Bug triage
- Cadence: daily / weekly / on-demand
- Attendees: QA Lead, Eng Lead, PM/PO (+ others as needed)
- SLA for retest: ______

---

## 10) Defect management & quality bar
### 10.1 Severity definitions
- Blocker: core journey unusable / blocks testing
- Critical: major revenue/security/data integrity impact
- Major: significant feature broken with workaround
- Minor: low impact / UI / usability
- Trivial: polish/typos

### 10.2 Bug quality bar (minimum)
Every defect includes:
- Summary + user impact
- Environment/build
- Repro steps
- Expected vs actual
- Evidence (screenshots/video/logs)
- Frequency + scope (browsers/devices)

---

## 11) Deliverables
- Test plan
- Test scenarios/cases + traceability (if required)
- Execution evidence
- Defect reports
- Test summary report (release recommendation)
- (Optional) automation + CI reports

---

## 12) Roles & responsibilities
| Role | Name | Responsibilities |
|---|---|---|
| QA Lead |  | strategy, reporting, sign-off |
| QA |  | design, execution, defects |
| Eng Lead |  | fixes, clarifications |
| PM/PO |  | scope, acceptance decisions |

---

## 13) Schedule & milestones
| Activity | Owner | Start | End | Output |
|---|---|---|---|---|
| Planning | QA Lead |  |  | Approved plan |
| Test design | QA |  |  | Suite ready |
| Execution | QA |  |  | Runs + defects |
| Reporting | QA Lead |  |  | Summary report |

---

## 14) Risks & contingencies
| Risk | Impact | Mitigation | Contingency |
|---|---|---|---|
| Env instability | delays | early smoke | backup env / timebox |
| Limited devices | coverage gaps | pairwise | device farm |

---

## 15) Approvals
| Name | Role | Approval | Date |
|---|---|---|---|
|  | PM/PO | ✅/❌ |  |
|  | Eng Lead | ✅/❌ |  |
|  | QA Lead | ✅/❌ |  |
