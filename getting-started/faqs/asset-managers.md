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

Balancer partnered with Aave to create the first Asset Manager \(coming soon!\).

## Where can I read more about Asset Managers?

Read more about Asset Managers on the Medium post [here](https://medium.com/balancer-protocol/balancer-partners-with-aave-to-build-the-first-v2-asset-manager-d9c173330151)!

