# Flash Loans

## Overview

As discussed in the Vault section, the consolidated liquidity in the Vault does not improve price impact on a per-pool basis, but it does enable Balancer Protocol to leverage that combined liquidity by offering Flash Loans. A Flash Loan is an uncollateralized loan that must be repaid \(plus interest\) in the same transaction as it is borrowed. If a strategy is unable to repay the loan, the entire transaction is reverted, returning all borrowed tokens to the Vault.

## Workflow

What does a sample Flash Loan transaction look like? A simplified workflow might look like:

* Phase 1: Borrow X amount of DAI
* Phase 2: Do something with DAI
  * Examples
    * Arbitrage Trade
      * Trade DAI for TokenA on one DEX
      * Trade TokenA for DAI on another DEX
    * Collateral Swap
      * Pay off DAI loan for collateral
      * Trade collateral for TokenA
      * Take out another DAI loan with TokenA as collateral
* Phase 3: Repay the loan
  * Check if `final_amount >= X * (1 + interest_rate)`
    * If successful, repay `X * (1 + interest_rate)` of DAI and keep profit \(if any\)
    * If unsuccessful, revert transaction and lose gas fee

## Flash Swaps

Further, anyone who identifies a price discrepancy in two Balancer Pools can execute a **Flash Swap**. ****An arbitrageur who makes a flash swap does not need to hold any of the input tokens that one would normally need to make a trade. Instead, the trader identifies the imbalance, tells the Vault to make the swap, and is rewarded with the profit.

