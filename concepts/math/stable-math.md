# Stable Math

## Overview

Stable Math is designed to allow for swaps between any assets that have the same price, or are "pegged" to the same asset. The most common examples are stablecoins that track US Dollars (DAI, USDT, USDC), and assets that track the price of Bitcoin (WBTC, renBTC, sBTC). Prices are determined by the pool balances, the _amplification parameter_, and amounts of the tokens that are being swapped.

**In an ideal scenario**, it would make sense to simply allow 1-to-1 trades for these assets; this would be a _Constant Sum_ curve. **In a worst case scenario** where one or more of these assets loses their peg and their value diverges, it would make sense to enforce trade rules for uncorrelated assets; this would be a _Constant Product_ curve, such as the one in [Weighted Math](broken-reference).&#x20;

Since most cases are neither ideal nor disasters, the Stable Math curve combines the _Constant Sum_ and _Constant Product_ curves and is designed to facilitate approximately 1-to-1 trades that incur large price changes only when token balances differ greatly. The _amplification parameter_, $$A$$, defines the degree to which the Stable Math curve approximates the Constant Product curve (when $$A=0$$), or the Constant Sum curve (when $$A\rightarrow \infty$$).&#x20;

For more stable math formulas, [check out the Developer Docs](https://dev.balancer.fi/resources/pools/math/stable-math).

![StableSwap approaches Constant Product as A->0 and Constant Sum as A->∞](<../../.gitbook/assets/output (5).gif>)

## Invariant

Since the Stable Math equation is quite complex, determining the invariant, $$D$$, is typically done iteratively. For an example of how to do this, please refer to [this function](https://github.com/georgeroman/balancer-v2-pools/blob/main/src/pools/stable/math.ts#L16).

$$
A \cdot n^n \cdot \sum{x_i} +D = A \cdot D \cdot n^n + { \frac{D^{n+1}}{{n}^{n}\cdot \prod{x_i} } }
$$

Where:

* $$n$$ is the number of tokens
* $$x_i$$ is is balance of token $$i$$
* $$A$$ is the amplification parameter
