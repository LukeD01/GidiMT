# MoneyManager

A personal finance dashboard: track account balances, assets, and liabilities to calculate net worth, plus log income/expense transactions.

## Project scope (as discussed)

### Goals
- Track balances for bank accounts, cash, and other assets (with name + location)
- Track liabilities separately
- Calculate overall net worth (assets - liabilities)
- Track net worth over time (history/snapshots)
- Manually log income/expense transactions, categorized, linked to an account
- Future: API integrations to auto-import transactions
- Future: ROI on investments (requires tracking contributions/cost basis separately from growth)
- Future: allocation views (% net worth in cash vs investments vs real estate vs debt)

### Assumptions / decisions
- Single currency per user (multi-currency deferred)
- Open questions still to resolve:
  - Account balances: derived from transaction history (balance = opening balance + sum of transactions) vs. manually maintained snapshots with transactions as a separate log
  - Categories: flat preset list (editable) vs. custom from day one
  - Transfers between own accounts modeled as their own transaction type (don't count as income/expense)

### Data model (draft)
- **Account**: id, name, type (checking/savings/cash/brokerage/crypto/property/vehicle/etc.), location/institution, balance, opening balance, opening date
- **Liability**: id, name, type (mortgage/loan/credit card/etc.), balance, interest rate (optional, for future use)
- **Transaction**: id, date, amount, category, account id, type (income/expense/transfer), counterparty account id (for transfers), note/payee
- **NetWorthSnapshot**: date, total assets, total liabilities, net worth

## Project structure
- `src/MoneyManager.Api` - ASP.NET Core Web API
