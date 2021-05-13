# The Vault

## What is the Vault?

It is a single contract that holds and manages all the assets added by all Balancer pools. This allows Balancer to take full advantage of its multi-pool trading routing in order to offer the best trade routing options.

### How does the Vault work?

Balancer V2 separates the Automated Market Maker \(AMM\) logic from the token management and accounting. Token management/accounting is done by the vault while the AMM logic is individual to each pool.

Because pools are contracts external to the vault, they can implement any arbitrary, customized AMM logic.

## What are Internal Balances?

{% hint style="warning" %}
Important: **DO NOT** blindly transfer tokens to the Vault expecting to get an Internal Balance. They must be added through the UserBalance smart contract.
{% endhint %}

Internal token balances are tokens that belong to you that are kept inside the Vault. They are extremely useful for high-frequency trading since they require no external token transfers. The only ERC20 token transfers you need to perform are when you're initially putting your tokens in the Vault and withdrawing them later.

