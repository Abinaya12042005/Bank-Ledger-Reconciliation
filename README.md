# Bank vs Ledger Reconciliation

An end-to-end reconciliation project using Python, Excel and Power BI. It matches a bank statement against a ledger, classifies every mismatch, and reports the results in a dashboard.

Note: all data is synthetic, generated to mimic a real reconciliation workflow.

## Problem
Bank statements and ledgers rarely agree. Finance and MIS teams have to find which entries are missing, duplicated, mistimed or wrong. This project automates that.

## Approach
1. Data generation: synthetic bank statement (5,060 rows) and ledger (5,000 rows) with injected errors (timing differences, amount mismatches, duplicates, missing entries, bank charges)
2. Cleaning: standardised dates, text fields and amounts (paise-level integers to avoid float errors)
3. Matching in three passes:
   - Exact: customer, type, date and amount all equal
   - Timing difference: same amount, date within +/- 4 days
   - Amount mismatch: same date, amount difference up to Rs 500
4. Leftovers classified as Only in Bank, Only in Ledger or Duplicate in Ledger
5. Reconciliation statement: bank balance + adjustments = ledger balance
6. Excel report: Summary, Recon_Statement, Exceptions, Aging, Monthly_Trend, Full_Result
7. Validation against the injected-error answer key
8. Power BI dashboard (2 pages)

## Results
- Exact match: 90.91%
- Reconciled (including timing and amount differences): 95.85%
- Total exceptions: 610
- Unexplained difference in the reconciliation statement: 0.00
- Validation: 99.12% row-level, 100% group-level (identical duplicate rows cannot be told apart at row level; financial impact is zero)

## Dashboard
Page 1: Reconciliation Summary
![Page 1](screenshots/page1_reconciliation_summary.png)

Page 2: Exception Details
![Page 2](screenshots/page2_exception_details.png)

## Tech stack
Python (pandas, numpy), Excel (xlsxwriter), Power BI (DAX), Google Colab

## How to run
1. Open the notebook in Google Colab
2. Run the cells in order
3. Open the .pbix file in Power BI Desktop (load the CSVs from the output folder if prompted)

## Limitations
- Synthetic data, so results are cleaner than real-world data
- Tolerance rules (4 days, Rs 500) would need tuning on real data
- Aging is calculated against a fixed report date (31-Dec-2024)

## Author
Abinayaa J
LinkedIn: linkedin.com/in/abinaya-j-69549227b
