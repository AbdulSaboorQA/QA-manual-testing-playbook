# Bug report (eCommerce)

> **Purpose:** Showcase real-world bug reporting quality in a column-based layout (like Jira/Linear lists), while preserving the core details devs need: steps, expected vs actual, environment, evidence.  
> **Note:** All URLs/IDs are placeholders; no client data/PII included.

---

## Bug 1 — Payments (3DS cancel)

### A) Bug summary

| Field | Value |
|---|---|
| Bug ID | BR-ECOM-001 |
| Title | Checkout: “Pay now” stuck on infinite loader after 3DS cancel on iOS Safari |
| Module / Component | Checkout → Payments (3DS return/callback handling) |
| Severity | Critical |
| Priority | P0 |
| Status | New |
| Environment | Staging |
| Build / Version | web@R-2026.02-rc3 |
| Platform | Mobile web |
| Device | iPhone 13 |
| OS | iOS 17.3 |
| Browser | Safari iOS 17.3 |
| Network | Wi-Fi |
| Account / Role | Registered user |
| Reproducibility | Often (4/5) |
| Workaround | Refresh page (inconsistent; may show “processing” ~30s) |
| Evidence | Video + Screenshot + HAR (sanitized) |
| Reporter / Date | Abdul Saboor — 2026-02-19 |

### B) Preconditions / test data
| Field | Value |
|---|---|
| Preconditions | Logged in; cart has 1 in-stock item; shipping address selected |
| SKU | RM-TSHIRT-001 |
| Payment method | Card (3DS required) — sandbox |
| Flags / Experiments | None |

### C) Steps / expected / actual
| Step # | Action | Expected result | Actual result |
|---:|---|---|---|
| 1 | Login on staging | User logged in | Works |
| 2 | Add SKU RM-TSHIRT-001 to cart → checkout | Checkout opens | Works |
| 3 | Select **Card (3DS)** → **Pay now** | Redirect to 3DS | Works |
| 4 | On 3DS page tap **Cancel** | Return to Payment step; show “Cancelled”; allow retry/change method | Infinite loader; Pay now disabled; no message |

### D) Notes / acceptance criteria
| Area | Details |
|---|---|
| Notes | `/api/payments/confirm` sometimes hangs then returns 504 (intermittent). |
| Acceptance criteria | Cancel returns ≤2s; retry enabled; clear message; no stuck pending confirm; regress iOS Safari + Android Chrome |

---

## Bug 2 — Totals integrity (coupon + shipping recalculation)

### A) Bug summary

| Field | Value |
|---|---|
| Bug ID | BR-ECOM-002 |
| Title | Cart/Checkout: total amount not recalculated after removing coupon when shipping method is changed |
| Module / Component | Cart → Checkout (Totals calculation) |
| Severity | Critical |
| Priority | P0 |
| Status | New |
| Environment | Staging |
| Build / Version | web@R-2026.02-rc3 |
| Platform | Web |
| Device | MacBook / Desktop |
| OS | macOS 14.x |
| Browser | Chrome latest |
| Network | Wi-Fi |
| Account / Role | Guest or Registered (both) |
| Reproducibility | Always (5/5) |
| Workaround | Refresh cart page; totals correct only after refresh |
| Evidence | Screenshot + network log snippet |
| Reporter / Date | Abdul Saboor — 2026-02-19 |

### B) Preconditions / test data
| Field | Value |
|---|---|
| Preconditions | Cart has 2 items; coupon applied; shipping selectable at checkout |
| Coupon | SAVE10 (example) |
| Shipping methods | Standard + Express (example) |

### C) Steps / expected / actual
| Step # | Action | Expected result | Actual result |
|---:|---|---|---|
| 1 | Add 2 items to cart | Cart totals correct | Works |
| 2 | Apply coupon SAVE10 | Discount + totals update | Works |
| 3 | Proceed to checkout; select **Express** shipping | Shipping increases; totals update accordingly | Works |
| 4 | Remove coupon on checkout | Discount removed; totals recomputed with current shipping | Discount removed visually but **grand total stays discounted** (incorrect) |

### D) Notes / acceptance criteria
| Area | Details |
|---|---|
| Notes | Incorrect total can lead to undercharge/incorrect order summary. |
| Acceptance criteria | Removing coupon recalculates grand total immediately across cart/checkout/confirmation; totals consistent across API + UI |

---

## Bug 3 — Duplicate order risk (double tap / rapid click)

### A) Bug summary

