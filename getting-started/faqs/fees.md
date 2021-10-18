# Fees

## What type of fees are there?

* Trading fees: A small percentage of the trade paid by traders to pool LPs, set by the pool creator or dynamically optimized by Gauntlet. Additionally, Balancer governance can vote to introduce a Protocol Trading Fee, which is a percentage of the Trading Fee.\
  \
  For instance, if a pool had a 1% fee, and governance introduced a 1% protocol fee - the total swap fee to the trader would remain at 1%, but now 0.99% would accrue to the pool's LPs, and 0.01% would accrue to the protocol fee collector contract.\

* Flash Loan fees: A small percentage of assets that are used for flash loans from Balancer’s vault. This is the protocol fee - it accrues to the protocol, for allocation by governance.

All protocol fees were set to zero at launch, and can only be changed through governance.

## What are the fees for a trade?

Balancer Pools are extremely customizable, and each pool can have a different fee. It is up to the pool creator to decide how high the fees should be, ranging from 0.0001% to 10%. When using the Smart Order Router, the fees will always be taken into account when finding the best price.

Some pools have Dynamic Trade Fees that are [algorithmically set by Gauntlet](https://medium.com/gauntlet-networks/balancer-v2-pools-trading-fee-methodology-7a65df671b8c). The pool detail page on the UI shows you which type of pool it is, and how the fees are managed.

## When will the Protocol Trading Fees be turned on?

Protocol trading fees are set by governance, and will be turned on whenever they are voted to be active. The fees can be set from 0 to 50% of the existing pool swap fee.

## What happens to the protocol fees?

All protocol fees will be kept in the Protocol Fees Collector contract. It is up to Balancer’s governance to decide whether and how these fees are used.

## Why do pools have Dynamic Fees?

Today, it’s nearly impossible to choose a correct swap fee at pool creation time. Inherently, the optimal trading fee for a pair continuously changes throughout both tokens’ lifecycles and the overall market cycle.

For example, a static fee can have diminishing returns after circumstances change, like liquidity moving to another pool. Another example is that during times of wild volatility, liquidity providers risk sustaining greater impermanent losses.

Just like ride-sharing apps have surge pricing during high-traffic times, thanks to a partnership with Gauntlet, Balancer pools can optimize fees for current market conditions.
