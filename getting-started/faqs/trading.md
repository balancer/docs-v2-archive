# Trading

## How do I make my first swap?

First time here? Check out [this tutorial](../walkthroughs/trading.md) for a walkthrough on how to make your first trade. 

In short, you'll need:

* ETH to pay for gas fees
* ERC20 tokens \(or ETH\) to trade
* An Ethereum address you can use with one of the following compatible wallets
  * MetaMask
  * Coinbase Wallet
  * A WalletConnect compatible wallet
  * Portis
  * Fortmatic

## What is Slippage?

Slippage is how much the price of an asset changes during a trade. To make sure you get within the price range you expect, trades have Slippage Tolerances. You can change this tolerance by in the slippage settings.

## Is it cheaper in gas fees to trade with ETH or WETH?

WETH is slightly cheaper. If you happen to have WETH on hand, you'll save a bit of gas by using it directly. When making a trade with ETH, it will be wrapped into WETH first, which has a small gas fee associated with it.

## What is the Smart Order Router?

The Smart Order Router \(SOR\) is a system that intelligently sources liquidity from multiple pools so as to automatically figure out the best available price from the range of available pools.

## How is Balancer V2 more gas efficient?

Balancer V2 consolidates each pool’s assets in the Vault, which holds the assets for all Balancer pools. Even though trades can be carried out in batches against multiple pools, only the final net token amounts are transferred from and to the vault, saving a significant amount of gas in the process. While previous multi-hop trades would have required as many token transfers as hops, the Vault simplifies the trade by only transferring the input and final output tokens; all other swaps are done with internal balances.

## Can I trade if I have no tokens?

Yes**\***, Flash Swaps allow arbitrageurs to find and swap imbalanced pools and claim the difference as profit. Since only final net amounts are transferred, arbitrage trades are also significantly easier. An arber who has no tokens but detects a price asymmetry between Balancer pools could trade DAI for MKR in pool 1, MKR for BAL in pool 2 then BAL for DAI in pool 3 and end up making a profit in DAI.

**\***You'll still need ETH to pay gas fees

## What happens if my transaction fails?

Unfortunately, if your transaction fails you will lose your gas fees. Miners collect these gas fees when attempting to execute your trade; they are not collected by Balancer.

## What are Internal Balances?

Internal Balances are tokens that you have inside the Balancer Vault. You can supply the Vault with tokens, and once they're inside, you'll be able to trade without needing to move ERC20 tokens, saving you a lot of money on gas fees. The only ERC20 token transfers you need to perform are when you're initially putting your tokens in the Vault and withdrawing them later.

## Why should I use Internal Balances?

If you are trading ETH for DAI but know that you’ll trade DAI back to ETH in a few hours, you can keep both tokens in the vault and use them for your next trade without the need for a useless intermediate ERC20 transaction.

