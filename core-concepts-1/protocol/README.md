# Protocol

## Overview

### Architecture

At the protocol level, Balancer V2 makes some important changes to improve upon the concept laid out by V1. While each pool in V1 held its own tokens and made swaps, V2 takes an entirely different approach.

Balancer V2's Vault architecture abstracts all trading logic to **Pools**, and lets the **Vault** handle all intermediate swaps involved in a multi-hop trade. Among other advantages and features, the Vault reduces swap fees by transferring the minimal necessary amount.

{% page-ref page="pools.md" %}

{% page-ref page="vault.md" %}

### New Features

#### Asset Managers

Asset Managers improve the capital efficiency of trading pools by reinvesting idle assets. Typical trading pools with deep liquidity benefit only from low slippage, but tokens not involved in trades do not contribute to the fees accrued by the pool. Asset Managers tap into that otherwise idle capital, putting it to work on external protocols. For example, the Aave Asset Manager can take these assets and lend them out to borrowers, earning interest for the Balancer Pool.

{% page-ref page="asset-managers.md" %}

#### Flash Loans

Flash Loans are uncollateralized loans that must be repaid \(with interest\) in the same transaction that they are borrowed. Consolidating multiple pools' tokens in the Vault, otherwise fragmented liquidity can be lent in a flash.

{% page-ref page="flash-loans.md" %}

### Fees

Trading fees and flash loan fees collected from traders and borrowers are separated into two categories: Liquidity Provider Fees and Protocol Fees. Protocol Fees are turned off by default but can be turned on by governance vote. 

{% page-ref page="../governance/governable-protocol-fees.md" %}

