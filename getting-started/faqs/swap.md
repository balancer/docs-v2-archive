# Swap

## How do I make my first swap?

First time here? Check out this tutorial for a walkthrough on how to make your first trade. 

In a nutshell though, you'll need:

* ETH to pay for gas fees
* ERC20 tokens \(or ETH\) to trade
* An Ethereum address you can use with one of the following compatible wallets
  * MetaMask
  * Coinbase Wallet
  * A WalletConnect compatible wallet
  * Portis
  * Fortmatic

For each of the steps below, you'll need to pay a gas fee and wait for your transaction to be approved. You can check transaction status on [etherscan.io](https://etherscan.io/) 

1. Unlock your **input** token to allow the Balancer Vault to make a swap. 
2. Once unlocked, you can trade that token for any other token in a Balancer pool.

## How do I use Internal Token Balances?

Internal Balances are tokens that you have inside the Balancer Vault. You can supply the Vault with tokens, and once they're inside, you'll be able to trade without needing to move ERC20 tokens, saving you a lot of money on gas fees. The only token ERC20 transfers you need to perform are when you're initially putting your tokens in the Vault and withdrawing them later.

Balancer V2 allows users to hold internal token balances inside the vault. For example, if you are trading ETH for DAI but know that you’ll trade DAI back to ETH in a few hours, you can keep both tokens in the vault and use them for your next trade without the need for a useless intermediate ERC20 transaction.

## What is Slippage?

Slippage is how much the price of an asset changes during a trade. To make sure you get within the price range you expect, trades have Slippage Tolerances. You can change this tolerance by in the slippage settings.

## Is it cheaper in gas fees to trade with ETH or WETH?

WETH is slightly cheaper. If you happen to have WETH on hand, you'll save a bit of gas by using it directly. When making a trade with ETH, it will be wrapped into WETH first, which has a small gas fee associated with it.



