# Batch Swaps

"Given In" means the caller knows the exact amount of the incoming token, and is asking the pool to calculate the tokenOut amount. The opposite is true of "Given Out." 

In these examples, we’re trading token A for token C, through the intermediate token B. A, B, and C token could be in different pools, or in the same pool.

The first case is a “Given In” Swap: say we have 10 A and want to know how much C we can get for it. We can accomplish this with a two-step multi-hop swap: A for B, then B for C.

Since we know the starting amount of A, the first swap is “Given In,” with an amount of 10.

The first swap will produce some amount of B, but we don’t know in advance how much. Since the amount of B **will** be known when the second swap executes, the second swap in the batch is also “Given In.”

Since we don’t know the amount of B when constructing the multi-hop, we initialize the amount in the second swap to 0, which instructs the multi-hop logic to use the calculated output amount from the first swap as input to the second.

| Parameter | Swap 1 | Swap 2 |
| :--- | :--- | :--- |
| Amount | 10 | 0 |
| Swap Kind | Given In | Given In |
| Tokens In/Out | A / B | B / C |

Say we get 5 B from the first swap. The amount of the second swap is then set to 5 in the Vault logic, and the second “Given In” swap produces some output amount of C. \(The caller would then validate the overall swap by comparing this value to the minimum amountOut of C.\)

The second case is a “Given Out” Swap: say we want 20 C, and want to know how much A that will cost. Here we need to do the swaps “backwards,” first trading C for B, then B for A.

The first swap is “Given Out,” and the amount is the desired amount of token C. It will produce some amount of token B, but as before, we don’t know how much in advance. So again we set the amount of the second swap to zero.

After the first swap, the amount of B will be known, and the zero amount in the second swap instructs the multi-hop logic to substitute the calculated amount from the last swap. Since this is “Given In,” the result will be some input amount of token A. \(The caller would then validate the overall swap by comparing this value to the maximum amountIn of A.\)

| Parameter | Swap 1 | Swap 2 |
| :--- | :--- | :--- |
| Amount | 20 | 0 |
| Swap Kind | Given Out | Given In |
| Tokens In/Out | B / C | B / A |

So in both cases, setting the amount of a swap within a batch to zero causes the multi-hop logic to substitute the calculated amount from the previous swap. If the previous swap was “Given In,” the calculated amount will be the “output” \(tokenOut\). If the previous swap was “Given Out,” the calculated amount will be the “input” \(tokenIn\).

Of course, the amount of the first swap in a batch cannot be zero.

