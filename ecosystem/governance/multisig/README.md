# Multisig

## Overview

First of all, a very important point: **the multisig does not have decision making power**, as its role is to simply enact on-chain the decisions BAL holders make via off-chain voting.

It is deployed using [Gnosis Safe](https://gnosis-safe.io/), the most battle-tested multisig contract on Ethereum. Its n-of-m configuration will start as 6-of-11 on Ethereum mainnet, 3-of-5 on Polygon and Arbitrum. Both parameters n and m may evolve and are ultimately defined by BAL holders with protocol security in mind.

Balancer’s multisig signers are a diverse set of widely respected community members. Balancer V2 contracts allow for some tweaking of core protocol parameters, for instance, in setting protocol fees. As a placeholder for a future on-chain DAO, limited admin powers has been initially granted to a Multisig.

## Multisig Powers

Balancer V2 smart contracts can grant some specific powers to an `admin` address, which will initially point to the multisig’s address.

These powers are:

* set protocol swap fee (maximum value 50%)
* set a flash loan fee
* extract from the vault collected protocol fees and/or excess balances (e.g. airdrops), to any destination
* set the address of the oracle implementation
* pause/resume swaps on all pools before a 4-month-after-launch deadline, after which Balancer V2 becomes unstoppable
* set relayer addresses: relayers are (user opt-in, audited) contracts that can make calls to the vault (with the transaction “sender” being any arbitrary address) and use the sender’s ERC20 vault allowance, internal balance or BPTs on their behalf
* set dynamic-fee controllers: addresses (initially assigned to Gauntlet) that may change the swap fee for pools created by the dynamic-fee pool factory that will be deployed by Balancer Labs

It’s worth highlighting that the multisig does **not** have custody of (nor control over) funds from liquidity providers that lie inside Balancer Protocol contracts. Balancer V2 was designed so that even if the multisig goes rogue, all the liquidity is safe and can be withdrawn by their rightful owners.

## Multisigs

{% tabs %}
{% tab title="Ethereum" %}
## Address

[0x10A19e7eE7d7F8a52822f6817de8ea18204F2e4f](https://etherscan.io/address/0x10A19e7eE7d7F8a52822f6817de8ea18204F2e4f)

## Signers

* [Alexander Lange](https://twitter.com/AlexLangeVC) (Inflection)
* [Ernesto](https://mobile.twitter.com/eboadom) (Bored Ghosts Developing)
* [Solarcurve](https://twitter.com/0xsolarcurve) (Baller)
* [Fabien](https://twitter.com/bonustrack87) (Snapshot Labs)
* [David Garai](https://twitter.com/davgarai) (Tempus)
* [Kain Warwick](https://twitter.com/kaiynne) (Synthetix)
* [Evan](https://twitter.com/sausage\_crypto) (Copper Launch)
* [Mariano Conti](https://twitter.com/nanexcool) (Ethereum)
* [Stefan](https://twitter.com/StefanDGeorge) (Gnosis)
* [Trent McConaghy](https://twitter.com/trentmc0) (Ocean Protocol)
* [0xMaki](https://twitter.com/0xMaki)
{% endtab %}

{% tab title="Polygon" %}
## Address

[0xd2bD536ADB0198f74D5f4f2Bd4Fe68Bae1e1Ba80](https://polygonscan.com/address/0xd2bD536ADB0198f74D5f4f2Bd4Fe68Bae1e1Ba80)

## Signers

* [fabien](https://twitter.com/bonustrack87) (Snapshot Labs)
* [solarcurve](https://twitter.com/0xsolarcurve) (Baller)
* [bakamoto](https://twitter.com/bakamoto20) (Baller, Liquidity Mining Committee)
* jnapier (Baller)
* [Xeonus](https://twitter.com/Xeonusify) (Baller)
* [Mike B](https://twitter.com/DefiGod5) (Baller)
* [zekraken](https://twitter.com/The\_Krake) (Baller)
{% endtab %}

{% tab title="Arbitrum" %}
## Address

[0x6207ed574152496c9B072C24FD87cE9cd9E17320](https://arbiscan.io/address/0x6207ed574152496c9B072C24FD87cE9cd9E17320)

## Signers

* [fabien](https://twitter.com/bonustrack87) (Snapshot Labs)
* [solarcurve](https://twitter.com/0xsolarcurve) (Baller)
* [bakamoto](https://twitter.com/bakamoto20) (Baller, Liquidity Mining Committee)
* jnapier (Baller)
* [Xeonus](https://twitter.com/Xeonusify) (Baller)
* [Mike B](https://twitter.com/DefiGod5) (Baller)
* [zekraken](https://twitter.com/The\_Krake) (Baller)
{% endtab %}
{% endtabs %}



## Context

Since its inception, the long term vision for the Balancer Protocol is to be fully governed by BAL token holders, while token ownership is aimed to be widely spread across the Balancer community.

But getting to that ideal, long-term vision of a truly decentralized and effective governance is no easy task. Protocol governance is a highly complex and rapidly evolving topic. The whole crypto ecosystem is still in the very early days of trying to figure out:

* which mechanisms and processes work best
* the necessary infrastructure, tooling, and user interfaces
* the risks and concerns associated with each approach

Experimentation has been running wild in all directions:

* vote delegation
* minimum quorum
* specialized committees
* continuous voting
* augmented voting power via token lock
* off-chain voting for signaling / polling
* on-chain actions from off-chain voting by way of oracles
* upgradeable smart contracts
* time delays on sensitive actions
* emergency actions via Multisig (e.g. pause, shutdown)
* legal entities (e.g. foundation) providing support for the DAO
* tools for DAO treasury management
* token issuance to cover protocol expenses
* incentivized voting
* incentivized off-chain engagement (e.g. forum participation)
* and so on…

While also actively experimenting with governance-related initiatives, the Balancer community has leaned towards the more cautious and thoughtful approach of not trying to rush the path to full decentralization, so each step towards a mature on-chain governance will be taken with due care, having learned from others’ experiences.

## Signer Duties

All signers are expected to create an Ethereum transaction ratifying each decision made by BAL holders through Snapshot votes. This signature is expected to be done within the two weeks after the snapshot vote was concluded. Even after quorum is reached (by n signers), the remaining signers are also expected to sign before a multisig action is executed. This procedure aims to regularly confirm each signers’ conformity to the off-chain votes and also to serve as recent proof of their ability to sign.

A signer shall lose his/her role (by action of the remaining multisig signers excluding him/her) in case he/she:

* acts against BAL token holders’ off-chain voting;
* goes through 3 months or 2 votes (whichever takes longer) without performing any of their signer duties.

## Future Signer Short-List

Beyond the current signers, the community should strive to keep a short, ordered list of potential signers in order to make any eventual signer substitution as smooth and timely as possible.

During its lifecycle, the operation of the multisig is expected to gradually evolve towards requiring less and less trust, for instance by using [SafeSnap](https://blog.gnosis.pm/introducing-safesnap-the-first-in-a-decentralized-governance-tool-suite-for-the-gnosis-safe-ea67eb95c34f) (which binds the results from Snapshot off-chain BAL voting to on-chain execution with the help of [Reality.eth](https://reality.eth.link/) oracles). Balancer has been an early supporter of SafeSnap.

In the long run, BAL holders are expected to retire the multisig in favor of a full-fledged Balancer DAO.
