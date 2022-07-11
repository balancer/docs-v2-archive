# Claiming Tokens

## Claiming From The App

Users can claim tokens from the button on the top right of [app.balancer.fi,](https://app.balancer.fi/#/claim) [polygon.balancer.fi](https://polygon.balancer.fi/#/claim), and [arbitrum.balancer.fi](https://arbitrum.balancer.fi/#/claim).

![](<../../.gitbook/assets/Screen Shot 2021-10-18 at 12.18.26 PM.png>) ![](<../../.gitbook/assets/Screen Shot 2021-10-18 at 12.19.05 PM (1).png>)

## Claiming from the contract directly

There are 3 functions that allow you to claim tokens from the MerkleOrchard.

* `claimDistributions`
* `claimDistributionsToInternalBalance`&#x20;
* `claimDistributionsToCallbackContract`&#x20;

&#x20;The simplest of which, `claimDistributions`, takes the following arguments:&#x20;

* `claimer` - the address of the account claiming tokens)&#x20;
* `claims` - an array of the claim structs that describes the claim being made
  * `distributionId` - id of the distribution, generally starting at 1
  * `balance` - the number of tokens being claimed (in wei), as sourced from the [published distributions](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports)&#x20;
  * `distributor` - the address that added the tokens&#x20;
  * `tokenIndex` - the index of the token being claimed (index of the address in the `tokens` parameter)&#x20;
  * `merkleProof` - an array of hashes that prove the validity of the claim&#x20;
* `tokens` - an array of the set of all tokens being claimed, referenced by `tokenIndex`. Tokens can be in any order so long as they are indexed correctly.

The contract also allows tokens to be claimed to callback contracts, enabling more powerful use cases, such as putting the tokens directly into liquidity pools. The Balancer community is highly encouraged to build custom interfaces that make this easy for users.&#x20;
