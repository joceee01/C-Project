## How to Run
1. **Prerequisites**:
   - .NET SDK installed (check using `dotnet --version`).
   - A C# IDE like Visual Studio or Visual Studio Code. (C# extension has to be installed using Visual Studio Code)

2. **Steps**:
   - Clone this repository:
     ```bash
     git clone https://github.com/joceee01/CSharp-Project.git
     cd BankingApp
     ```
   - Build the project:
     ```bash
     dotnet build
     ```
   - Run the project:
     ```bash
     dotnet run
     ```

---

## Overview
This repository contains the solution for a practical case study of a Banking App. It is implemented as a C# console application that fulfills the following requirements:
- **Input Transactions**: Allows users to input transactions with details like date, account, type (deposit/withdrawal), and amount.
- **Define Interest Rates**: Supports defining interest rate rules with effective dates and rates.
- **Print Account Statement**: Displays account statements, calculates pro-rated interest rates.
- **Transfer Transaction**: Allows transferring amount from a payer account to a payee account.
- **Quit**: Exits the application.

---

## Features
1. **Input Transactions**:
   - Allows the user to input transactions in the format:
     ```
     <Date>|<Account>|<Type>|<Amount>
     ```
     Example:
     ```
     14102024|AC001|D|200.00
     ```
   - Automatically creates an account if it does not exist.
   - Displays transactions for the account, ordered by date.
   - Displays account information
   - **Validation**:
     - For **withdrawals (W)**, checks if the account balance is sufficient:
       - If the balance is insufficient, the transaction will fail, and the user will see a message:
         ```
         Insufficient balance for withdrawal.
         ```

2. **Define Interest Rate Rules**:
   - Allows the user to define interest rate rules in the format:
     ```
     <Date>|<RuleId>|<Rate>
     ```
     Example:
     ```
     01012024|RULE01|1.95
     ```
   - Displays the list of defined rates, ordered by their effective date.
   - **Validation**:
     - Checks if the `RuleId` is unique:
       - If not, the user is prompted:
         ```
         Rule ID is not unique. Do you want to update the existing rule? (Y/N)
         ```
         - If `Y`, the rule input will be updated to the existing Rule ID.
         - If `N`, the user is asked to reenter the Rule ID.
         - If enter a blank line, the user is able to reenter the interest rate rule.

3. **Print Account Statement**:
   - Prompts for the account and month:
     ```
     <Account>|<MMYY>
     ```
     Example:
     ```
     AC001|0924
     ```
   - Displays the account statement, calculates daily interest, and includes it as a transaction at the end of the month.

3. **Transfer Transaction**:
   - Allows the user to transfer money from 1 account to another in the format:
     ```
     <Payer Account>|<Payee Account>|<Amount>
     ```
     Example:
     ```
     AC001|AC002|100
     ```
     Explanation:
     ```
     100 from AC001 will be transfered to AC002
     ```
   - Displays both accounts' information.
   - **Validation**:
     - Transferring to the same account is not allowed and both accounts must exist
     - For **Payer Account**, checks if the account balance is sufficient for the transfer amount:
       - If the balance is insufficient, the transaction will fail, and the user will see a message:
         ```
         Transaction failed. Payer Account {payerAcc} has insufficient funds.
         ```

5. **Quit**:
   - Closes the application.

---

## Error Handling
1. **Unsuccessful Withdrawals**:
   - If a withdrawal transaction is attempted with an amount greater than the account's current balance:
     - The transaction is rejected, and the user is notified:
       ```
       Insufficient balance for withdrawal.
       ```
     - The account balance remains unchanged.

2. **Duplicate Rule IDs**:
   - When defining an interest rate rule, if the `RuleId` already exists:
     - The user is prompted:
       ```
       Rule ID is not unique. Do you want to update the existing rule? (Y/N)
       ```
       - If the user selects **Y**, the rule for the existing Rule ID is updated.
       - If the user selects **N**, the user is asked to reenter the Rule ID and new rule will be added.

3. **Input Validation**:
   - Ensures that all inputs (e.g., date, type, amount) follow the correct format.
   - Displays user-friendly error messages for invalid inputs, such as:
     ```
     Invalid input. Please follow the format: DDMMYYYY|Account|Type|Amount.
     ```

4. **Numeric Validation**:
    - Ensure that all amount and rate input are in a correct format. (e.g., positive numeric number)
   - Displays user-friendly error messages for invalid inputs, such as:
     ```
     Amount must be a positive decimal number.
     ```

5. **Unsuccessful Transfer**:
   - If a transfer transaction is attempted with an amount greater than the payer account's current balance:
     - The transaction is rejected, and the user is notified:
       ```
       Transaction failed. Payer Account {payerAcc} has insufficient funds.
       ```
     - The account balance remains unchanged.

5. **Non-existence Account**:
   - If user input a account that does not exist for transfer transaction
     - The transaction is rejected, and the user is notified:
       ```
       Payer/Payee Account does not exist.
       ```
