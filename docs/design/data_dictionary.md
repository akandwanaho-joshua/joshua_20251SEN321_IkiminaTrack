# Data Dictionary

## Table: MEMBERS
| Column | Meaning | Required | Unique |
|---|---|---|---|
| Member_ID | Unique ID for the borrower | Yes | Yes |
| Group_ID | Links member to their Ikimina group | Yes | No |
| First_Name | Borrower's first name | Yes | No |
| Last_Name | Borrower's last name | Yes | No |
| Annual_Income | Borrower's yearly income (converted to RWF) | Yes | No |

## Table: LOANS
| Column | Meaning | Required | Unique |
|---|---|---|---|
| Loan_ID | Unique ID for the loan | Yes | Yes |
| Member_ID | Links loan to the member | Yes | No |
| Loan_Amount | Principal amount borrowed | Yes | No |
| Interest_Rate | The rate applied to this loan | Yes | No |
| Loan_Status | Current status (Fully Paid, Defaulted) | Yes | No |

## Table: CONTRIBUTIONS
| Column | Meaning | Required | Unique |
|---|---|---|---|
| Contribution_ID | Unique ID for the savings transaction | Yes | Yes |
| Member_ID | Links the savings to a specific member | Yes | No |
| Amount_Saved | The amount of money deposited | Yes | No |
| Contribution_Date | The date the deposit was made | Yes | No |

## Table: REPAYMENTS
| Column | Meaning | Required | Unique |
|---|---|---|---|
| Repayment_ID | Unique ID for the repayment | Yes | Yes |
| Loan_ID | Links the payment to a specific loan | Yes | No |
| Amount_Paid | The amount paid back | Yes | No |
| Payment_Date | The date the payment was made | Yes | No |

## Table: GROUPS
| Column | Meaning | Required | Unique |
|---|---|---|---|
| Group_ID | Unique ID for the Ikimina group | Yes | Yes |
| Group_Name | Name of the savings group | Yes | Yes |
| Location | District or sector where the group operates | Yes | No |
