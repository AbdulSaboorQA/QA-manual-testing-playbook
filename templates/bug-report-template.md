# Bug Report Template 

> **Purpose:** Create a clear, reproducible, developer-friendly defect report that minimizes back-and-forth.  
> **How to use:** Copy into Jira/Linear/GitHub Issues. Fill all **Required** fields. Add optional fields when helpful.  
> **Real-world note (experience-based):** This template reflects how I write bug reports in real delivery teams, based on **6+ years of hands-on QA experience** across web + mobile. It’s optimized to help engineers reproduce quickly (clear environment + steps + expected vs actual + evidence).

---

## 1) Bug summary

| Field | Value |
|---|---|
| Bug ID | *(e.g., BR-ECOM-001)* |
| Title | *(Sentence case; module + symptom + condition)* |
| Module / Component | |
| Severity | Blocker / Critical / Major / Minor / Trivial |
| Priority | P0 / P1 / P2 / P3 |
| Status | New / Triaged / In progress / Fixed / Reopen / Can’t repro |
| Reporter | |
| Reported on | *(YYYY-MM-DD)* |
| Assignee / Owner (optional) | |
| Labels / Tags (optional) | *(e.g., ios, safari, regression, checkout)* |

---

## 2) Summary / impact

| Field | Value |
|---|---|
| What’s broken | |
| User impact | *(conversion, revenue, trust, data integrity, access, etc.)* |
| Business impact (if known) | |
| Why it matters now | *(release blocker? affects P0 journey?)* |

---

## 3) Environment

| Field | Value |
|---|---|
| Environment | QA / Staging / Production |
| Build / Version | *(web tag, app build number, API version)* |
| Platform | Web / Mobile web / iOS / Android / API |
| Device | *(model)* |
| OS version | |
| Browser | *(name + version — for web/mobile web)* |
| Network | Wi-Fi / 4G / slow / flaky *(if relevant)* |
| Account / Role | guest / registered / admin *(never include real credentials)* |
| Locale / Region (optional) | |
| Time / Timezone (optional) | |
| App state (optional) | fresh install / upgraded / logged in/out |

---

## 4) Preconditions / test data

| Field | Value |
|---|---|
| Preconditions | *(e.g., logged in, cart has 1 item, coupon applied)* |
| Test data used | *(SKU/product, coupon, address type, payment method)* |
| Feature flags / experiments | *(on/off)* |
| 3rd-party dependency | *(payment gateway, OTP provider, map service)* |

---

## 5) Steps to reproduce

| Step # | Action |
|---:|---|
| 1 | |
| 2 | |
| 3 | |
| 4 | |

> Tip: Keep steps numbered, precise, and actionable (like a recipe). Avoid vague “observe” steps.

---

## 6) Results 

| Field | Value |
|---|---|
| Actual result | *(What happened after the last step? Include error text, state, and visible side effects.)* |
| Expected result | *(What should have happened instead?)* |

---

## 7) Reproducibility 

| Field | Value |
|---|---|
| Repro rate | *(1/1, 3/5, intermittent)* |
| Frequency | always / often / sometimes / once |
| Regression? | yes / no / unknown |
| Last known good build (if known) | |

---

## 8) Severity & priority definitions 

| Type | Options | Guidance |
|---|---|---|
| Severity (impact) | Blocker / Critical / Major / Minor / Trivial | Impact to core journey, security, revenue, data integrity, or usability |
| Priority (urgency) | P0 / P1 / P2 / P3 | Release urgency and scheduling |

---

## 9) Suspected cause / notes (Optional)

| Field | Value |
|---|---|
| Notes | *(timing issues, caching, race conditions, feature flags)* |
| Possible root cause | *(avoid guessing; keep evidence-based)* |
| Related tickets/PRs | |

---

## 10) Acceptance criteria for fix (Optional but great for clarity)

| Field | Value |
|---|---|
| Fix is verified when | *(clear pass conditions)* |
| Regression checks required | *(P0 journey list)* |
