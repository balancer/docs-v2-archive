# V1 -&gt; V2 Migration

## How do I migrate from V1 to V2?

For two asset pools, you can automatically migrate your liquidity from comparable pools. See more \(TODO: here.\)

For pools with more than two assets, we recommend manually removing liquidity from V1 and and re-adding your liquidity to V2. \(TODO: is this what we are advising? what about identical pools?\)

## What happens if I don't migrate?

Balancer V1 is not being "turned off" \(it can't be even if we wanted to\), so if you choose not to migrate, your liquidity will remain in the older trading pools. Trade aggregators will likely \(TODO: definitely?\) still consider V1 pools when looking for the cheapest prices, but as liquidity falls and price slippage increases, it may not be worth the gas fees for them to use those pools.

Balancer V1 pools will continue earning trade fees, but the BAL governance distributions will transition to V2. 

\(TODO: is the SOR going to consider V1 pools?\)

## Does the BAL for Gas program apply to migrating my liquidity?

\(TODO: I have no idea\)



