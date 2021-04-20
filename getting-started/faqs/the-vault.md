# The Vault

### What is the Vault?

It is a single contract that holds and manages all the assets added by all Balancer pools. The benefit is that what would have been multiple token transfers before, each with gas fees, now is a single transfer pair. This allows Balancer to take full advantage of its multi-pool trading routing so as to offer the greatest possible liquidity with the lowest possible slippage.

![Changes in the architecture of the Balancer Pools](../../.gitbook/assets/image%20%284%29.png)

### How does the Vault work?

Balancer V2 separates the Automated Market Maker \(AMM\) logic from the token management and accounting. Token management/accounting is done by the vault while the AMM logic is individual to each pool.

Because pools are contracts external to the vault, they can implement any arbitrary, customized AMM logic.

## What are Internal Balances?

{% hint style="warning" %}
Important: **Do not** blindly transfer tokens to the Vault expecting to get an Internal Balance. They must be added through the UserBalance smart contract.
{% endhint %}

Internal token balances are tokens that belong to you that are kept inside the Vault. They are extremely useful for high-frequency trading since they require no external token transfers. The only token ERC20 transfers you need to perform are when you're initially putting your tokens in the Vault and withdrawing them later.

