---
cover: ../../.gitbook/assets/bannerPools (1).png
coverY: 0
---

# Balancer Pools

## Overview

Pools are the fundamental building blocks of the Balancer Protocol; they are smart contracts that define how traders can swap between tokens on Balancer. What makes Balancer Pools unique from those of other protocols is their limitless flexibility. While other exchanges have pools with constrained parameters, Balancer can accommodate pools of any composition and underlying math. Balancer's architecture allows for anyone to develop their own pool type, opening the door for customized pricing functions in trading pools.

## Oracle Functionality

Some pools (WeightedPool2Tokens and MetaStable Pools) have optional Oracle functionality. This means that they can be used as sources of on-chain price data.&#x20;

## Pools At A Glance

### [Weighted Pools](weighted-pools.md)

Designed for general cases, including tokens that don't necessarily have price correlation (ex. DAI/WETH).

### [Stable Pools](broken-reference)

Ideal for soft-pegged tokens with strong correlation (ex. DAI/USDC/USDT).

### [MetaStable Pools](metastable-pools.md)

Built for non-pegged tokens that maintain correlation but may slowly diverge over time, such as derivatives (ex. stETH/WETH).

### [Liquidity Bootstrapping Pools](liquidity-bootstrapping-pools-lbps.md)

Ideal for shifting liquidity of one token into another (ex. AKITA/ETH).

### [Managed Pools](managed-pools.md)

Designed to have extreme flexibility to manage a dynamic fund. Features weight shifting to rebalance, swap pausing, and management fees. (ex. WSBDapp).

## Comparison

| Pool                        |     Math | Max # Tokens | Uses Oracle | Can _Be_ Oracle | Time-dependent pricing |
| --------------------------- | -------: | -----------: | ----------: | --------------: | ---------------------: |
| **Weighted**                | Weighted |            8 |          No |             Yes |                     No |
| **Stable**                  |   Stable |            5 |          No |              No |                     No |
| **MetaStable**              |   Stable |            2 |         Yes |             Yes |                     No |
| **Liquidity Bootstrapping** | Weighted |            4 |          No |              No |                    Yes |
| **Managed**                 | Weighted |           50 |          No |              No |                    Yes |
