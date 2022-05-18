# Balancer CoW Protocol

![](<../.gitbook/assets/Screen Shot 2021-11-02 at 2.25.01 PM.png>)

## Overview

The Balancer CoW Partnership (BCP) is the default trade interface on [app.balancer.fi](https://app.balancer.fi). Users of BCP can benefit from:

* Gasless trades
* MEV protection
* Best on-chain prices available
* No gas fees charged for failed transactions
* Transaction management that a professional third party handles

## What is BCP?

The Balancer CoW Protocol is a trade interface that uses **CoW Solvers** tightly integrated with the Balancer Vault to execute trades in batches. Using CoW Solvers, traders submit their swaps by simply signing a message to send a **gasless trade**. The solvers then prioritize matching the various trades to take advantage of any possible **Coincidence of Wants** ([more on those below](balancer-cow-protocol.md#here-come-the-cows) :point\_down:) before settling the remaining trades using on-chain liquidity, which allows the solvers to **protect traders for Miner Extractable Value** (MEV).

BCP utilizes multiple different Decentralized Exchanges to ensure **traders always get the best price**; however, its tight integration with Balancer's Vault allows it to execute complex multihop trades with minimal token transfers, drastically reducing transaction costs. And since BCP batches gasless transactions together, **failed trades result in no loss of fees**.

Read the announcement post [here](https://medium.com/balancer-protocol/two-protocols-one-dex-introducing-the-balancer-gnosis-protocol-f471aaeb4dce)!

## Here Come The CoWs

![](<../.gitbook/assets/Screen Shot 2021-11-02 at 3.52.02 PM.png>)

Coincidence of Wants (CoWs) refers to an economic phenomenon in which peer-to-peer trades are settled directly **without** using an AMM, therefore without incurring any slippage and fees. CowSwap, the first trading interface built on CoW Protocol, allows users to buy and sell tokens using gasless orders settled peer-to-peer or into any on-chain liquidity source while providing MEV protection. BCP uses Coincidence of Wants, removing the need for an external market maker or liquidity provider; this allows users to save on gas costs, slippage tolerance, and protocol fees.
