# Liquidity

## How do I invest/provide liquidity?

First time here? Check out [this tutorial](../walkthroughs/invest.md) for a walk-through on how to add/withdraw liquidity.&#x20;

In short, you'll need:

* ETH to pay for gas fees
* ERC20 tokens
* An Ethereum address you can use with one of the following compatible wallets
  * MetaMask
  * Coinbase Wallet
  * A WalletConnect compatible wallet
  * Portis
  * Fortmatic

## What are the benefits of providing liquidity?

Balancer Liquidity Providers (LPs) collect trading fees on each swap. In addition, some pools in V2 are eligible for Governance Distributions through the Liquidity Mining program.&#x20;

To read more about fees, click [here](fees.md).

## How are trade fees collected?

When there is a trade in a pool, the pool collects a trade fee. The trade fee is denominated in the **input** token.

{% hint style="info" %}
**Example**: Let's say there is a pool holding BAL and DAI with a 3% trade fee. If Alice trades 100 DAI for BAL, the pool will keep 3 DAI (3% of 100 DAI) and give her back an amount of BAL worth 97 DAI.
{% endhint %}

## How do I get _my_ trade fees?

As the pool collects fees, your **Balancer Pool Tokens automatically collect fees** because they represent your **proportional share of the pool.**&#x20;

Let's say Alice, Bob, Chuck, and Diana all provide liquidity in the same pool starting out worth $100. After some time, it has earned many trade fees and is now worth $200. The pool itself grows while their proportional shares stay the same.&#x20;

| Person | Proportional Share  | Initial Value | Value After Trading |
| ------ | ------------------- | ------------- | ------------------- |
| Alice  | 50.0%               | $50           | $100                |
| Bob    | 25.0%               | $25           | $50                 |
| Chuck  | 12.5%               | $12.50        | $25                 |
| Diana  | 12.5%               | $12.50        | $25                 |

![](../../.gitbook/assets/screen-shot-2021-08-12-at-10.10.06-am.png)

## How does a pool determine the price of tokens?

In general the AMM logic determines the prices that traders pay. For example, Weighted Pools, use a constant product formula and Stable Pools, use a StableSwap formula.

## How does the self-balancing index fund work?

Balancer allows anyone to create a self-balancing index fund. Instead of paying a portfolio manager to continuously rebalance the fund, as investors do with an ETF, liquidity providers collect fees as traders rebalance the trading pools. This works because market actors are incentivized to rebalance the portfolio to take advantage of arbitrage opportunities.&#x20;
