# Liquidity

## What does the customizable AMM logic mean for me?

Balancer V2 pioneers customizable AMM logic by creating a launchpad for teams to innovate with different AMM strategies without having to worry about low-level token transfers, balance accounting, security checks and smart order routing. With Balancer V2, this all comes out of the box.

## How do Liquidity Providers earn Yield?

Balancer LPs can earn yield in a few ways:

* Swap fees \(which can be dynamically optimized in Gauntlet pools!\)
* Asset Managers

In addition, some pools in V2 are eligible for Governance Distributions through the Liquidity Mining program.

## How does a pool determine the price of tokens?

In general the AMM logic determines the prices that traders pay. If a pool is designated as the Oracle for a Token Pair, dApps are able to query prices with minimal gas costs and without having to store past accumulator states. We plan on offering two types of prices that can be queried with low gas costs:

* Instant: A more up-to-date price but less resilient to manipulation
* Resilient: A less up-to-date price but more resilient to manipulation

