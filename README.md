# Project 1: Data Cleaning & Preparation
**DecodeLabs Data Analytics Internship — Industrial Training Kit**

## Overview
This project transforms a raw, messy transactional dataset (1,200 records) into a
production-ready "gold standard" dataset through a structured data cleaning and
preparation workflow.

## Dataset
- **Source:** Raw e-commerce transactional data
- **Size:** 1,200 records, 14 fields (OrderID, Date, CustomerID, Product, Quantity,
  UnitPrice, ShippingAddress, PaymentMethod, OrderStatus, TrackingNumber,
  ItemsInCart, CouponCode, ReferralSource, TotalPrice)

## What Was Done

### Phase 1 — Strategic Imputation
- Identified 309 missing values (25.75%) in the `CouponCode` field.
- Imputed with the explicit label `"No Coupon"` instead of mean/median/mode or
  row deletion, since the missing values represent *no coupon applied* rather
  than a random data gap — preserving full statistical power.

### Phase 2 — Integrity Audit
- Audited `OrderID` and `TrackingNumber` (unique identifiers) for duplicates.
- Checked for fully duplicated rows.
- Result: 0 duplicates found — 100% unique records confirmed.

### Phase 3 — Standardization
- Converted all `Date` values to strict **ISO 8601** format (`YYYY-MM-DD`).
- Trimmed whitespace and applied consistent **Title Case** across categorical
  text fields (`Product`, `PaymentMethod`, `OrderStatus`, `ReferralSource`) to
  prevent category fragmentation (e.g. `mumbai` vs `MUMBAI`).
- Standardized `UnitPrice` and `TotalPrice` to **2-decimal precision** for
  consistent currency formatting.

## Verification Gate Results
| Check | Result |
|---|---|
| Unique Identifier error rate | **0%** (1,200 / 1,200 unique) |
| Date format error rate | **0%** (ISO 8601 compliant) |
| Status | ✅ **Passed — cleared for Project 2** |

## Files in This Repository
- `Dataset_for_Data_Analytics_CLEANED.xlsx` — final cleaned, production-ready dataset
- `Change_Log.pdf` — full documentation of every change made (Change ID, Description, Impact, Status)
- `README.md` — this file

## Tools Used
Python, Pandas — chosen for reproducible, scriptable data cleaning workflows.

---
*Part of the DecodeLabs Data Analytics Internship — Project 1 of the Industrial Training Kit.*
