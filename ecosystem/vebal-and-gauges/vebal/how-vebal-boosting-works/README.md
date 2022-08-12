# How veBAL Boosting Works

As opposed to the initial liquidity mining incentives where a liquidity provider receives incentives based only on their share of the total liquidity, the veBAL system implements a multiplier based upon the time locking mechanism. Locking the same amount of BPT for a longer period will yield a higher incentive multiplier for a user.

Original Liquidity Mining:

$$
BAL \ Mined \ = \ Pool's \ Total \ Incentives \ * \frac{BPT \ Held}{Total \ BPT}
$$

veBAL Liquidity Mining:

$$
\\ \\\ \\ BAL \ Mined \ = \ Pool's \ Total \ Incenvites \ * \ \frac{0.4 \ * \ BPT \ Staked \ * \ Boost}{Total \ Working \ Supply}
$$

Please note the maximum boost possible for liquidity mining incentives is 2.5x. For tooling, calculate your boost [here.](https://balancer.tools/boost)

The boosting mechanism theory is visualized by the graphic below. The fraction of a pool's working supply a user owns is based on upon their share of the respective pool, and their share of total veBAL. Continue reading through this boosting sections for further information on the [working supply.](working-supply.md)

​

![View Graphic Equations here](<../../../../.gitbook/assets/Boosting graphic.gif>) ![](<../../../../.gitbook/assets/Boosting graphic legend.png>)

Based upon this mechanism locking the same number of tokens for twice as long will result in twice the veBAL a user receives. The boosting proportion and governance voting are directly coupled with veBAL, however only governance is directly proportional.
