# Stable Pools

## Overview

Stable Pools are designed specifically for assets that are expected to consistently trade at near parity, such as different varieties of stablecoins or synthetics. Stable Pools use [Stable Math](../../concepts/math/stable-math.md) (based on StableSwap, popularized by Curve) which allows for significantly larger trades before encountering substantial price impact, vastly increasing capital efficiency for like-kind swaps.

## Advantages

#### Low Price Impact

Traders enjoy tighter spreads and lower price impact. These pools allow for larger trades of assets before encountering significant price impact. 

#### Stable Swaps Under the Balancer Umbrella

One of the key advantages to having Stable Pools on Balancer specifically is that they are plugged into the same protocol as all other pools. Swapping between stable coins is frequently used for arbitrage when one token is paired with two different stable coins in different pools. By leveraging Batch Swaps on Balancer, these trades can be combined into a single, gas efficient transaction.

## Use Cases

The two largest stable pools in use right now are for USD stablecoins and tokens that track Bitcoin:

* ****[**staBAL3-USD**](https://app.balancer.fi/#/pool/0x06df3b2bbb68adc8b0e302443692037ed9f91b42000000000000000000000063)** composed of DAI/USDC/USDT**
* ****[**staBAL3-BTC**](https://app.balancer.fi/#/pool/0xfeadd389a5c427952d8fdb8057d6c8ba1156cc56000000000000000000000066)** composed of WBTC/renBTC/sBTC**
