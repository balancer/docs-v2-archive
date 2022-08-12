# Calculating My Boost

To determine a user's boost their portion of staked liquidity in a pool as well as their share of total veBAL must be considered. First, a user's "non-boosted" and actual working supply are calculated as such:

$$
Non-boosted \ working  \ supply_{user} = 0.4*l
$$

* This equation assumes a user holds no veBAL

$$
working \ supply_{user}=min \bigg(0.4*l \ + \  0.6* L'* \frac{veBAL \ Held}{Total \ veBAL} \ , \ liquidity \ provided (l) \bigg)
$$

* This equation accounts for a user's veBAL holdings, while bounding boost between 1x and 2.5x

The boost a user receives is the the ratio of their working supply over the new total working supply, divided by the minimum case of their working supply entering a pool.

$$
Boost = \frac{\frac{working \ supply_{user}}{working \ supply_{user} + total \ working \ supply_{pool}}}{\frac{Non-boosted \ working \ supply_{user}}{Non-boosted \ working \ supply_{user} + total \ working \ supply_{pool}}}
$$

* The total working supply can be pulled from a pool's gauge contract or simulated.

In the case of already being in the pool and depositing further liquidity, further adjustments to the calculation must be considered.&#x20;
