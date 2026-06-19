# simranpreetkaur_2511852_part1_data_cleaning
# Business Data Cleaning, Validation & Excel Reporting

## Student: Simranpreet Kaur | ID: 2511852

---

## 1. Problem Summary

A retail company exported order-level sales data from multiple internal systems.
The raw dataset contained issues including inconsistent text formatting, date format
problems, duplicate records, missing values, invalid discounts, calculation
mismatches, and order status inconsistencies. The goal was to clean, validate,
and produce summary reports for business review.

---

## 2. Dataset Description

| Property | Value |
|---|---|
| File | raw_orders.xlsx |
| Total Raw Rows | 932 |
| Total Columns | 21 |
| Total Cleaned Rows | 912 |
| Date Range | January 2024 – October 2025 |
| Key Fields | order_id, order_date, ship_date, customer_name, segment, region, category, sub_category, discount, sales, profit |

---

## 3. Tools Used

- Google Sheets (data cleaning, validation, calculated columns, pivot summaries)
- GitHub (version control and submission)
- Markdown (cleaning log and README documentation)

---

## 4. Cleaning Steps Performed

1. Preserved raw data unchanged in data/raw_orders.xlsx
2. Created separate cleaned file: data/cleaned_orders.xlsx
3. Cleaned text fields using TRIM and PROPER functions on 10 columns
4. Standardized 4 different date formats into consistent date values
5. Removed 20 exact duplicate rows
6. Flagged 24 conflicting duplicate order_id rows for review
7. Filled 26 missing region values with "Unknown"
8. Filled 22 missing ship_mode values with "Unknown"
9. Validated and cleaned discount column
10. Created 8 calculated columns including calculated_sales, calculated_profit, profit_margin, shipping_delay_days, data_quality_flag

---

## 5. Business Rules Applied

| Rule | Action |
|---|---|
| Missing region | Filled as Unknown, flagged |
| Missing ship_mode | Filled as Unknown, flagged |
| Missing discount | Defaulted to 0 if other fields valid |
| Negative discount | Flagged invalid, set to 0 |
| Discount above 0.25 | Flagged invalid, set to 0 |
| Cancelled orders | Excluded from completed sales summary |
| Failed payments | Excluded from completed sales summary |
| Refunded orders | Separately summarized |
| Ship date before order date | Flagged as invalid shipping record |

---

## 6. Summary of Data Quality Issues Found

| Issue | Count |
|---|---|
| Exact duplicate rows | 20 |
| Conflicting duplicate order_ids | 12 (24 rows) |
| Missing region | 26 |
| Missing ship_mode | 22 |
| Missing discount | 18 |
| Invalid negative discount | 15 |
| Discount above allowed range | 15 |
| Ship date before order date | 22 |
| Clean records | 840 |
| Warning records | 42 |
| Invalid records | 30 |

---

## 7. Summary of Final Pivot Reports

| Pivot | Description |
|---|---|
| Sales by Region | Total sales and profit per region, sorted descending |
| Sales by Category | Total sales and profit per category and sub-category, sorted descending |
| Orders by Ship Mode | Order count per shipping method |
| Profit Margin by Segment | Average profit margin per customer segment |
| Refunded/Cancelled/Failed by Region | Count of problematic orders per region |
| Monthly Sales Trend | Total sales per month across 2024-2025 |

---

## 8. Key Business Insights

- South region had highest total sales (2,330,643) followed closely by East (2,207,667)
- East region had highest total profit (687,222) despite being second in sales
- Chairs was the top-selling sub-category (985,020) within Furniture
- Copiers led Technology sub-categories with 897,783 in sales
- Consumer segment had the highest average profit margin (0.31)
- 22 orders had ship dates before order dates — potential system data entry issue
- 163 returned orders represent a significant refund risk area
- Standard Class was the most used shipping method (242 orders)

---

## 9. Assumptions and Limitations

- Slash-format dates treated as MM/DD/YYYY (US format) based on data evidence
- Dash-format dates treated as DD-MM-YYYY based on data evidence
- Valid discount range assumed as 0 to 0.25 based on majority of data values
- Text discounts "70%" and "85%" converted to decimal then flagged as above range
- Conflicting duplicate records kept and flagged — not deleted
- Missing region/ship_mode filled with "Unknown" — original values unrecoverable
- missing_field_flag column was built after filling blanks so shows empty — counts documented in cleaning log

---

## 10. Screenshots

| File | Description |
|---|---|
| screenshots/raw_data_preview.png | Raw dataset before cleaning |
| screenshots/cleaned_data_preview.png | Cleaned dataset with calculated columns |
| screenshots/pivot_summary_1.png | Sales and profit by region |
| screenshots/pivot_summary_2.png | Sales and profit by category |

---
