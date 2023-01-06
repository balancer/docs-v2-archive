# Governance

## Overview

Balancer Governance is the heart and brain of Balancer Protocol.&#x20;

Anyone can be part of the Balancer Governance Process, and anyone with BAL voting power can vote on proposals. Governance makes decisions about new features and directions of where the Balancer Protocol should go. Governance is the ultimate decision body for the Balancer Protocol; no one can override vote results.&#x20;

## [Governance Process](governance-process/)

The Balancer Governance Process tracks an initiative from discussion, to proposal, to a vote, to enactment. It is designed to be an open, transparent, and intuitive way to progress the future of the protocol.

## [BAL Governance Token](bal-governance-token.md)

Voting power for the Balancer Protocol is derived from the Balancer Governance Token (BAL). BAL holders, also called Balancer Governors, vote on proposals relevant to the protocol. These proposals are wide ranging, from Governable Protocol Fees to how BAL Tokens themselves are distributed into the future.

## [Snapshot](snapshot.md)

Snapshot, a spinoff of Balancer, is an off-chain gasless multi-governance client with easy to verify and hard to contest results. Balancer Governance Votes take place on Snapshot.

## [Multisig](multisig/)

To enact the off-chain votes on Snapshot, Balancer Protocol uses a Multisig to solidify these changes on-chain. Balancer’s Multisig signers are a diverse set of widely respected community members. The multisig does NOT have decision making power, as its role is to simply enact on-chain the decisions BAL holders make via off-chain voting.

## [Governable Protocol Fees](governable-protocol-fees.md)

Balancer Governors have the power to enable and modify Governable Protocol Fees. These can be collected from trading fees and flash loan fees and stored in the Vault. The Governors themselves also get to decide what becomes of these fees, and how to best spend them to support the health and progress of the protocol.

## Emergency subDAO

The [Emergency DAO](https://dao.curve.fi/emergencymembers) is an idea pioneered by Curve that empowers a small group to “kill” pools and gauges **in the** **event of malicious activity and/or potential loss of funds.** The Balancer emergency subDAO was established after the [following vote](https://vote.balancer.fi/#/proposal/0x63fab7ab9ef5b9579dabb82058b8ea309e39c766d435438b55fff8db7c1f69fd).&#x20;

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
