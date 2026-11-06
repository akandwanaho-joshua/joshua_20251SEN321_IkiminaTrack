# IkiminaTrack: Digital Savings Group Ledger and Micro-Loan System

*Student Name:* Akandwanaho Joshua
*Student ID:* 20251SEN321
*Course:* INSY 8311 & Database Development with PL/SQL
*Instructor:* Eric Maniraguha

## 1. Problem Statement
In Rwanda, community savings groups (Ikimina) are a vital financial tool for thousands of citizens. However, most groups still rely on paper notebooks to track member contributions, loan disbursements, and interest calculations. This manual approach is highly prone to human error, leads to lost financial records, and frequently causes disputes among members regarding balances and late penalties. 

## 2. Objectives
*Main Objective:* 
To develop a robust, automated Oracle database system using PL/SQL that manages the financial operations of a community savings group.

*Specific Objectives:*
1. To automate the tracking of member savings contributions and loan repayments.
2. To enforce business rules using PL/SQL triggers (e.g., preventing loans for members with outstanding late fees).
3. To automatically calculate interest and penalties using stored procedures and cursors.
4. To provide an interactive dashboard for the treasurer to monitor total capital and default risk.

## 3. Data Source
- *Source:* Kaggle Public Microfinance/Loan Dataset (Anonymized Lending Club data) adapted for the Rwandan Ikimina context.
- *Size:* ~2,000+ records of members, loans, and repayment histories.
- *Licence:* Open Database License (ODbL) / Educational Use.

## 4. Innovation
*Option:* Analytics Dashboard / User Interface
*Tool:* Python (Streamlit) & Oracle Database
*Description:* I will build a simple web interface using Streamlit that connects directly to the Oracle Database. The group treasurer can use it to register members, log monthly contributions, and view a real-time dashboard showing the group's total liquidity and a list of members with overdue loans. Business rules will remain strictly enforced by PL/SQL on the database side.

## 5. Planned Tables
- Members: Stores member details (ID, Name, Join_Date, Status).
- Contributions: Records monthly savings (Contribution_ID, Member_ID, Amount, Date).
- Loans: Tracks loans taken by members (Loan_ID, Member_ID, Principal_Amount, Interest_Rate, Status).
- Repayments: Records loan payments (Repayment_ID, Loan_ID, Amount_Paid, Date).
- Audit_Log: Tracks changes to sensitive data (e.g., changing a member's status).

## 6. Planned PL/SQL Features
- *Triggers:* 
  - Prevent a new loan if the member has unpaid penalties or active loans.
  - Prevent deletion of a member if they have an active loan balance.
- *Stored Procedures:* 
  - record_contribution(): Accepts payment and automatically splits it between savings and outstanding loan interest.
  - apply_monthly_penalties(): Applies a late fee to members who missed a deadline.
- *Functions:* 
  - calculate_outstanding_balance(member_id): Returns the total amount a member owes.
- *Cursors:* 
  - Loop through all active loans at month-end to calculate and add accrued interest.
- *Packages:* 
  - pkg_financials: Groups related procedures and functions for the savings and loan logic.

## 7. References
- FinScope Rwanda. (2020). Financial Inclusion in Rwanda.
- Lending Club. (2023). Loan Data. Kaggle.
- Mwangi, P., & Karanja, J. (2019). The role of digital systems in informal savings groups. Journal of African Finance.
- National Bank of Rwanda. (2022). Annual Financial Stability Report.
- Oracle Corporation. (2023). Database PL/SQL Language Reference.
