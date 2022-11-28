# Governable Protocol Fees

## Overview

Governable Protocol Fees are fees collected by the Balancer Protocol, **not** Liquidity Providers. There are a few ways in which the fees can be collected, and far more in which they can be used. Though many Liquidity Providers may also be Balancer Governors, we will discuss them here as distinct groups for clarity.&#x20;

## Sources

### Swap Fees

The obvious source of Protocol Fees are the swaps. Balancer swappers already pay swap fees to Liquidity Providers in exchange for making their swap possible. Fees are denominated in the Input Token when executing a swap.&#x20;

The Protocol Fees for swaps can be collected as a percentage of the swap fees already being collected (a fraction of a fraction). From the swapper's perspective, there will be no price increase.&#x20;

Upon launch, Balancer V2's **Protocol Fees for trades are turned off by default**. They can be turned on only by a vote of the Balancer Governors (BAL token holders). The governors have the power to activate and determine the amount of these fees.

### Flash Loan Fees (currently set to 0)

Another source of Protocol Fees is represented by interest on [Flash Loans](../../concepts/features/flash-loans.md). Any fees collected as interest on flash loans go to the DAO Treasury. However, at deployment **flash loans fees were set to zero**, and at the time of writing, they have still not been activated by the governance.

## Protocol Fee Percentages Provider

The Protocol Fee Percentages Provider contract provides a convenient way to access Protocol Fee percentages (i.e.:how much the protocol charges for performing certain actions).

| Network                                                                                                                                                                                                                      | Address                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Ethereum Mainnet                                                                                                                                                                                                             | [0x97207B095e4D5C9a6e4cfbfcd2C3358E03B90c4A](https://etherscan.io/address/0x97207b095e4d5c9a6e4cfbfcd2c3358e03b90c4a#code)            |
| Polygon Mainnet                                                                                                                                                                                                              | [0x42AC0e6FA47385D55Aff070d79eF0079868C48a6](https://polygonscan.com/address/0x42AC0e6FA47385D55Aff070d79eF0079868C48a6#code)         |
| Arbitrum Mainnet                                                                                                                                                                                                             | [0x5ef4c5352882b10893b70DbcaA0C000965bd23c5](https://arbiscan.io/address/0x5ef4c5352882b10893b70dbcaa0c000965bd23c5#code)             |
| Ortimism Mainnet                                                                                                                                                                                                             | [0xacAaC3e6D6Df918Bf3c809DFC7d42de0e4a72d4C](https://optimistic.etherscan.io/address/0xacaac3e6d6df918bf3c809dfc7d42de0e4a72d4c#code) |
| [Protocol Fee Percentage Provider artifact](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/deployments/tasks/20220725-protocol-fee-percentages-provider/artifact/ProtocolFeePercentagesProvider.json) |                                                                                                                                       |

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
