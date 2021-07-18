# Pools and LBPs

## I see many types of pools, how are they different?

In V1 there are three types of Pools:

* public pools \(also called shared\)— anyone can add liquidity \(and get Balancer Pool Tokens in return\), but all the pool parameters are fixed forever. \(trustless, finalized\)
* private pools — all the parameters are flexible — only the owner can change them but also only the owner can add liquidity \(trusted, unfinalized\)
* smart pools — anybody can add liquidity to them and the parameters can be fixed or dynamic controlled through smart contracts. \(partially trustless, flexible\).

Initially in V2 there are currently three core pool types

* weighted pools - permissionless, 8-token pools like V1 shared pools - but more gas efficient
* two-token weighted oracle pools - permissionless weighted pools with two tokens that act as on-chain price oracles
* stable pools - permissionless pools with 2-5 tokens that use different math \(similar to Curve\), and contain tokens of similar value. For example, DAI/USDC/USDT, and WBTC/renBTC/sBTC.

Balancer Labs is currently developing and testing:

* "Heavyweight" pools - WeightedPools that can support up to 20-tokens, but are otherwise identical.
* Metastable pools -- a generalized stable pool that can hold "proportional" assets \(e.g., DAI/cDA\), or 
* LiquidityBootstrappingPool - this will be used for LBPs in V2 . It is a 2-5 token pool with the ability to enable and disable trading, and change weights. Only the creator can add liquidity.
* Investment pools - pools with up to 100 tokens, with LBP-like rights to disable trading and change weights, but which do allow public LPs. They will also have advanced features, such as circuit breakers \(halting trading automatically to limit IL\), different types of management fees, and the ability to add/remove tokens from the pool.

## Can I have nested pools?

Yes, you can create Balancer pools of Balancer pools. This can fill the need of products that want to aggregate across many different products — imagine a project which tokenizes real estate and has separate Balancer pools for each city — a composed version of that pool could represent a whole state.

## What is an LBP?

{% hint style="info" %}
Coming soon on V2
{% endhint %}

For V1 LBPs, see [this FAQ](https://docs.balancer.fi/v/v1/smart-contracts/smart-pools/liquidity-bootstrapping-faq).   
  
It is a smart pool that dynamically changes the token weighting \(e.g 1%/99% ETH/$TOKEN to 99%/1% ETH/$TOKEN\), allowing founders to create a liquidity bootstrapping pool with minimal capital requirements. The result is that the token price continually experiences downward pressure throughout the sale. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once. PrimeDAO is building the IDO Launchpad, which will streamline the process for a smoother experience. Other partners are building UIs as well.

## How long do LBPs last?

LBPs can live as long as the creators decide they should. In general, pool creators tend to run them for less than 2 weeks.

## How does the pricing in LBP work?

At the creation of an LBP the team should set up a price that is significantly higher than what they think is a market price. After the launch, the token price continually experiences downward pressure throughout the sale, until it reaches the right market price. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once.

## Should I join an LBP as soon as it launches?

No, this is not the point. Prices are _supposed_ to start intentionally high and then come down. If you join early may end up paying way more than if you wait for the price to stabilize.

## Why do teams decide to launch an LBP?

Funders create a liquidity bootstrapping pool with little required capital from their side.

