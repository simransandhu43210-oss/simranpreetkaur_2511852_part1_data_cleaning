# Data Cleaning Log
## Project: Business Data Cleaning, Validation & Excel Reporting
## File: cleaned_orders.xlsx
## Total Raw Rows: 932 | Total Cleaned Rows: 912

---

## 1. Issues Found

| Issue | Count |
|---|---|
| Exact duplicate rows | 20 |
| Conflicting duplicate order_ids | 12 (24 rows) |
| Missing region | 26 |
| Missing ship_mode | 22 |
| Missing discount | 18 |
| Invalid negative discount | 15 |
| Discount above allowed range (>0.25) | 15 |
| Ship date before order date | 22 |
| Mixed date formats | 4 formats across all rows |
| Inconsistent text casing | Multiple columns |

---

## 2. Cleaning Actions Performed

- Removed 20 exact duplicate rows, keeping first occurrence
- Flagged 24 rows with conflicting order_ids in duplicate_review_note column
- Applied TRIM and PROPER functions to: customer_name, segment, region, state, city, category, sub_category, ship_mode, payment_status, order_status
- Standardized all date formats to consistent date values in order_date and ship_date columns
- Filled 26 missing region values with "Unknown"
- Filled 22 missing ship_mode values with "Unknown"
- Converted text-format discounts (70%, 85%) to decimal equivalents
- Flagged negative and above-range discounts in discount_validity_flag column
- Set cleaned_discount to 0 for invalid/missing discounts where applicable

---

## 3. Business Rules Applied

| Rule | Action Taken |
|---|---|
| Missing region | Filled as "Unknown", flagged in missing_field_flag |
| Missing ship_mode | Filled as "Unknown", flagged in missing_field_flag |
| Missing discount | Treated as 0 if all other sales fields valid |
| Negative discount | Flagged as invalid, cleaned_discount set to 0 |
| Discount above 0.25 | Flagged as invalid, cleaned_discount set to 0 |
| Cancelled orders | Categorized as "Excluded - Cancelled" in sales_summary_category |
| Failed payments | Categorized as "Excluded - Failed Payment" in sales_summary_category |
| Refunded orders | Categorized as "Refunded - Separate Summary" |
| Ship date before order date | Flagged as "Ship date before order date" in date_issue_flag |

---

## 4. Assumptions Made

- Slash-format dates (MM/DD/YYYY) treated as US format based on data evidence
- Dash-format dates (DD-MM-YYYY) confirmed as day-first based on data evidence
- Valid discount range assumed to be 0 to 0.25 based on majority of data
- Text discounts "70%" and "85%" converted to 0.70 and 0.85, then flagged as above allowed range
- Missing discounts defaulted to 0 only when quantity, unit_price, sales, cost, profit all present
- Conflicting duplicate order_ids kept in dataset and flagged rather than deleted

---

## 5. Records Removed

- 20 exact duplicate rows removed
- No other rows deleted

---

## 6. Records Flagged

- 24 rows flagged in duplicate_review_note as conflicting duplicates
- 22 rows flagged in date_issue_flag as ship date before order date
- 15 rows flagged in discount_validity_flag as invalid negative discount
- 15 rows flagged in discount_validity_flag as invalid above allowed range
- 18 rows flagged in discount_validity_flag as missing defaulted to 0
- 30 rows flagged in data_quality_flag as Invalid
- 42 rows flagged in data_quality_flag as Warning

---

## 7. Limitations of Cleaning Process

- Missing region and ship_mode filled with "Unknown" — actual values cannot be recovered
- Conflicting duplicate order_ids were flagged but not resolved — manual review required
- Discount validity range (0–0.25) assumed from data patterns, not from official business documentation
- Ship-before-order-date records were flagged but not corrected — root cause unknown
- missing_field_flag column was built after filling blanks so shows empty — counts documented here instead
- Some sub-categories in Office Supplies may be underrepresented if data contains additional unlisted values
