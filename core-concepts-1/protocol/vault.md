# Vault

* Vault holds all tokens
* Gas efficiency
* Multihop swaps happen with internal balances, only net tokens are actually moved
* Internal token balances
* Pool balances are still independent from all other tokens
  * Having one contract hold all tokens does \*not\* decrease slippage
* Enables flash loans
* Flash swaps reward capital-less arbitrageurs

![The Vault holds all pool tokens while logic is handled by pool contracts](../../.gitbook/assets/vault.png)

