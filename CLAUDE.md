# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

MoneyManager ("Gidi") — a personal finance dashboard built as an ASP.NET Core 8.0 Web API. Track account balances, assets, and liabilities to calculate net worth, and log income/expense transactions.

## Commands

```bash
# Build
dotnet build Gidi.sln

# Run (dev, HTTP on localhost:5290, Swagger UI at /swagger)
dotnet run --project src/Gidi/Gidi.csproj

# Run with a specific launch profile
dotnet run --project src/Gidi/Gidi.csproj --launch-profile https
```

No test project exists yet.

## Architecture

The project is at an early stage — only the ASP.NET Core scaffold exists (`Program.cs` with a placeholder `/weatherforecast` endpoint). All meaningful implementation is still ahead.

**Planned domain model:**
- **Account** — `id, name, type (checking/savings/cash/brokerage/crypto/property/vehicle/…), location/institution, balance, opening balance, opening date`
- **Liability** — `id, name, type (mortgage/loan/credit card/…), balance, interest rate`
- **Transaction** — `id, date, amount, category, account_id, type (income/expense/transfer), counterparty_account_id, note/payee`
- **NetWorthSnapshot** — `date, total_assets, total_liabilities, net_worth`

**Open design decisions** (not yet resolved):
- Balance model: derived from transaction history vs. manually-maintained snapshots with transactions as a separate audit log
- Category management: flat preset list (editable) vs. user-defined from day one
- Transfers between own accounts: treated as their own transaction type (not income/expense)

**Constraints in scope:**
- Single currency per user (multi-currency deferred)
- No external API integrations in v1 (manual entry only)

## Code style

Only add comments on genuinely complex or non-obvious logic. Do not comment straightforward code.

Variable names should be written in full and be self-explanatory — good naming is the primary way to communicate intent.

## Key files

- `src/Gidi/Program.cs` — entry point and middleware pipeline
- `src/Gidi/appsettings.json` / `appsettings.Development.json` — configuration
- `src/Gidi/MoneyManager.Api.http` — REST client for manual endpoint testing
- `Gidi.sln` — solution file
