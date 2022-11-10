# Composable Stable Pools

## Overview

Composable Stable Pools are designed to optimize swaps for 2 types of tokens and use [Stable Math:](../../../concepts/math/stable-math.md)

1\) **pegged tokens**- tokens that trade near 1:1, such as two stablecoins of the same currency (eg: DAI, USDC, USDT), or synthetic assets (eg: renBTC, sBTC, WBTC)

2\) **correlated tokens**- tokens that trade near 1:R with some slowly changing exchange rate R, like derivatives (eg: wstETH, wETTH)

## What does Composability Mean?

Before talking about Composable Stable Pools, let’s first look at what it takes for a pool to be composable. A pool is **composable** if there is another pool that can have the composable pool as one of its constituents.

Let’s look at one example:

_Composable Stable Pool: \[DAI, USDC, USDT];_

_Weighted Pool: \[ETH, Composable Stable Pool];_

_Instead of \[ETH, DAI], \[ETH, USDC], \[ETH, USDT];_\


Now that we saw what it takes for a pool to be **composable**, we can look at Composable Stable Pools. **Composable Stable Pools** are a **superset of all previous Stable-type pools** (Stable Pools, MetaStable Pools, StablePhantom Pools, and StablePool v2). Composable Stable Pools build on top of Phantom BPTs and allow increased composability using a process called **nesting**.&#x20;

Currently, the only flavour in the existence of Stable pools is [`ComposableStablePool`](https://github.com/balancer-labs/balancer-v2-monorepo/blob/7610a7c04071c0f6a51ecef3385419042f6131c5/pkg/pool-stable/contracts/ComposableStablePool.sol). This is a 5-token stable pool that also contains its own BPT, which enables single-token joins and exits to be performed as part of a batch swap, while still supporting multi-token joins and exits.

### Nesting

**Phantom BPT Pools** are pools that mint the BPT tokens at the time of pool creation. This helps with gas reduction because instead of using the mint/burn mechanism to join a pool, it uses a swap (or more likely a batch swap) and saves on gas. By using Phantom BPT, it is possible to nest BPTs inside other pools and swap efficiently through the nested structures.

The combination of nesting with [Balancer's Vault architecture ](../../the-vault.md)allows for a fluid route for swaps. Instead of requiring multiple pools that fractionalize liquidity, trades can flow through an interconnected pathway within pool constructs. This allows capital-efficient Composable Stable Pools, such as stETH/ETH, to slot inside additional pool types.

### Increased Composability

Nesting allows increased composability. There is **free reign for pool composition with different combinations and forms depending on specific liquidity needs.**\
\
Since we talked about pool composability, let's look at an example. Composable Stable Pools can slot inside additional pool types. Let's assume we want to create a powerful interest-bearing Ethereum pool:

1. We pair RocketPool staked ETH (or any other type of staked ETH) with Aave-boosted ETH
2. This results in the following pool structure: rETH / (wETH / aETH)
3. This pool allows for efficient trades between ETH and rETH. However, we can also add stablecoin exposure
4. We could then pair the BPT of this pool with the BPT of the bb-a-USD pool (bb-a-USDC/bb-a-DAI/bb-a-USDT)
5. This includes (USDC/aUSDC) (DAI/aDAI) (USDT/aUSDT) (all are earning external yield)
6. This forms a BPT-rETH-aETH / bb-a-USD 50/50 weighted pool
7. In addition to swap fees, liquidity providers also get rewards from the underlying yield of tokens. Additionally, this final pool allows for efficient trades between ETH, rETH, USDC, DAI, USDT\


## Advantages of Composable Stable Pools:

a) Achieve extremely **efficient swaps** by implementing the **Stable Swap Invariant** (an equation that defines the relationship between balances of pool tokens and pool parameters). The Stable Swap Invariant has significantly lower slippage for stablecoin trades than a weighted pool would have for a similar value.

b) For **rate providers**: by querying/calculating exchange rates, pools can offer swaps for correlated tokens (eg: wETH/wstETH).

c) Take advantage of [Composability](./#increased-composability) and combine different pools based on liquidity needs.



### Composable Stable Swaps Under the Balancer Umbrella

One of the key advantages to having Composable Stable Pools on Balancer specifically is that they are plugged into the same protocol as all other pools. Swapping between stablecoins is frequently used for arbitrage when one token is paired with two different stablecoins in different pools. By leveraging Batch Swaps on Balancer, these trades can be combined into a single, gas-efficient transaction.

