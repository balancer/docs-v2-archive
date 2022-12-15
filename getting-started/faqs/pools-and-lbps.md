# Pools and LBPs

## What kind of pools exist of Balancer V2?

Balancer V2 pioneers customizable AMM logic by creating a launchpad for teams to innovate with different AMM strategies. This means if you want to launch a new style of trading pool, you can focus on the high-level concepts without having to worry about low-level token transfers, balance accounting, security checks and order routing. With Balancer V2, this all comes out of the box.

Some existing pool types are:

* **Weighted Pools** - 8-token pools with custom weighting
* **Two-Token Weighted Oracle Pools** - Weighted Pools with two tokens that act as on-chain price oracles
* **Stable Pools** - Pools with 2-5 tokens that use a StableSwap equation, and contain tokens of similar value. For example, DAI/USDC/USDT, and WBTC/renBTC/sBTC
* **Liquidity Bootstrapping Pool** - A 2-4 token pool with the ability to enable and disable trading, and change weights. Only the creator can add liquidity.
* **MetaStable Pools** - A generalized Stable Pool that can hold "proportional" assets that are related in price but may slowly drift apart in price. Some example use cases are pools of (DAI/cDAI) and (StablePoolBPT/NewStableCoin)
* **Investment Pools** - An LBP-like pool with the same rights to disable trading and change weights, but which allows public LPs. It also supports management fees (as a percentage of swap fees), and higher token counts.
* **Convergent Curve Pools** - A pool designed by Element.fi to support two tokens that converge in price. [Learn more here](https://docs.element.fi/developers/element-smart-contracts/custom-balancer-curve/convergent-curve-pool)!

Balancer Labs is currently developing and testing:

* **HeavyWeight Pools** - WeightedPools that can support up to 20-tokens, but are otherwise identical.
* **Managed Pools** - (name TBD - second generation Investment Pools), with all current Investment Pool features, but better scaling to higher token counts (e.g., 50). They will also have advanced features, such as circuit breakers (restricting trading to price ranges), different types of management fees, and the ability to add/remove tokens from the pool.\
  \
  There will be additional flexibility for pool ownership, likely in the form of pool owner template contracts that can be deployed as the immutable pool owners. For instance, there could be a "Gauntlet" template that allows a third party to control swap fees, while reserving all other permissioned functions to a different multi-sig. That way Managed Pool issuers could contract with Gauntlet (or another provider) to provide a fee optimization service for investors.

## Can I have nested pools?

Yes, you can create Balancer pools of Balancer pools. This can fill the need of products that want to aggregate across many different products — imagine a project which tokenizes real estate and has separate Balancer pools for each city — a composed version of that pool could represent a whole state.

## What is an LBP?

For V1 LBPs, see [this FAQ](https://docs.balancer.fi/v/v1/smart-contracts/smart-pools/liquidity-bootstrapping-faq). \
\
It is a smart pool that dynamically changes the token weighting (e.g 1%/99% ETH/$TOKEN to 99%/1% ETH/$TOKEN), allowing founders to create a liquidity bootstrapping pool with minimal capital requirements. The result is that the token price continually experiences downward pressure throughout the sale. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once.

[Fjord Foundry](https://fjordfoundry.com/pools) among others is a platform for Fair Launch Auctions (FLAs) — a simple crowdfunding mechanism that enables projects and ideas from across the world to raise money from individuals without barriers to entry. Fjord makes it easy to create and use LBPs through their intuitive and easy-to-use website. The main concept allows distribution of Tokens and NFTs with transparent, open and fair price discovery mechanism. Fjords long-standing reputation led to a recent [exclusive collaboration agreement](https://snapshot.org/#/balancer.eth/proposal/0xcc065f373e15a264e1647bc794a4a83039fc4d377a69875ec828eb0148faa4ba) between the Balancer DAO and Fjord Foundry.

## How long do LBPs last?

LBPs can live as long as the creators decide they should. In general, pool creators tend to run them for less than 2 weeks.

## How does the pricing in LBP work?

At the creation of an LBP the team should set up a price that is significantly higher than what they think is a market price. After the launch, the token price continually experiences downward pressure throughout the sale, until it reaches the right market price. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once.

## Should I join an LBP as soon as it launches?

No, this is not the point. Prices are _supposed_ to start intentionally high and then come down. If you join early may end up paying way more than if you wait for the price to stabilize.
