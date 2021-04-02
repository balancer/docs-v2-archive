# Pools

## Overview

![Each pool can implement its own logic while integrating into Balancer](../../.gitbook/assets/image.png)

* Pool logic abstracted from token transfers \(Vault\)
*  * Weighted Swaps
  * StableSwap
  * Other custom AMM curves

## Standard Pools

Balancer V2 will launch with two officially supported pool types.

* Standard weighted pools
* Stable pools

## Custom Pools

Arbitrary AMM pricing curves

* Anybody can deploy their own pool type and use it 

## Smart Pools

The flexibility introduced doesn't just extend to control over the pricing curve used by the pool but can effect any aspect of the pool.

Balancer V1 introduced the concept of smart pools where parameters can change over time, in V2 these features can be integrated directly into the pools themselves.

* Extensible to include anything you might want



