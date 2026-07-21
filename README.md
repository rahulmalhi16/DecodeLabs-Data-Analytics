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

# Project 2: Exploratory Data Analysis (EDA)
**DecodeLabs Data Analytics Internship — Industrial Training Kit**

## Overview
Following Project 1's data cleaning phase, this project performs exploratory data analysis
on the cleaned transactional dataset (1,200 records) to uncover patterns, trends, distributions,
and outliers — transforming a static table of numbers into actionable business insight.

## Methodology
Analysis performed using Python (Pandas, Matplotlib), following the IPO framework
(Input → Process → Output):
- **Descriptive statistics:** mean, median, five-number summary for all numeric fields
- **Outlier detection:** IQR method (1.5 × IQR beyond Q1/Q3)
- **Correlation analysis:** Pearson correlation coefficient across numeric variables
- **Trend analysis:** monthly revenue aggregation, categorical breakdowns

## Key Findings
1. **Order value is right-skewed** — mean ($1,053.97) exceeds median ($823.62), so median is
   the more reliable central tendency measure for TotalPrice.
2. **8 outliers detected in TotalPrice**, all confirmed as legitimate high-value bulk orders
   (max quantity × high unit-price products) — not data errors. No further cleaning needed.
3. **UnitPrice is the strongest driver of TotalPrice** (r = 0.72), stronger than Quantity
   (r = 0.62) — pricing strategy has more revenue leverage than order quantity.
4. **Chair and Printer are the top revenue-generating products** (~$195K each); Phone
   contributes the least despite similar order volume.
5. **Cancelled + Returned orders make up 41.4%** of all orders — a notable share worth
   root-cause investigation.
6. **Instagram drives the most orders (259)**; **Facebook customers spend the most per
   order** ($1,098.29 average); Referral has both the lowest volume and value.

## Recommendations
- Investigate the 41.4% Cancelled/Returned rate for revenue recovery opportunities
- Prioritize Facebook and Instagram acquisition channels
- Re-evaluate the Referral program's engagement strategy
- Consider targeted bulk-order promotions given the confirmed high-value outlier segment

## Files in This Repository
-  `Exploratory Data Analysis (EDA)`— full analysis report (problem statement, methodology, findings, recommendations)
- `Dataset_for_Data_Analytics_CLEANED.xlsx` — dataset used for analysis (from Project 1)

## Tools Used
Python, Pandas, Matplotlib — for reproducible statistical analysis and visualization.

---
*Part of the DecodeLabs Data Analytics Internship — Project 2 of the Industrial Training Kit.*
