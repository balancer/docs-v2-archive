# Weighted Math

## Overview

Weighted Math is designed to allow for swaps between any assets whether or not they have any price correlation. Prices are determined by the pool balances, pool weights, and amounts of the tokens that are being swapped.

Balancer's Weighted Math equation is a generalization of the $$x*y=k$$ constant product formula recommended for Automated Market Makers (AMMs) in [a post by Vitalik Buterin](https://www.reddit.com/r/ethereum/comments/55m04x/lets\_run\_onchain\_decentralized\_exchanges\_the\_way/). Balancer's generalization accounts for cases with $$n \geq2$$ tokens as well as weightings that are not an even 50/50 split.&#x20;

As the price of each token changes, traders and arbitrageurs rebalance the pool by making swaps. This maintains the desired weighting of the value held by each token whilst collecting trading fees from the traders.

For more weighted math formulas, [check out the Developer Docs](https://dev.balancer.fi/resources/pool-math/weighted-math).

## Invariant

The value function $$V$$is defined as:

$$
V= \prod_t B_t^{W_t}
$$

Where

* $$t$$ ranges over the tokens in the pool
* $$B_t$$ is the balance of the token in the pool
* $$W_t$$​is the normalized weight of the tokens, such that the sum of all normalized weights is 1.
