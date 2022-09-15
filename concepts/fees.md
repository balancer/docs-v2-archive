# Fees

## Overview

There are a few different types of fees on Balancer, each collected to support a healthy ecosystem. For example, Liquidity Providers collect swap fees as users trade with pools; this acts as an incentive for them to continue providing liquidity, which is useful to facilitate trades.&#x20;

## Swap Fees

Traders pay swap fees when they trade with a pool. For pools that inherit from BasePool, these fees can be customized with a minimum value of 0.0001% and a maximum value of 10%.&#x20;

The fees ultimately go to Liquidity Providers in exchange for them putting their tokens in the pool to facilitate trades. Trade fees are collected at the time of a swap, and it goes directly into the pool, growing the pool's balance. For a trade with a given $$inputToken$$ and $$outputToken$$, the amount collected by the pool as a fee is $$Amount_{fee} = Amount_{inputToken} * swapFee$$. As the pool collects fees, **Balancer Pool Tokens automatically collect fees** because they represent a **proportional share of the pool.**&#x20;

### Example

Let's say Alice, Bob, Chuck, and Diana all provide liquidity in the same pool starting out with a total value of $100. After some time, the pool has collected many trade fees and is now worth $200. The pool itself grows while the Liquidity Providers' proportional shares stay the same.

| Person | Proportional Share  | Initial Value | Value After Trading |
| ------ | ------------------- | ------------- | ------------------- |
| Alice  | 50.0%               | $50           | $100                |
| Bob    | 25.0%               | $25           | $50                 |
| Chuck  | 12.5%               | $12.50        | $25                 |
| Diana  | 12.5%               | $12.50        | $25                 |

![](<../.gitbook/assets/Screen Shot 2021-08-12 at 10.10.06 AM.png>)

### Static and Dynamic Fees

At the time of pool creation, the pool creator defines the **fee** and the **owner**. If the owner is set to an uncontrolled address (typically the zero address) then the swap fee is **static**. If the owner sets it to a controlled address, that address can set the fee at will, therefore making the swap fee **dynamic**.

There are two different ways that a pool can have **Dynamic Fees**, either the pool owner manually sets fees, or the pool creator delegates fees to a governance-approved controller by setting the pool owner to the `delegate` address.

[Governance approved Gauntlet](https://vote.balancer.fi/#/proposal/QmZZycpDWZYAzNho6uVaWL5nFpVzauc89HC9d5QNTSn18J) to have **Delegated Fee Control** on many pool types. They have been updating fees regularly based on models designed to optimize fee volume to Liquidity Providers. To learn more about how they determine fees, check out [their Medium post](https://medium.com/gauntlet-networks/balancer-v2-pools-trading-fee-methodology-7a65df671b8c).

### Protocol Swap Fees

Protocol Swap Fees are a percentage of swap fees collected by pools. These go to the DAO Treasury to be used or held as the DAO sees fit. At deployment, Protocol Fees for swaps were set to 0%. These fees were activated by [a governance vote](https://vote.balancer.fi/#/proposal/0xf6238d70f45f4dacfc39dd6c2d15d2505339b487bbfe014457eba1d7e4d603e3) and were later raised to 50% by [a subsequent proposal](https://vote.balancer.fi/#/proposal/0x03e64d35e21467841bab4847437d4064a8e4f42192ce6598d2d66770e5c51ace). For the most up-to-date protocol fee data, please call `getSwapFeePercentage()` on [the `ProtocolFeesCollector` contract](https://etherscan.io/address/0xce88686553686DA562CE7Cea497CE749DA109f9F#readContract).

Protocol Swap Fees are a percent of the already collected swap fees; the traders would see no change in the amount collected. The Liquidity Providers, however, would see a small change. For example, if a pool has a 1% swap fee, and there was a 10% protocol swap fee, 0.9% of each trade would be collected for the LPs, and 0.1% would be collected to the protocol fee collector contract.

## **Flash Loan Fees**

Flash Loan fees are a type of Protocol Fee on Balancer. The fees collected as interest on flash loans go to the DAO Treasury. At deployment, flash loan fees were set to zero, and as of this writing they have not been activated by governance.
