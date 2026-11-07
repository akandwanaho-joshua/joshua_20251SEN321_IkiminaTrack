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



   ## Phase I – Business Process Modeling

*Selected Process:* Micro-Loan Request and Disbursement
*Description:* This process handles the lifecycle of a member requesting a loan, automated eligibility checking by the system, manual approval for high-value loans, and fund disbursement.

*Modeling Tool Used:* draw.io (diagrams.net)
*Published Diagram Link:* [ https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=business_process_diagram.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22Page-1%22%20id%3D%22C8ZU_5-23c7CqQxPTOO2%22%3E7VzZdqM4EP2aPHYOi9keY8e9nElmcpLMdOdRBgXUAcQI4aW%2FfiQQZnVCaDCeJH1y2qgQQq5766pUkJypi2D7hYDIu8YO9M8UydmeqZdnimJZGvufG3aZQbOkzOAS5GQmuTDcoV9QGPNuCXJgXOlIMfYpiqpGG4chtGnFBgjBm2q3R%2BxX7xoBFzYMdzbwm9bvyKFeZjU1qbB%2Fhcj18jvLkjgTgLyzMMQecPCmZFKXZ%2BqCYEyzo2C7gD73Xe6X7LrPB87uJ0ZgSDtdABe3659%2FbO7nDxL%2BGnzfbBPzkzxrDiNGjukud0K8QYEPQtaaezTwmVFmh7aHfOcK7HDCL4wpsJ%2Fy1pzAmEF5k48q10zXgPND4uNhgn7hkAJfGNg4hAoeKNUed%2FwWotvGQxTeRcDm%2FTaMesyWzXsN%2FETM%2B4YxRRghoXBb%2Bn7CR18gDiAlO9bFK8GoKYK2mwJzSxdA5sMYoi2YvacsEJRz92MXqLADAcxrQNJaQHoOzRehe8bJwr8NX17DYAVJL2%2FKeos3Z1VvKmM5T5G6Ok9rOC%2FCKKTphLQ5%2B5HO5RnrtNh%2Fnmms1yI9k7WrNlNr7y2n1voIeW%2FxWRtbrtnymTR6V8dmPwxtD0T8GwVbl2v0%2BSoKwnO4Tt1RZgWHFTHpuwIr6N%2FgGFGEQ3ZuhSnFAevg8xNzFoQuwUnoLLCPSeop9TH9Vxrjwkcuv5ZiHplAtGx2T0YidR5Bghi%2B%2FPiSgcjUHN4UpjkTER%2BFcLEXdU5JEEdZ4xFtoVP0ysQndADhxngXrDD%2FRi4MIeF8zqZdGj79sg2CpzHRi9%2Bm1KC3WWX3rCoV6mhkb1kVPsj%2BxsgOwwrP2SABCgGFSmeqL9kIfYhuNIluVIluyjWma2MxXRmQ6UobodtsRtOY8Vt5mfSZzajz3WgjfJtNaTG2DtkWcLVJHo4UCuIn5UB%2BRRgj74Qb05hIiRlnaYQs1bJDnk0wwuYkhNsIcOKm7Lax74MoRqt0LG7h970G5CntD1YxJYDTv8ndW%2FhvAmMm1NI1sgn%2B5GMQDqXacj0pUY%2Bk2zORuEGnsRvpSm%2BcEBs%2BFzBSIw743XI8MaEednEI%2FGVhne9RTjEq%2BlxhrnQprj8hpTuRSoKE4ioL2OTJ7oe4Pm088Aajp2hebssnL3flVlnHuNGBjyDx6VW7MGc7OUEYtpa78Dm%2FZfrRZAiBPqBoXUVh%2BIxeP4GM%2Fp5AECekb1KvNOPnUFK%2Fq%2B0Dhl8N1K7%2B1D9Wg7e0GizTFIuHrVgVdBDwyYWrOKsI6D6%2FzkFrdujyQxRy%2BHcxhUF%2BllGu1GGwxUStBsO%2BMrSrBsfwwdBW0%2FkIhrcfDF%2F5KIqE12lIPLJZxIORWa6S2bCORGbZOoGV0vYAImwXF%2BN%2BqWaPtVIxx1orTbN3rml1zDXVJhYnnGsOmVZm%2B92p0kq1s%2FJbDYAK98sHNK7katH5xULDLVwjuGE2nzuOf%2FbdrenNCKqVHtRjbdbymkYvL3s4WCXxyx5OV6BvYYwceMi5F1FEmNazqX4eTOZrojTTjiXzxgnIfJ4VHkfhZ9JYCm8YvRXe6Kjw%2BfOx96fwij6lwiudtcdoAPSR2%2F%2BPc%2Fvb5f3tt%2BU%2FjCkXLZta24P2E494H7lohXxEd%2BNubq3a2qsdZ5kw%2BueunZWtuSl%2BL8pmTqlslvVWod0i%2BqMAk7UeSmcKXHmjUv7OLlK0MiPkI%2FIh92tJhf78a9LFr3PVvLn4DZl4ZyrLRx4s8a7pqXys8ko%2BlTGjzny3gmpNKqhH2AVMA20PQX0FrEPKnbj0hmfepWxJ1841WdZ5FVW3DN3UK8EuK7WNYUY0MUiNFftZ%2FYasmqchqxcBw6R4hCPy1Uauq0nSU6q8Y%2Ba3L9SWxtNjbfygbVal3okeq1I7F46UvXR%2BktESZmMUZxe3y4v7AxtKFqmQvw0pCrajPieVajXH%2BnvVo8WaPnqs5bLxDmNNnTLWcr%2BfTKz9fXN5MNaSyAGUPxxZAR%2BENowHjLeWNzbr8abXXk6uZx%2FDgdL5JZ0TEMDvBKWYXCQO4jp4hd2RZXCqJ%2BxafxnMn8W8mHIok8qg%2FDoZHP%2Fdw0m1Ueu%2FL%2ByMtzrtslcrmkmTAz7pWwFm%2F8pqZ8AnrvGczyy9GuSmNjtmtjNrLC4PMJ4SdKt%2FYa8r6Ookz4CHL9CdFGzq%2BLBNLc6veqAxvjbPJsW7%2Fy9%2BdNbmiV%2FGOzW8D6Tnv4s3axa%2Fy5%2BVZos%2FiKAu%2FwM%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E]

*Supporting Documents:*
* [Business Process Diagram (PDF)](docs/business_process/business_process_diagram.pdf)
* [Business Process Explanation (PDF)](docs/business_process/business_process_explanation.pdf)
