# Asset Managers

## What are Asset Managers?

Asset Managers are external smart contracts nominated by pools that have full power over the underlying tokens the pool has deposited in the vault.

## How can I be sure Asset Manager will not abuse its power?

Short answer: you can't, entirely. They are very powerful, and will need careful auditing and review. Pools with asset managers are therefore less trustless than core pools.

## What can Asset Managers do?

The Asset Manager can follow any arbitrary investment strategy. For example, it could lend tokens to a lending protocol to improve the pool’s yield.

![](../../.gitbook/assets/image%20%286%29.png)

## Why might an Asset Manager not be able to lend some tokens?

A buffer must always be kept in the vault, or else trades could fail; the vault cannot trade out assets it does not currently hold on behalf of a pool

## What Asset Managers are available today?

Balancer partnered with Aave to create the first Asset Manager; the unreleased prototype and infrastructure are available in GitHub.

We are currently developing new pool types that achieve the capital efficiency goals of asset managers in a more automated fashion \(asset managers require active management to ensure solvency\) - and with even better concentration of liquidity. The first capital efficient Aave pools will be launched using this new framework.

The original asset manager architecture can be used for many additional use cases - any time tokens need to be removed from the Vault temporarily: e.g., for voting or staking.

## Where can I read more about Asset Managers?

Read more about Asset Managers on the Medium post [here](https://medium.com/balancer-protocol/balancer-partners-with-aave-to-build-the-first-v2-asset-manager-d9c173330151)!

