# Trading

## How does Gas Efficiency work?

Balancer V2 consolidates each pool’s assets in the Vault, which holds the assets for all Balancer pools. Even though trades can be carried out in batches against multiple pools, only the final net token amounts are transferred from and to the vault, saving a significant amount of gas in the process. While previous multi-hop trades would have required as many token transfers as hops, the Vault simplifies the trade by only transferring the input and final output tokens; all other swaps are done with internal balances.

## Can I trade if I have no tokens?

Yes, Flash Swaps allow arbitrageurs to find and swap imbalanced pools and claim the difference as profit. Since only final net amounts are transferred, arbitrage trades are also significantly easier. An arber who has no tokens but detects a price asymmetry between Balancer pools could trade DAI for MKR in pool 1, MKR for BAL in pool 2 then BAL for DAI in pool 3 and end up making a profit in DAI.

## What is Net Token Transfer?

The final amount that is being transferred from and into the vault \(via an ERC20 transaction\). The result of using Internal Token Balancer.

## What happens when my transaction fails?

Unfortunately, if your transaction fails you will lose your gas fees. This is not dependent on Balancer - it is part of the Ethereum design.

## What are Balancer Price Oracles \(coming soon\)?

Balancer V2 will make the protocol more resilient and user-friendly by introducing price oracles that are resistant to such sandwich attacks by leveraging accumulators \(as pioneered by Uniswap V2\).

There are two types of oracles that can be queried for low gas costs:

* Instant — A more up-to-date price but less resilient to manipulation
* Resilient — Less up-to-date but more resilient to manipulation

The existence of two price types allows projects to use the one that best fits their use case — a lending protocol would likely use the resilient price whereas something like a prediction market may prefer the instant price.

## How do Balancer Oracles avoid Sandwich Attacks?

Balancer V2 will make the protocol more resilient and user-friendly by introducing price oracles that are resistant to such sandwich attacks by leveraging accumulators \([as pioneered by Uniswap V2](https://uniswap.org/blog/uniswap-v2/#price-oracles)\).

## How do I decide which type of Oracle to choose?

Choosing a price type varies depending on each use case. For example, lending protocols will likely rely on the resilient price while prediction markets could use the instant price.

## What is the Smart Order Router?

The Smart Order Router \(SOR\) is a system that intelligently sources liquidity from multiple pools so as to automatically figure out the best available price from the range of available pools

