# Emergency Pause

The Balancer V2 Vault and WeightedPool contracts have an emergency pause mechanism which can be activated within the first three months of mainnet operation. After three months, the mechanism cannot be activated by anyone, including the Balancer Governance Multisig and Balancer Labs. After three months, Balancer V2 becomes unstoppable.

The emergency pause is only meant to be activated in the event of a serious vulnerability being discovered which puts user funds at risk. During the pause, all trading is halted and liquidity can no longer be _added_ to the Vault, but **liquidity can always be removed by users**, even while the protocol is paused. Pausing does not grant anyone, including the Balancer Governance Multisig or Balancer Labs, direct access to user funds. It simply creates a safe environment in which funds can be withdrawn and any potential attack on the protocol can be mitigated.

By default, at deployment time, the Balancer Governance Multisig was the only entity with the authority to activate the emergency pause. But in the week immediately following the initial deployment, [Balancer governors voted to also grant this same authority to an EOA (Externally Owned Address) controlled by Balancer Labs.](https://vote.balancer.fi/#/proposal/Qma3oK8Ltq6YqLvh4xBc359LvYpkQ3b6kxhTCVMnDkHb1M) There is some concern that the Multisig may not be able to coordinate quickly enough during an emergency situation, so this EOA address is controlled by a handful of stakeholders at Balancer Labs across different time zones to ensure quick response time to potential emergencies. Again, to be clear, this address has no control over user funds and can only pause the system to protect funds from being drained (and only within the first three months).

{% hint style="info" %}
The emergency pause period ended on July 18, 2021. The Vault and WeightedPools are now immutable.
{% endhint %}

## The Emergency subDAO



The [Emergency DAO](https://dao.curve.fi/emergencymembers) is an idea pioneered by Curve that empowers a small group to “kill” pools and gauges **in the** **event of malicious activity and/or potential loss of funds.**

The Emergency subDAO is a 4-of-7 multisig with the following members:

* Solarcurve (0x512fce9B07Ce64590849115EE6B32fd40eC0f5F3)
* Mike B (0xF01Cc7154e255D20489E091a5aEA10Bc136696a8)
* Zekraken (0xafFC70b81D54F229A5F50ec07e2c76D2AAAD07Ae)
* Zen Dragon (0x7c2eA10D3e5922ba3bBBafa39Dc0677353D2AF17)
* Markus (0x6bB4720473d4D7133f944785e5EE1A650C07f34e)
* Fernando (0xbbF0Ae5195444264364CA7eb7E3BB1971B4c3eCb)
* Nico (0x815d654E930E840D0E0Ee1B18FFc8Fb4ddA4c6B3)

Gnosis safe address: `0xA29F61256e948F3FB707b4b3B138C5cCb9EF9888`

An additional power of the Emergency subDAO will be to add a token to the deny list on the newly created “[ProtocolFeesWithdrawer](https://forum.balancer.fi/t/introduce-protocolfeeswithdrawer/3188)” contract. In order for a token to be added back to the allow list a veBAL governance vote would be required. A token would only be added to the deny list in the event of an issue along the lines of the recent [Synthetix bug disclosure](https://forum.balancer.fi/t/medium-severity-bug-found/3161).

