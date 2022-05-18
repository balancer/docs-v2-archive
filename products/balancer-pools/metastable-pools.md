# MetaStable Pools

## Overview

MetaStable Pools are an extension of Stable Pools that contain tokens with known exchange rates. MetaStable Pools use [Stable Math](../../concepts/math/stable-math.md) in conjunction with this known exchange rate. They are great for tokens with highly correlated, but not pegged, prices.&#x20;

## Advantages

### Trades between correlated but non-pegged tokens

#### Pegged vs Correlated but Non-Pegged

**Pegged** tokens such as different stablecoins representing US Dollars or groups of tokens that all track BTC are well suited for[ Stable Pools](stable-pools.md).

**Correlated but Non-Pegged** tokens are often (but not always) base tokens and their derivatives. For example, DAI/cDAI have very strong correlation, but cDAI slowly accumulates lending fees by lending DAI to the Compound protocol, and appreciates relative to DAI.&#x20;

## Use Cases

### **The Lido wstETH/WETH Liquidity Pool**

![](https://lh6.googleusercontent.com/u1Zmk3-eal-Fi7HpOQ24qwFtZNU2O3IA0cKY2lq\_P9J2jwXvxtnmadWRVPsCp\_V3UBmVoKQI0\_daYuKsTTX1vU40mOmhyh66TMkJfN\_70i8a3hCS0KNw6LaR9G3LEcnxcX5jIdPi=s0)

[Lido](https://lido.fi/) is a liquid staking solution for ETH 2.0 backed by industry-leading staking providers. Lido lets users stake their ETH - without locking assets or maintaining their own infrastructure. The goal is to solve problems associated with initial ETH 2.0 staking: illiquidity, immovability and accessibility by making staked ETH liquid and allowing for participation with any amount of ETH to improve security of the Ethereum network.

stETH is a token that represents **Staked Ether**, combining the value of deposited ETH with staking returns. As an ERC20, stETH tokens can be traded as one would swap WETH, allowing the benefits of ETH 2.0 staking rewards while allowing users to continue using their staked Ether on decentralized finance products.

Balancer MetaStable pools are ideal for the wstETH-WETH pair as the stETH asset is highly correlated but not pegged 1:1 to ETH as it accrues staking returns.

Note: To overcome Balancer's incompatibility with streaming/rebasing tokens, stETH must be wrapped into wstETH. This is done through a relayer contract.
