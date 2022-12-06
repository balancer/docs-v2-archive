# Governable Protocol Fees

## Overview

Governable Protocol Fees are fees collected by the Balancer Protocol, **not** Liquidity Providers. There are a few ways in which the fees can be collected, and far more in which they can be used. Though many Liquidity Providers may also be Balancer Governors, we will discuss them here as distinct groups for clarity.&#x20;

## Sources

### Swap Fees

The obvious source of Protocol Fees are the swaps. Balancer swappers already pay swap fees to Liquidity Providers in exchange for making their swap possible. Fees are denominated in the Input Token when executing a swap.&#x20;

The Protocol Fees for swaps can be collected as a percentage of the swap fees already being collected (a fraction of a fraction). From the swapper's perspective, there will be no price increase.&#x20;

Upon launch, Balancer V2's **Protocol Fees for trades are turned off by default**. They can be turned on only by a vote of the Balancer Governors (BAL token holders). The governors have the power to activate and determine the amount of these fees.

### Flash Loan Fees (currently set to 0)

Another source of Protocol Fees is represented by interest on [Flash Loans](../../products/the-vault/flash-loans.md). Any fees collected as interest on flash loans go to the DAO Treasury. However, at deployment **flash loans fees were set to zero**, and at the time of writing, **they have still not been activated by the governance.**

## Protocol Fees

Once integrators start paying fees themselves, it is expected that they start paying protocol fees to the Balancer DAO. However, the 50% protocol fee on swaps and yield is not mandatory. There is no need to pay Balancer DAO any fee while your project is in its early stages. You decide when to turn fees on, how to charge a fee, and can work with Balancer to determine what split makes sense. \
The payment of protocol fees comes with some important advantages:

* Active support by the various service providers in the Balancer ecosystem in areas like Software development, Marketing, biz-dev etc.
* Inclusion in the Balancer SDK, SOR (Smart Order Router) and Balancer Subgraph, making the integrator’s liquidity visible to all existing consumers of the SDK/SOR/subgraph.
* Streamlined integration with leading liquidity aggregators like 1Inch, CowSwap, 0x and ParaSwap.&#x20;

The [ProtocolFeePercentagesProvider](https://github.com/balancer-labs/balancer-v2-monorepo/blob/faff088615a09f0a2fc52b904d58ca4aa5ae0566/pkg/interfaces/contracts/standalone-utils/IProtocolFeePercentagesProvider.sol) should be used as the ground truth to determine the protocol fee percentages to be paid by integrators.

### Protocol Fee Percentages Provider

The Protocol Fee Percentages Provider contract provides a convenient way to access Protocol Fee percentages (i.e.:how much the protocol charges for performing certain actions).

| Network                                                                                                                                                                                                                      | Address                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Ethereum Mainnet                                                                                                                                                                                                             | [0x97207B095e4D5C9a6e4cfbfcd2C3358E03B90c4A](https://etherscan.io/address/0x97207b095e4d5c9a6e4cfbfcd2c3358e03b90c4a#code)            |
| Polygon Mainnet                                                                                                                                                                                                              | [0x42AC0e6FA47385D55Aff070d79eF0079868C48a6](https://polygonscan.com/address/0x42AC0e6FA47385D55Aff070d79eF0079868C48a6#code)         |
| Arbitrum Mainnet                                                                                                                                                                                                             | [0x5ef4c5352882b10893b70DbcaA0C000965bd23c5](https://arbiscan.io/address/0x5ef4c5352882b10893b70dbcaa0c000965bd23c5#code)             |
| Ortimism Mainnet                                                                                                                                                                                                             | [0xacAaC3e6D6Df918Bf3c809DFC7d42de0e4a72d4C](https://optimistic.etherscan.io/address/0xacaac3e6d6df918bf3c809dfc7d42de0e4a72d4c#code) |
| [Protocol Fee Percentage Provider artifact](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/deployments/tasks/20220725-protocol-fee-percentages-provider/artifact/ProtocolFeePercentagesProvider.json) |                                                                                                                                       |

{% hint style="info" %}
More details about Protocol Fees can be found in [BIP77.](https://forum.balancer.fi/t/bip-77-friendly-balancer-protocol-fees-for-integrators/3732)
{% endhint %}

## Uses

Protocol Fees are to be used according to proposals and votes by the Balancer Governors. There are endless possibilities for what the Balancer Protocol could do with these fees, some of which may not even exist yet. This list of example uses is not meant to be recommendations for what to do with them, but is instead meant to start the conversation on how to use this incredible power.

We invite you to join our Discord and Forums to take part in the discussion over how to use these fees.

#### Possible uses of Balancer Protocol Fees

* Put them into a Balancer Pool
* Fund Gitcoin Grants for protocol improvements
* Fund advertising campaigns
* Fund grants to attract strategic partnerships
* Buy a decentralized insurance policy
* Lend them on an external protocol
* Pay them directly to Balancer Governors
* Fund Service Providers (SPs) under the [Operating Framework for Balancer DAO](https://forum.balancer.fi/t/bip-1-operating-framework-for-balancer-dao/3237)
