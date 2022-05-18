# Emergency Pause

The Balancer V2 Vault and WeightedPool contracts have an emergency pause mechanism which can be activated within the first three months of mainnet operation. After three months, the mechanism cannot can be activated by anyone, including the Balancer Governance Multisig and Balancer Labs. After three months, Balancer V2 becomes unstoppable.

The emergency pause is only meant to be activated in the event of a serious vulnerability being discovered which puts user funds at risk. During the pause, all trading is halted and liquidity can no longer be _added_ to the Vault, but **liquidity can always be removed by users**, even while the protocol is paused. Pausing does not grant anyone, including the Balancer Governance Multisig or Balancer Labs, direct access to user funds. It simply creates a safe environment in which funds can be withdrawn and any potential attack on the protocol can be mitigated.

By default, at deployment time, the Balancer Governance Multisig was the only entity with the authority to activate the emergency pause. But in the week immediately following the initial deployment, [Balancer governors voted to also grant this same authority to an EOA \(Externally Owned Address\) controlled by Balancer Labs](https://snapshot.org/#/balancer/proposal/Qma3oK8Ltq6YqLvh4xBc359LvYpkQ3b6kxhTCVMnDkHb1M). There is some concern that the Multisig may not be able to coordinate quickly enough during an emergency situation, so this EOA address is controlled by a handful of stakeholders at Balancer Labs across different time zones to ensure quick response time to potential emergencies. Again, to be clear, this address has no control over user funds and can only pause the system to protect funds from being drained \(and only within the first three months\).

{% hint style="info" %}
The emergency pause period ended on July 18, 2021. The Vault and WeightedPools are now immutable.
{% endhint %}

