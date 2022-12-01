# Fees

## What type of fees are there?

* Trading fees: A small percentage of the trade paid by traders to pool LPs, set by the pool creator or dynamically optimized by Gauntlet. Additionally, Balancer governance can vote to introduce a Protocol Trading Fee, which is a percentage of the Trading Fee.\
  \
  For instance, if a pool had a 1% fee, and governance introduced a 1% protocol fee - the total swap fee to the trader would remain at 1%, but now 0.99% would accrue to the pool's LPs, and 0.01% would accrue to the protocol fee collector contract.\

* Flash Loan fees: A small percentage of assets that are used for flash loans from Balancer’s vault. This is the protocol fee - it accrues to the protocol, for allocation by governance.

All protocol fees were set to zero at launch, and in Dec 2021, were set to 10% [by a governance vote](https://vote.balancer.fi/#/proposal/0xf6238d70f45f4dacfc39dd6c2d15d2505339b487bbfe014457eba1d7e4d603e3).

## What are the fees for a trade?

Balancer Pools are extremely customizable, and each pool can have a different fee. It is up to the pool creator to decide how high the fees should be, ranging from 0.0001% to 10%. When using the Smart Order Router, the fees will always be taken into account when finding the best price.

Some pools have Dynamic Trade Fees that are [algorithmically set by Gauntlet](https://medium.com/gauntlet-networks/balancer-v2-pools-trading-fee-methodology-7a65df671b8c). The pool detail page on the UI shows you which type of pool it is, and how the fees are managed.



## What happens to the protocol fees?

All protocol fees are kept in the ProtocolFeesCollector contract. It is up to Balancer’s governance to decide whether and how these fees are used.

The Protocol Fees Collector contracts are deployed at the following:

| Network          | Contract Address                                                                                                         |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Ethereum Mainnet | [0xce88686553686DA562CE7Cea497CE749DA109f9F](https://etherscan.io/address/0xce88686553686da562ce7cea497ce749da109f9f)    |
| Polygon          | [0xce88686553686da562ce7cea497ce749da109f9f](https://polygonscan.com/address/0xce88686553686da562ce7cea497ce749da109f9f) |
| Arbitrum         | [0xce88686553686da562ce7cea497ce749da109f9f](https://arbiscan.io/address/0xce88686553686da562ce7cea497ce749da109f9f)     |

## Why do pools have Dynamic Fees?

Today, it’s nearly impossible to choose a correct swap fee at pool creation time. Inherently, the optimal trading fee for a pair continuously changes throughout both tokens’ lifecycles and the overall market cycle.

For example, a static fee can have diminishing returns after circumstances change, like liquidity moving to another pool. Another example is that during times of wild volatility, liquidity providers risk sustaining greater impermanent losses.

Just like ride-sharing apps have surge pricing during high-traffic times, thanks to a partnership with Gauntlet, Balancer pools can optimize fees for current market conditions.
