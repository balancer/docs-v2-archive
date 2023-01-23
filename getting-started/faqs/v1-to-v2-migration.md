# V1 ➝ V2 Migration

## How do I migrate from V1 to V2?

For supported two-asset pools, you can use the migration system to move your liquidity from a V1 pool to a comparable, if not identical, V2 pool.

### 1. Go to [https://pools.balancer.exchange/#/](https://pools.balancer.exchange/#/) and click "Connect Wallet" in the top right

![](../../.gitbook/assets/screen-shot-2021-05-13-at-9.30.41-am.png)

### 2. Click on "Dashboard" on the left menu

![](<../../.gitbook/assets/Screen Shot 2021-05-13 at 9.25.57 AM.png>)

### 3. Pools with Automatic Migration available will have a "V2 Migrate" button

![](../../.gitbook/assets/migration\_dashboard.png)

There are two transactions involved in migrations

* You will need to Approve the migration tool to migrate your BPT
* The migration itself

For pools that do not have Automatic Migration, you should remove liquidity from V1 and re-adding your liquidity to V2. Pools that do not have automatic migration are multi-asset pools and pools that do not have a similar pool in V2. For further reference, here is our [Medium article ](https://medium.com/balancer-protocol/balancer-liquidity-migration-tutorial-85800436d486)about migration.

## Do I have to migrate? What happens if I don't?

Balancer V1 is not being "turned off" (it can't be), so if you choose not to migrate, your liquidity will remain in the older trading pools. Trade aggregators will likely still consider V1 pools when looking for the cheapest prices, but as liquidity falls and price slippage increases, it may not be worth the gas fees for them to use those pools.

Balancer V1 pools will continue earning trade fees, but the BAL governance distributions will transition to V2.
