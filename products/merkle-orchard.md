# Merkle Orchard

## Overview

Liquidity Mining distributions are available to claim weekly through the [`MerkleOrchard`](https://github.com/balancer-labs/balancer-v2-monorepo/blob/346ffdc995b709df2bd9e66f4e15ca22b2fc2c94/pkg/distributors/contracts/MerkleOrchard.sol) contract. Liquidity Providers can claim tokens from this contract by submitting claims to the tokens. These claims are checked against a Merkle root of the accrued token balances which are stored in a Merkle tree.

A Merkle tree is a data structure that makes it easy to check data validity, in this case token balances. On each level of a balanced binary tree, elements are hashed together so it’s possible to verify that data exists in the tree by submitting hashes from leaf to root, a “Merkle Proof”. 

## Claiming Tokens 

### From the app

LPs can claim tokens from the button on the top right of [app.balancer.fi](https://app.balancer.fi/#/).

![](<../.gitbook/assets/Screen Shot 2021-10-18 at 12.18.26 PM.png>) ![](<../.gitbook/assets/Screen Shot 2021-10-18 at 12.19.05 PM.png>)

Claiming is much more gas-efficient than the previous generation of claiming contracts, especially when claiming multiple weeks of distributions, and when claiming multiple tokens. Claiming from the contract directly

There are 3 functions that allow you to claim tokens from the MerkleOrchard.

* `claimDistributions`
* `claimDistributionsToInternalBalance` 
* `claimDistributionsToCallbackContract `

 The simplest of which, `claimDistributions`, takes the following arguments: 

* `claimer` - the address of the account claiming tokens) 
* `claims` - an array of the claim structs that describes the claim being made
  * `distributionId` - id of the distribution, generally starting at 1
  * `balance` - the number of tokens being claimed (in wei), as sourced from the [published distributions](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports) 
  * `distributor` - the address that added the tokens 
  * `tokenIndex` - the index of the token being claimed (index of the address in the `tokens` parameter) 
  * `merkleProof` - an array of hashes that prove the validity of the claim 
* `tokens` - an array of the set of all tokens being claimed, referenced by `tokenIndex`. Tokens can be in any order so long as they are indexed correctly

The contract also allows tokens to be claimed to callback contracts, enabling more powerful use cases, such as putting the tokens directly into liquidity pools. The Balancer community is highly encouraged to build custom interfaces that make this easy for users. Distributors - Creating distributions Anyone can add their tokens to the `MerkleOrchard` to be claimed. We hope people use it to incentivize liquidity mining on pools of interest or use it as a general utility for distributing ERC20 tokens to any number of recipients!

Currently, the `MerkleOrchard` is used to distribute BAL and other tokens from a number of projects that incentivize pool liquidity on balancer. How Merkle Trees are built Each distribution has a merkle tree built from the `sha3(address, balance)` of each token recipient and the balance that they are due. The merkle trees are built with this library: https://github.com/balancer-labs/bal-mining-scripts/blob/master/js/src/merkle.ts

Merkle trees for distributions of BAL and other tokens are computed, and published each week to https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports

`_current*.json` files contain ipfs links to distributions that have been made available for liquidity mining on both the legacy merkle redeem contracts, and the new merkle orchard contracts. They contain the full details of accounts and balances.

`_roots*.json` files contain the merkle roots of the trees for each distributionId. These roots are stored in the MerkleRedeem and MerkleOrchard contracts to enable claims.

Projects that wish to use the `MerkleOrchard` to distribute tokens can build their own roots using the scripts above. To be added to the frontend, they should contact Balancer Labs to be added so that users can easily claim tokens. We also invite projects to build their own claim interfaces best suited to their needs. Publishing a Merkle root to the contract To issue a distribution of tokens Approve the number of tokens you will be distributing to the MerkleOrchard contract. The MerkleOrchard will pull the tokens it needs in the next step. Call `createDistribution` on the MerkleOrchard contract with the following args

* token - ERC20 token being distributed
* merkleRoot - the root of the Merkle tree (generated in step 1) amount - the number of tokens (in wei) being distributed. While this is not strictly enforced, this should be the total of the balances in the tree to avoid running out of tokens distributionId - the id of the distribution. Generally this should start at 1 but an initial offset is allowed. Ids must be sequential in each distribution
