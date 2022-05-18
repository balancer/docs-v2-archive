# Liquidity Bootstrapping Pools (LBPs)

## Overview

Liquidity Bootstrapping Pools (LBPs) are pools that can dynamically change token weighting (e.g 1/99 to 99/1 for TokenA/TokenB). LBPs use [Weighted Math ](../../concepts/math/weighted-math.md)with time-dependent weights. The starting and end weights and times are selected by the pool owner, who also has the power to pause swaps.&#x20;

## Advantages

### Sell Pressure

During a weight shift, the token price of one token experiences sell pressure while the other experiences buy pressure. When this is mixed with modest trading volume, the price approaches the generally agreed-upon market price.&#x20;

### Fair Market

LBPs often start with intentionally high prices. This strongly disincentivizes whales and bots from snatching up much of the pool liquidity at the get-go. When LBPs are used for early-stage tokens, this can help increase how widespread the token distribution is.

### Starting Capital Can Be Small

Teams who use LBPs to kickstart the liquidity of a token that has not been well distributed yet can do so with minimal starting capital. For a team running an LBP with their TOKEN and DAI, starting with 10% or 20% DAI, as opposed to 50% DAI __ like they might need on another platform, significantly reduces their starting capital requirements. Shifting from 80/20 TOKEN/DAI __ to 20/80 would look like this:

![](https://lh3.googleusercontent.com/jJSoUvPnPwQFAEemsJlKZctFspEJrRQhRIncmoaaq5a6\_CzyXssVwokti4HQQyIBqVcv5GG9bMKDplrAaDIC3MkdFoVJAprLHu\_NhTSWW4GEoMRe3mUhFnB0lG3kVqIGvjK7aGJD=s0)

and would ultimately result in the team holding far more DAI __ at the end of their LBP while reducing the (sometimes extreme) price volatility that teams experience when just launching a 50/50 pool.

## Use Cases

### Copper Fair Launch Auctions

[Copper](https://copperlaunch.com/) is a platform for Fair Launch Auctions (FLAs) — a simple crowdfunding mechanism that enables projects and ideas from across the world to raise money from individuals without barriers to entry. Copper makes it easy to create and use LBPs through their intuitive and easy-to-use website.

### Gitcoin's AKITA/ETH LBP

[Gitcoin's LBP](https://copperlaunch.com/v1/auctions/0xb00d4c6966f07f045411ec201f657f376b33c0c3) is composed of AKITA and WETH, and is meant to slowly transfer the Akita held by Gitcoin (as donated by Vitalik) back to the community. Using an LBP here is useful in performing a gradual sale with continuous pressure. Gitcoin is running a few of these in succession to validate the process, raise more ETH for the next LBPs, and also help fund public goods. Some of the ETH generated will be split with the Akita Development fund and a Dog Rescue charity.
