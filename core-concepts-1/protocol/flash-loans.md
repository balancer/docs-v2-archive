# Flash Loans

* Vault architecture consolidates all tokens in one contract
* Does not reduce slippage on a per-pool basis, but does enable flash loans
* Flash Loan Workflow
  * Phase 1: Borrow X amount of TokenA
  * Phase 2: ???
  * Phase 3: Profit
  * Phase 4: Return X \* \(1+interest\_rate\) of TokenA
* If return amount &lt; X \* \(1+interest\_rate\), revert transaction



