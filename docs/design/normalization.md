# Normalization Process

## 1. Unnormalized Form (UNF)
The raw data from Kaggle is a single, wide CSV file containing loan details, borrower details, and payment history all in one row. 
Data redundancy: If a borrower takes multiple loans, their personal details (income, employment length) would be repeated for every loan.

| id | member_id | loan_amnt | int_rate | annual_inc | loan_status |
|---|---|---|---|---|---|
| 68407277 | 3600 | 3600 | 13.99% | 55000 | Fully Paid |
| 68355089 | 24700 | 24700 | 11.99% | 65000 | Fully Paid |
| 68468343 | 11950 | 11950 | 13.44% | 34000 | Fully Paid |

## 2. First Normal Form (1NF)
*Rule:* Eliminate repeating groups; ensure every column contains atomic (single) values.
*Action:* We ensure every cell has only one value. We assign a Primary Key to every row (id becomes Loan_ID).

| Loan_ID | Member_ID | Loan_Amount | Interest_Rate | Annual_Income | Loan_Status |
|---|---|---|---|---|---|
| 68407277 | 3600 | 3600 | 13.99 | 55000 | Fully Paid |
| 68355089 | 24700 | 24700 | 11.99 | 65000 | Fully Paid |
| 68468343 | 11950 | 11950 | 13.44 | 34000 | Fully Paid |

## 3. Second Normal Form (2NF)
*Rule:* Remove partial dependencies (all non-key columns must depend on the entire primary key). 
*Action:* We separate the Borrower (Member) data from the Loan data. 
*Split 1: Create the MEMBERS entity*
Dependency removed: Borrower details (Annual_Income) depend on the Member, not the specific loan. We extract these into a MEMBERS table.

*MEMBERS Table:*
| Member_ID | Annual_Income |
|---|---|
| 3600 | 55000 |
| 24700 | 65000 |
| 11950 | 34000 |

*LOANS Table (Partial):*
| Loan_ID | Member_ID | Loan_Amount | Interest_Rate | Loan_Status |
|---|---|---|---|---|
| 68407277 | 3600 | 3600 | 13.99 | Fully Paid |
| 68355089 | 24700 | 24700 | 11.99 | Fully Paid |
| 68468343 | 11950 | 11950 | 13.44 | Fully Paid |

## 4. Third Normal Form (3NF)
*Rule:* Remove transitive dependencies (non-key columns must not depend on other non-key columns).
*Action:* We create separate tables for Groups, Contributions, and Repayments to match our Ikimina business logic.

*Split 2: Create the GROUPS entity*
Dependency removed: The dataset does not have a "Group", but our Ikimina system requires one. We create a GROUPS table. (Note: We will simulate Group data in Phase IV).

*Split 3: Create the CONTRIBUTIONS entity*
Dependency removed: Savings happen independently of loans. We create a CONTRIBUTIONS table to track deposits.

*Split 4: Create the REPAYMENTS entity*
Dependency removed: Repayments are transactions linked to a specific loan. We create a REPAYMENTS table to track each installment.

### Resulting 3NF Schema (Final):
1. *GROUPS* (Group_ID, Group_Name, Location)
2. *MEMBERS* (Member_ID, Group_ID, First_Name, Last_Name, Annual_Income)
3. *CONTRIBUTIONS* (Contribution_ID, Member_ID, Amount_Saved, Contribution_Date)
4. *LOANS* (Loan_ID, Member_ID, Loan_Amount, Interest_Rate, Loan_Status)
5. *REPAYMENTS* (Repayment_ID, Loan_ID, Amount_Paid, Payment_Date)
