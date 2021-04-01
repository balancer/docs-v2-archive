# Risks

Here we could mention the emergency stop mechanism - Balancer governance \*temporarily\* has the ability to halt swaps on the entire Vault, or disable individual pools. After the emergency period expires, the Vault becomes trustless, and the only things governance controls are 1\) protocol-level fees, 2\) whitelisting relayers, 3\) Oracle pool assignments/overrides; 4\) setting the dynamic swap fee provider \(e.g., Gauntlet\) on pools where that is enabled - which is all our standard Weighted/Stable pools

