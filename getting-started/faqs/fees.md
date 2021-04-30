# Fees

## What type of fees are there?

* Trading fees: A small percentage of the trade paid by traders to pool LPs, set by the pool creator or dynamically optimized by Gauntlet. Additionally, the pool can introduce a Protocol Trading Fee, which is a percentage of the Trading Fee \(so, very small\)
* Flash Loan fees: A small percentage of assets that are used for flash loans from Balancer’s vault. This is the protocol fee - it accrues to the protocol, for allocation by governance

## How high are the Pool Fees?

Balancer Pools are extremely customizable. It is up to the pool creator to decide how high the fees should be, ranging from 0.0001% to 10%.

## When will the Protocol Trading Fees be turned on?

Protocol trading fees are set by governance, and will be turned on whenever they are voted to be active. The fees can be set from 0 to 50% of the existing pool swap fee.

## What happens to the fees?

All protocol fees will be kept in the vault. It is up to Balancer’s governance to decide if and how these fees are used.

## Why did you introduce Dynamic Fees?

Today, it’s nearly impossible to choose a correct swap fee at pool creation time. Inherently, the optimal trading fee for a pair continuously changes throughout both tokens’ lifecycles and the overall market cycle.

For example, a static fee can have diminishing returns after circumstances change, like liquidity moving to another pool. Another example is that during times of wild volatility, liquidity providers risk sustaining greater impermanent losses.

Just like ride-sharing apps have surge pricing during high-traffic times, thanks to a partnership with Gauntlet, Balancer pools can optimize fees for current market conditions.

