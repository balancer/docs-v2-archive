# Pools

## Overview

With the introduction of the Vault, Balancer Pools are now contracts that only need to handle the **logic** of swaps and liquidity provision/removal; all token transfers are handled by the Vault. This pool abstraction enables pool creators to design a pool with any arbitrary Automated Market Maker \(AMM\) equation they might want. 

## Pool Types

Balancer V2 can leverage any arbitrary pool type. Some examples are below:

### Weighted Pools

Weighted Pools are a generalization of the standard constant product AMM popularized by Uniswap. Each pool can contain up to 8 different tokens and each token is assigned a weight defining what fraction of the pool is made up by each asset. Balancer's weighted pool equation is a generalization of the x\*y=k by accounting for uneven weights and more assets:

$$
V = \prod_t B_t^{W_t}
$$

where V is constant, B is an asset's balance, and W is an asset's weight in the pool.

As the price of each token changes, traders and arbitrageurs rebalance the pool by making swaps. This maintains the desired weighting of the value held by each token whilst collecting trading fees from the traders.

### Oracle Pools

These are a subset of weighted pools that hold two tokens and provide price oracles for the tokens they hold.

### Stable Pools

For certain assets that are expected to consistently trade at near parity \(e.g. different varieties of stablecoins or synthetics\) a more efficient design is the StableSwap AMM as popularized by Curve. These pools allow for larger trades of these assets before encountering significant price impact.

### MetaStable Pools

These are a generalization of stable pools that contain tokens with known exchange rates. They use equations similar to those of stable pools, but can be used to facilitate swaps between tokens that have gradually shifting prices. 

Example use cases:

* DAI/cDAI
  * cDAI slowly accumulates lending fees and appreciates relative to DAI
* ArbitraryStableUsdToken/StaBAL3-USD
  * StaBAL3-USD Pool token collects trade fees relative to other Stable USD tokens

### Liquidity Bootstrapping Pools

These pools are useful for launching tokens and swapping large amounts over time. They feature weight shifting mechanisms that results in high start prices with continuously changing sell pressure.

There is a simulator [here](https://docs.google.com/spreadsheets/d/125MgAqv0f81Qp6y9VZHAcwMkVhvdcNKA) for how different weight change settings and project sales rates affect the price curve.

## Custom Pools

Due to Balancer's abstracted pool architecture, it's very easy to implement new price curves for new AMM designs and integrate them into the protocol. New pool types can be developed and utilized by anyone, and the Balancer Community can vote to add support for these custom pools to the UI and/or SOR.

## Smart Pools

The flexibility introduced doesn't just extend to control over the pricing curve used by the pool but can affect any aspect of the pool.

Balancer V1 introduced smart pools, which give external contracts control over parameters, and in V2 these features are integrated directly into the pools themselves. Thanks to Balancer's modular architecture, any of the smart contracts defining the behavior of a pool can be replaced as long as it maintains the common interface with the Vault.

The first smart pool to launch was the Liquidity Bootstrapping Pool \(LBP\). It is a specialized 2-4 token WeightedPool, which restricts liquidity provision to the pool creator, and supports pausing trading, setting the swap fee, and changing weights gradually.

There are significant differences in the V2 LBPs:

* Weights change automatically; no triggering \(`pokeWeights()`\) necessary
* Pools can launch in a paused state
* LBPs can range over the full 1%-99% WeightedPool math limits

Given the flexibility and composability of the native architecture, there is likely no need in V2 for a generic "Swiss army knife" like the V1 Configurable Rights Pool. New smart pools can be created by inheriting from the appropriate contract in the hierarchy, and customizing.

The most general smart pool currently under development is the Managed \(Investment\) Pool. This will support higher token counts, and contain advanced features like circuit breakers: an automatic mechanism to halt trading for a token if the pool becomes "unbalanced" \(e.g., if a malicious or buggy token contract allows infinite minting, or otherwise breaks the pricing algorithm of the pool\). It will likely also support different kinds of management fees, and the ability to add and remove tokens.

The architecture will also support the creation of "permissioned" pools, which allow external trusted parties to restrict token transfers, to support private pools or institutional use cases.

## Dynamic Swap Fees

Some pools, including the initial set of Weighted Pools deployed by Balancer Labs, have their swap fees optimized by [Gauntlet](https://gauntlet.network/). The optimal swap fee for a given pool depends on many conflicting market forces which are bound to change over time, and therefore it is not possible for a fixed swap fee to also be the optimal swap fee. This [partnership](https://medium.com/gauntlet-networks/balancer-v2-pools-trading-fee-methodology-7a65df671b8c) seeks to help optimize returns for liquidity providers while removing a degree of freedom from the pool design process, thereby further consolidating liquidity and reducing gas costs across the protocol.

