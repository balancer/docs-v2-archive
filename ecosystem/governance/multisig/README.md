# Multisig

## Overview

First of all, a very important point: **the multisig does not have decision making power**, as its role is to simply enact on-chain the decisions BAL holders make via off-chain voting.

It is deployed using [Gnosis Safe](https://gnosis-safe.io/), the most battle-tested multisig contract on Ethereum. Its n-of-m configuration will start as 6-of-11 on Ethereum mainnet, 3-of-5 on Polygon and Arbitrum. Both parameters n and m may evolve and are ultimately defined by BAL holders with protocol security in mind.

Balancer’s multisig signers are a diverse set of widely respected community members. Balancer V2 contracts allow for some tweaking of core protocol parameters, for instance, in setting protocol fees. As a placeholder for a future on-chain DAO, limited admin powers has been initially granted to a Multisig.

## Multisig Powers

Balancer V2 smart contracts can grant some specific powers to an `admin` address, which will initially point to the multisig’s address.

These powers are:

* grant roles in the Authorizer
* set protocol swap fee (maximum value 50%)
* set a flash loan fee
* extract collected protocol fees and/or excess balances (e.g. airdrops), from the Vault to any destination&#x20;
* set the address of the oracle implementation
* pause/resume swaps on all pools before a 4-month-after-launch deadline, after which Balancer V2 becomes unstoppable
* set relayer addresses: relayers are (user opt-in, audited) contracts that can make calls to the vault (with the transaction “sender” being any arbitrary address) and use the sender’s ERC20 vault allowance, internal balance or BPTs on their behalf
* set dynamic-fee controllers: addresses that may change the swap fee for pools created by the dynamic-fee pool factory that will be deployed by Balancer Labs

It’s worth highlighting that the multisig does **not** have custody of (nor control over) funds from liquidity providers that lie inside Balancer Protocol contracts. Balancer V2 was designed so that even if the multisig goes rogue, all the liquidity is safe and can be withdrawn by their rightful owners.

## Future Signer Short-List

Beyond the current signers, the community shall keep a short, ordered list of potential signers in order to make any eventual signer substitution as smooth and timely as possible.

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



## Future Signer Short-List

{% hint style="info" %}
Every so often, multisig signers are rotated out if they request to leave the multisig or do not fulfill their [Signer Duties](./#signer-duties). This is a list of replacement candidates should current signers be removed.
{% endhint %}

* Evgeny Yurtaev, CEO at Zerion (0xcec0d1a31129af0b1088a3d8dfa6abb4bd1ecb45)
* Lewis, Stablecoin Labs / Gyroscope (0xbcf751dBfe314Ee96A660EFA2Fcb259CBc364c29)
* Mounir, Paraswap (0x0951ff0835302929d6c0162b3d2495a85e38ec3a)
* Anna, Cowswap (0x04ce1ccF81AE660e23ca0c0823911df709B0E7Fc)
* Kaito, Utopia Labs (0x01eacADF51FF60916157E32A58F640fe854e530F)
* Mr. Kind, BeethovenX (0xD876847533828bE6770D1dEdB6F8f5E91fed824e)
* Hubert, StakeDAO (0x28827186555d99d9eF9E1fdB97F65C93BA554F86)
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

{% tab title="Optimism" %}
## Address

[0x043f9687842771b3dF8852c1E9801DCAeED3f6bc](https://optimistic.etherscan.io/address/0x043f9687842771b3dF8852c1E9801DCAeED3f6bc)

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

## Relevant  Votes

The below Snapshot votes are instances of multisig or shortlist signers

* [Vote #1](https://snapshot.org/#/balancer.eth/proposal/0xadd41023d90e4e66bc1af834f7a3951b7c6171388d24f3779afed4ca9ad75a9e)
* [Vote #2 ](https://snapshot.org/#/balancer.eth/proposal/0xbd025f8f5a0b1d748a8ad034f5a2b6fd50cc8ff7257cbee6b8344b2a70e9e2ed)
* [Vote #3 ](https://snapshot.org/#/balancer.eth/proposal/0x9614c890099947b96d36cee4f6d64e649fe41bdd66331d1d93b39ed952c4ffcd)
