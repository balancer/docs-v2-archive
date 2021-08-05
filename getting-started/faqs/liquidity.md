# Liquidity

## How do I invest/provide liquidity?

First time here? Check out [this tutorial](../walkthroughs/invest.md) for a walkthrough on how to add/withdraw liquidity. 

In short, you'll need:

* ETH to pay for gas fees
* ERC20 tokens
* An Ethereum address you can use with one of the following compatible wallets
  * MetaMask
  * Coinbase Wallet
  * A WalletConnect compatible wallet
  * Portis
  * Fortmatic

## How do Liquidity Providers earn yield?

Balancer LPs can earn yield in a few ways:

* Trading Fees
* Returns from Asset Managers

In addition, some pools in V2 are eligible for Governance Distributions through the Liquidity Mining program. 

To read more about fees, click [here](fees.md).

## How does a pool determine the price of tokens?

In general the AMM logic determines the prices that traders pay. For example, Weighted Pools, use a constant product formula and Stable Pools, use a StableSwap formula.

## How does the self-balancing index fund work?

Balancer allows anyone to create a self-balancing index fund. Instead of paying a portfolio manager to continuously rebalance the fund, as investors do with an ETF, liquidity providers collect fees as traders rebalance the trading pools. This works because market actors are incentivized to rebalance the portfolio to take advantage of arbitrage opportunities. 

