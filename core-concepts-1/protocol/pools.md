# Pools

## Overview

With the introduction of the Vault, Balancer Pools are now contracts that only need to handle the **logic** of swaps and liquidity provision/removal; all token transfers are handled by the Vault. This pool abstraction enables pool creators to design a pool with any arbitrary Automated Market Maker \(AMM\) equation they might want. 

![Each pool can implement its own logic while integrating into Balancer](../../.gitbook/assets/image.png)

## Standard Pools

Balancer V2 will launch with two officially supported pool types:

### Weighted Pools

Weighted Pools are a generalisation of the standard constant product AMM popularised by Uniswap. Each pool can contain up to 8 different tokens and each token is assigned a weight defining what fraction of the pool is made up by each asset. 

As the prices of each constituent token changes, the pool will automatically rebalance the pool's balances to maintain the desired weighting of the value held of each token whilst collecting trading fees from the traders performing this rebalancing.

### Stable Pools

For certain assets which are expected to consistently trade at near parity \(e.g. different varieties of stablecoins or synthetics\) a more efficient design is the StableSwap AMM as used by Curve. These pools allow for larger trades of these assets before encountering significant price impact.

## Custom Pools

Due to Balancer's abstracted pool architecture, it's very easy to implement new price curves for new AMM designs and integrate them into the protocol. New pool types will be added by the Balancer Labs team as well as the broader Balancer Community due to the permission-less nature of the Balancer protocol.

## Smart Pools

The flexibility introduced doesn't just extend to control over the pricing curve used by the pool but can affect any aspect of the pool.

Balancer V1 introduced the concept of smart pools where parameters can change over time, in V2 these features can be integrated directly into the pools themselves. Due to Balancer's modular architecture, any of the smart contracts defining the behaviour of a pool can be replaced as long as it maintains the common interface with the Vault.

The first smart pool will be the Liquidity Bootstrapping Pool, designed to support V2 LBPs. It is a specialized 2-token WeightedPool, which restricts liquidity provision to the pool creator, and supports pausing trading, setting the swap fee, and changing weights gradually, as in V1.

However, there are significant differences:

* You can launch the pool in a paused state \(by popular demand\)
* Rights are revocable - you can revoke any of the three available rights, making the pool more trustless \(e.g. revoke pausing and weight change to transition from an LBP to a smart treasury\)
* You can cleanly renounce ownership entirely, which allows public LPs, and effectively creates a WeightedPool \(though slightly less gas-efficient than a "native" WeightedPool\).

Likewise, there are two versions of the general Smart Pool \(for Weighted and Stable pools\).These have very similar rights to V1 smart pools - except they are individually revocable. In addition, Weighted Pools may support a "circuit breaker", to halt trading for a token if the pool becomes "unbalanced" \(e.g., if a malicious or buggy token contract allows infinite minting, or otherwise breaks the pricing algorithm of the pool\).

