# Pools and LBPs

## I see many types of pools, how are they different?

In V1 there are three types of Pools:

* public pools \(also called shared\)— anyone can add liquidity \(and get Balancer Pool Tokens in return\), but all the pool parameters are fixed forever. \(trustless, finalized\)
* private pools — all the parameters are flexible — only the owner can change them but also only the owner can add liquidity \(trusted, unfinalized\)
* smart pools — anybody can add liquidity to them and the parameters can be fixed or dynamic controlled through smart contracts. \(trustless, flexible\).

Initially in V2 there will be two pool types

* weighted pools - permissionless, 8-token pools like V1 shared pools - but more gas efficient
* two-token weighted oracle pools - permissionless weighted pools with two tokens that act as on-chain price oracles

Balancer Labs is currently developing and testing:

* stable pools -- suitable for tokens that are soft pegged to each other \(building on the great work by the Curve team\).
* LiquidityBootstrappingPool - these will be used for LBPs in V2 . It is a 2-token pool with pause and weight change rights. You can revoke the rights and transform it into a smart treasury or Weighted Pool equivalent.
* Smart versions of the Weighted and Stable pools \(with the same rights as V1, and more - and they are revocable, so can become more trustless over time\).

## Can I have nested pools?

Yes, you can create Balancer pools of Balancer pools. This can fill the need of products that want to aggregate across many different products — imagine a project which tokenizes real estate and has separate Balancer pools for each city — a composed version of that pool could represent a whole state.

## What is an LBP?

{% hint style="info" %}
Coming soon on V2
{% endhint %}

It is a short-lived smart pool which dynamically changes their token weighting \(e.g 1%/99% ETH/$TOKEN to 99%/1% ETH/$TOKEN\), allowing founders to create a liquidity bootstrapping pool with little required capital from their side. The result is that the token price continually experiences downward pressure throughout the sale. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once. PrimeDAO is building the IDO Launchpad, which will streamline the process for a smoother experience. 

## How long do LBPs last?

LBPs can live as long as the creators decide they should. In general, pool creators tend to run them for less than 2 weeks.

## How does the pricing in LBP work?

At the creation of an LBP the team should set up a price that is significantly higher than what they think is a market price. After the launch, the token price continually experiences downward pressure throughout the sale, until it reaches the right market price. When this is mixed with modest buying demand, the price stays stable throughout the sale, as whales/bots are disincentivized to buy it all at once.

## Should I join an LBP as soon as it launches?

No, this is not the point. Prices are _supposed_ to start intentionally high and then come down. If you join early may end up paying way more than if you wait for the price to stabilize.

## Why do teams decide to launch an LBP?

Funders create a liquidity bootstrapping pool with little required capital from their side.

