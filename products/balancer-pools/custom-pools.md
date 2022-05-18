# Custom Pools

## Overview

With Balancer's abstracted Vault and Pool architecture, designers creating their own AMM only need to worry about their price curves since all the token bookkeeping is handled by The Vault. Since Balancer is permissionless, anyone can develop their own custom Pool Type and integrate it into the protocol. Custom Pool Types are ideal for any team developing custom trade equations and strategies.

## Advantages

### Tap into Balancer's Existing Liquidity

Rather than launching their own Decentralized Exchanges and worrying about attracting liquidity, teams can launch on top of Balancer, allowing them to directly tap into Balancer's existing liquidity from Day 0.

### Worry About The Math, Not The Bookkeeping

Instead of worrying about the accounting groundwork, pool designers only need to worry about their pricing functions. For a custom pool type, they just need to implement functionality for joining, exiting, and trading with a pool.

## Use Cases

### **Element.fi**

> _“We use Balancer V2’s custom trading curve functionality to enable an invariant that works really well for assets that converge in value over time. Plugging into the V2 ecosystem lets users be able to purchase and sell fixed yield assets from any other major asset, building on the existing liquidity Balancer has.” —_ Will Villanueva, CEO & Co-Founder of [Element Finance](https://element.fi/)

By focusing on the math, the Element team was able to create pools that use their Convergent Curve equation and plug right into Balancer's framework. The Element Pools handle the calculations while the Balancer Vault ensures that all tokens are properly accounted for. To learn more, check out [Element's documentation](https://docs.element.fi/developers/element-smart-contracts/custom-balancer-curve/convergent-curve-pool).