| Field | Value |
|---|---|
| Bug ID | BR-ECOM-003 |
| Title | Checkout: double-clicking “Pay now” creates duplicate order attempts (two order IDs generated) |
| Module / Component | Checkout → Order creation / Payments |
| Severity | Critical |
| Priority | P0 |
| Status | New |
| Environment | Staging |
| Build / Version | web@R-2026.02-rc3 |
| Platform | Web |
| Device | Windows PC |
| OS | Windows 11 |
| Browser | Edge latest |
| Network | Wi-Fi |
| Account / Role | Registered user |
| Reproducibility | Often (3/5) |
| Workaround | Wait 3–5s before clicking; no in-app mitigation |
| Evidence | Screen recording + API logs (sanitized) |
| Reporter / Date | Abdul Saboor — 2026-02-19 |

### B) Preconditions / test data
| Field | Value |
|---|---|
| Preconditions | Cart has 1 item; payment method selected |
| Payment method | Card sandbox (non-3DS) |

### C) Steps / expected / actual
| Step # | Action | Expected result | Actual result |
|---:|---|---|---|
| 1 | Proceed to checkout and reach Payment step | Ready to place order | Works |
| 2 | Double-click **Pay now** rapidly | Button should lock after first click; only one order attempt | Two order attempts created (two order IDs); UI shows one confirmation but order history shows duplicates (intermittent) |

### D) Notes / acceptance criteria
| Area | Details |
|---|---|
| Notes | Indicates missing UI lock and/or missing idempotency on create-order endpoint. |
| Acceptance criteria | Button disables immediately; backend prevents duplicates for same cart/payment attempt; only one order created |

---

## Bug 4 — Search & filters (pagination resets filters)

### A) Bug summary

| Field | Value |
|---|---|
| Bug ID | BR-ECOM-004 |
| Title | Search: navigating to page 2 resets selected filters and shows unfiltered results |
| Module / Component | Search & Filters → Pagination |
| Severity | Major |
| Priority | P1 |
| Status | New |
| Environment | Staging |
| Build / Version | web@R-2026.02-rc3 |
| Platform | Web (responsive) |
| Device | Desktop |
| OS | macOS 14.x |
| Browser | Firefox latest |
| Network | Wi-Fi |
| Account / Role | Guest |
| Reproducibility | Often (4/5) |
| Workaround | Re-apply filters after every page change |
| Evidence | Screenshot set + query string comparison |
| Reporter / Date | Abdul Saboor — 2026-02-19 |

### B) Preconditions / test data
| Field | Value |
|---|---|
| Preconditions | Search returns > 50 results; multiple filters available |
| Filters | Brand = “X”, Price = “Low–Mid” (examples) |

### C) Steps / expected / actual
| Step # | Action | Expected result | Actual result |
|---:|---|---|---|
| 1 | Search for “shoes” | PLP shows results | Works |
| 2 | Apply Brand filter + Price range | Results filtered; filter chips visible | Works |
| 3 | Click pagination **2** | Page 2 should maintain filters | Filters visually remain, but results become unfiltered (query params dropped/intermittent) |

### D) Notes / acceptance criteria
| Area | Details |
|---|---|
| Notes | High UX impact; users see inconsistent discovery and lose trust in filters. |
| Acceptance criteria | Pagination preserves filters/sort in URL + API calls; filters and results stay consistent |

---

## Bug 5 — Mobile web UX (keyboard covers CTA)

### A) Bug summary

| Field | Value |
|---|---|
| Bug ID | BR-ECOM-005 |
| Title | Mobile web checkout: iOS keyboard hides “Continue/Pay” CTA on address & payment forms |
| Module / Component | Checkout → Forms (Mobile web) |
| Severity | Major |
| Priority | P1 |
| Status | New |
| Environment | Staging |
| Build / Version | web@R-2026.02-rc3 |
| Platform | Mobile web |
| Device | iPhone 12 |
| OS | iOS 16.7 |
| Browser | Safari iOS |
| Network | Wi-Fi |
| Account / Role | Guest |
| Reproducibility | Always (5/5) |
| Workaround | User must manually scroll; CTA sometimes remains unreachable until keyboard dismissed |
| Evidence | Screen recording |
| Reporter / Date | Abdul Saboor — 2026-02-19 |

### B) Preconditions / test data
| Field | Value |
|---|---|
| Preconditions | Checkout open on mobile web; address form requires multiple inputs |
| Fields | Phone, Address line 1, City, Postal code |

### C) Steps / expected / actual
| Step # | Action | Expected result | Actual result |
|---:|---|---|---|
| 1 | Open checkout on iOS Safari | Address step visible | Works |
| 2 | Tap into Phone / Address fields | Keyboard opens; form scrolls appropriately | Keyboard overlaps CTA; CTA not visible/reachable |
| 3 | Attempt to continue without dismissing keyboard | CTA should remain accessible (sticky or above keyboard) | User cannot reliably click CTA; forced to dismiss keyboard |

### D) Notes / acceptance criteria
| Area | Details |
|---|---|
| Notes | Increases friction; can block checkout completion for some users. |
| Acceptance criteria | CTA remains reachable when keyboard is open (sticky button above keyboard or auto-scroll); verified on iOS Safari + Android Chrome |
