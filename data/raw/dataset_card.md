# Dataset Card

* *Source:* Kaggle - All Lending Club loan data (https://www.kaggle.com/datasets/wordsforthewise/lending-club)
* *Licence:* Open Database License (ODbL) - Public Domain for educational use.
* *Format:* CSV
* *Size:* 1,000 records (sample extracted from the full dataset for testing).
* *Date collected:* November 2026.
* *What one record represents:* One record represents a single accepted loan given to a borrower. It contains details about the loan amount, interest rate, the borrower's income, and the current loan status (e.g., Fully Paid, Charged Off/Defaulted). 

## Data Quality Issues (Counts based on 1,000 rows)
(Do not fix these yet; we will clean them in Phase IV)
*   *Missing values:* 82 rows missing emp_length (employment length).
*   *Duplicate rows:* 0 exact duplicates found in the 1,000 sample.
*   *Data type issues:* The term column contains text (" 36 months") instead of a clean number. The issue_d column is stored as text (e.g., "Dec-2015") instead of a standard Date format.
*   *Formatting issues:* The int_rate column contains a percentage sign (e.g., "13.99%") instead of a pure decimal number (13.99).

## Data Mapping (Raw Field to Target Table)
| Raw Field | Target Table | Target Column | Type Conversion Needed |
|---|---|---|---|
| id | LOANS | Loan_ID | None (INT) |
| member_id | MEMBERS | Member_ID | None (INT) |
| loan_amnt | LOANS | Loan_Amount | None (DECIMAL) |
| int_rate | LOANS | Interest_Rate | Remove '%' and convert to DECIMAL |
| term | LOANS | Loan_Term | Remove 'months' text and convert to INT |
| issue_d | LOANS | Issue_Date | Convert text "Dec-2015" to DATE |
| loan_status | LOANS | Loan_Status | None (VARCHAR) |
| annual_inc | MEMBERS | Annual_Income | None (DECIMAL) |
