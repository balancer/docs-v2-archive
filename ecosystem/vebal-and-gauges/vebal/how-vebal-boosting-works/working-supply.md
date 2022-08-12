# Working Supply

The variables to consider when calculating working supply and veBAL incentives boosting are the following:

* The Liquidity you will provide and stake: l
* The staked liquidity in the pool before you deposit and stake: L
* The liquidity in the pool after your deposit and stake: L' = L + l
* The total veBAL in circulation
* The amount of veBAL you hold

The liquidity in terms of how much veBAL correlates to it what is called a _**working supply**_. The _**working supply**_ can range from 40% to 100% of a user’s staked liquidity position. This is the main theory behind how incentives are boosted and distributed. The equation below defines a user’s working supply. (see variable list [here](minimum-vebal-for-max-boost.md))

If a user owns no veBAL use the following equation:

$$
Non-boosted \ working \ supply_{user} \ = \ 0.4 \ * \ l
$$

Actual working supply adds the veBAL dependent term for 60% of incentives boosting to become available.

$$
working \ supply_{user} = min \bigg(0.4  *  l \ + \ 0.6*L' * \frac{veBAL \ Held}{Total \ veBAL} \ , \ liquidity \ provided \ (l) \bigg)
$$

* The minimum function ensures a user cannot receive a boost over 2.5x

The maximum working supply possible is defined as the following:

$$
max \ working \ supply_{user} = 0.4*l +0.6 * L'*\frac{min \ veBAL_{max \ boost}}{Total \ veBAL}
$$

* Please note a users working supply will not impact the pools total working supply beyond this point.
