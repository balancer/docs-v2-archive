# Flash Loans

## Overview

While the consolidated liquidity in the Vault does not improve price impact on a per-pool basis, but it does enable Balancer Protocol to leverage that combined liquidity by offering Flash Loans. Flash Loans, [originally created by Aave](https://aave.com/flash-loans/), are uncollateralized loans that must be repaid (plus interest) in the same transaction as they is borrowed. If a strategy is unable to repay the loan, the entire transaction is reverted, returning all borrowed tokens to the Vault.

## Workflow

What does a sample Flash Loan transaction look like?

### 1. Take out a loan

Borrow X amount of DAI, up to the total amount of DAI available in the Vault.

### 2. Do something

Any maneuver that can be profitable within the span of a single transaction is worth performing with a flash loan. Two of the most common flash loan use cases are **arbitrage** and **collateral swap**:

**Arbitrage Trade**

* Trade DAI for TokenA on one DEX
* Trade TokenA for DAI on another DEX

**Collateral Swap**

* Pay off DAI loan for collateral
* Trade collateral for TokenA
* Take out another DAI loan with TokenA as collateral

### 3. Repay the loan

Check if `final_amount >= X * (1 + interest_rate)`

* If successful, repay `X * (1 + interest_rate)` of DAI and keep profit (if any)
* If unsuccessful, revert transaction and lose gas fee

## Flash Swaps

Further, anyone who identifies a price discrepancy in two Balancer Pools can execute a **Flash Swap**. **** An arbitrageur who makes a flash swap does not need to hold any of the input tokens that one would normally need to make a trade. Instead, the trader identifies the imbalance, tells the Vault to make the swap, and is rewarded with the profit.
