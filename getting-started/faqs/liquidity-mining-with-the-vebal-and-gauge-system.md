# Liquidity Mining with the veBAL and Gauge System

## How does liquidity mining in the Gauge system work?

With the introduction of the tokenomics revamp to [veBAL](https://docs.balancer.fi/ecosystem/vebal-and-gauges/vebal) and the introduction of [gauges](https://docs.balancer.fi/ecosystem/vebal-and-gauges/gauges), the liquidity mining mechanics on Balancer changed drastically compared to the [legacy system](liquidity-mining.md#how-does-liquidity-mining-on-balancer-work). The new system involves staking of liquidity provider positions in the official gauges that are eligible to receive incentives.

You can see which pools receive liquidity mining incentives by the 3 star icon next to the pool position on [https://app.balancer.fi/#/](https://app.balancer.fi/#/) :&#x20;

![Example of a gauge receiving BAL incentives as well as other incentives as well as swap fees indicated on the tooltip when hovering over the 3 star symbol](<../../.gitbook/assets/image (1).png>)

## What does Min. BAL and Max. BAL APR mean?

{% hint style="info" %}
All APRs are extrapolated estimates based on recent data; they are not guaranteed.
{% endhint %}

With the introduction of the veBAL and gauge system, Balancer also introduced a boosting system on mainnet. This boosting system allows veBAL holders to increase their liquidity mining distributions on mainnet pools based on their locked veBAL and locked liquidity position.

* The Min. APR is the minimal APR a user can expect when staking any amount of liquidity in a gauge while not holding any veBAL
* The Max. APR is the max. theoretically achievable APR of 2.5x the Min. APR.

{% hint style="warning" %}
Please note that liquidity mining boosting is only available on Mainnet
{% endhint %}

If you want to better understand the relationship between the Min. and Max. APR boost and your liquidity position relative to your veBAL holdings, we recommend to consult the [community boosting calculator](https://balancer.tools/boost).

## How are Liquidity Mining Incentives distributed?

The gauge system introduced staking of LP positions. Therefore, rewards are calculated every block and can be claimed immediately through the [claim page](https://app.balancer.fi/#/claim). You can consult the [claim guide here](https://docs.balancer.fi/ecosystem/vebal-and-gauges/gauges/how-to-use-gauges#claiming-liquidity-mining-tokens).

## How are incentives directed to the Gauges?

The flow of incentives are now fully controlled by veBAL holders. Following rules apply

* A pool may receive liquidity mining only if it is eligible for voting. To be eligible to vote, a pool has to be allowlisted through a community proposal and vote
* Incentives for the running week have been voted upon on the previous week
* Voting epochs last between Thu-Thu 00:00 UTC.

## What do I have to be aware of when voting?

The voting system enables full control over how incentives are distributed; however, not all mechanisms are directly clear to the user. Please be aware of following mechanisms when voting:

* Voting involves a 10 day cool-down period
  * Changing a vote on a certain gauge also imposes a 10 day cooldown on that gauge
* If you increase your veBAL position, **make sure to revote** to fully register your newly acquired veBAL
* Additional rewards can be obtained by partaking in vote bribing like on the [Hidden Hand Market Place](https://hiddenhand.finance/balancer)
