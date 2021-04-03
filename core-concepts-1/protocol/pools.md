# Pools

## Overview

![Each pool can implement its own logic while integrating into Balancer](../../.gitbook/assets/image.png)

* Pool logic abstracted from token transfers \(Vault\)
*  * Weighted Swaps
  * StableSwap
  * Other custom AMM curves

## Standard Pools

Balancer V2 will launch with two officially supported pool types.

* Standard weighted pools
* Stable pools

## Custom Pools

Arbitrary AMM pricing curves

* Anybody can deploy their own pool type and use it 

## Smart Pools

The flexibility introduced doesn't just extend to control over the pricing curve used by the pool but can affect any aspect of the pool.

Balancer V1 introduced the concept of smart pools where parameters can change over time, in V2 these features can be integrated directly into the pools themselves.

* Extensible to include anything you might want

The first smart pool will be the Liquidity Bootstrapping Pool, designed to support V2 LBPs. It is a specialized 2-token WeightedPool, which restricts liquidity provision to the pool creator, and supports pausing trading, setting the swap fee, and changing weights gradually, as in V1.

However, there are significant differences:

* You can launch the pool in a paused state \(by popular demand\)
* Rights are revocable - you can revoke any of the three available rights, making the pool more trustless \(e.g., revoke pausing and weight change to transition from an LBP to a smart treasury\)
* You can cleanly renounce ownership entirely, which allows public LPs, and effectively creates a WeightedPool \(though slightly less gas-efficient than a "native" WeightedPool\).

Likewise, there are two versions of the general Smart Pool \(for Weighted and Stable pools\).These have very similar rights to V1 smart pools - except they are individually revocable. In addition, Weighted Pools may support a "circuit breaker," to halt trading for a token if the pool becomes "unbalanced" \(e.g., if a malicious or buggy token contract allows infinite minting, or otherwise breaks the pricing algorithm of the pool\).

