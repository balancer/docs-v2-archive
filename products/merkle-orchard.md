# Merkle Orchard

## Overview

Liquidity Mining distributions are available to claim weekly through the [`MerkleOrchard`](https://github.com/balancer-labs/balancer-v2-monorepo/blob/346ffdc995b709df2bd9e66f4e15ca22b2fc2c94/pkg/distributors/contracts/MerkleOrchard.sol) contract. Liquidity Providers can claim tokens from this contract by submitting claims to the tokens. These claims are checked against a Merkle root of the accrued token balances which are stored in a Merkle tree. Claiming through the MerkleOrchard is much more gas-efficient than the previous generation of claiming contracts, especially when claiming multiple weeks of rewards, and when claiming multiple tokens.&#x20;

A Merkle tree is a data structure that makes it easy to check data validity, in this case token balances. On each level of a balanced binary tree, elements are hashed together so it’s possible to verify that data exists in the tree by submitting hashes from leaf to root, a “Merkle Proof”.&#x20;

## Addresses

| Network          | Address                                      |
| ---------------- | -------------------------------------------- |
| Ethereum Mainnet | `0xdAE7e32ADc5d490a43cCba1f0c736033F2b4eFca` |
| Polygon          | `0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e` |
| Arbitrum         | `0x751A0bC0e3f75b38e01Cf25bFCE7fF36DE1C87DE` |
| Kovan            | `0xc33e0fE411322009947931c32d2273ee645cDb5B` |
| Rinkeby          | `0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e` |

## Claiming Tokens&#x20;

### Claiming From The App

Users can claim tokens from the button on the top right of [app.balancer.fi](https://app.balancer.fi/#/).

![](<../.gitbook/assets/Screen Shot 2021-10-18 at 12.18.26 PM (1).png>) ![](<../.gitbook/assets/Screen Shot 2021-10-18 at 12.19.05 PM (2).png>)

### Claiming from the contract directly

There are 3 functions that allow you to claim tokens from the MerkleOrchard.

* `claimDistributions`
* `claimDistributionsToInternalBalance`&#x20;
* `claimDistributionsToCallbackContract `

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

## Distributors

### Creating Distributions&#x20;

Anyone can add their tokens to the `MerkleOrchard` to be claimed. We hope people use it to incentivize liquidity mining on pools of interest or use it as a general utility for distributing ERC20 tokens to any number of recipients!

Currently, the `MerkleOrchard` is used to distribute BAL and other tokens from a number of projects that incentivize pool liquidity on balancer.&#x20;

### How Merkle Trees Are Built&#x20;

Each distribution has a Merkle tree built from the `sha3(address, balance)` of each token recipient and the balance that they are due. The Merkle trees are built with [this library](https://github.com/balancer-labs/bal-mining-scripts/blob/master/js/src/merkle.ts).

Merkle trees for distributions of BAL and other tokens are computed, and published each week to [GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports).

* `_current*.json` files contain IPFS links to distributions that have been made available for liquidity mining on both the legacy Merkle redeem contracts, and the new Merkle orchard contracts. They contain the full details of accounts and balances.
* `_roots*.json` files contain the Merkle roots of the trees for each distributionId. These roots are stored in the MerkleRedeem and MerkleOrchard contracts to enable claims.

Projects that wish to use the `MerkleOrchard` to distribute tokens can build their own roots using the scripts above. To be added to the frontend, they should contact Balancer Labs to be added so that users can easily claim tokens. We also invite projects to build their own claim interfaces best suited to their needs.&#x20;

### Publishing a Merkle Root To The Contract&#x20;

#### To issue a distribution of tokens&#x20;

* Approve the number of tokens you will be distributing to the MerkleOrchard contract. The MerkleOrchard will pull the tokens it needs in the next step.&#x20;
* Call `createDistribution` on the MerkleOrchard contract with the following args
  * `token` - erc20 token being distributed
  * `merkleRoot` - the root of the Merkle tree (generated in step 1)&#x20;
  * `amount` - the number of tokens (in wei) being distributed. While this is not strictly enforced, this should be the total of the balances in the tree to avoid running out of tokens&#x20;
  * `distributionId` - the id of the distribution. Generally this should start at 1 but an initial offset is allowed. Ids must be sequential in each distribution

### Instructions for teams providing dual incentives

Teams that reach out to the Liquidity Mining Committee looking to provide incentives to Balancer pools can have their distributions computed within the context of the [BAL distributions](https://github.com/balancer-labs/bal-mining-scripts), in which case the merkle roots will have been computed an published [to GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports).&#x20;

* [On GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports), find the JSON file that starts with `_roots` that corresponds to your token/network. For example, [`_roots-mcdex-arbitrum.json`](merkle-orchard.md#overview)``

![](<../.gitbook/assets/image (7).png>)

* Take note of the number and the string in the last line of that file - in the example above, `3` and `0xd89432c5e6dcd7c05fd9a2b3ce6f004dfdf6f56fad540f7d63236817408ed1e9`
* Approve the number of tokens you will be distributing to the MerkleOrchard contract.
* Call `createDistribution` on the MerkleOrchard contract (see the [Addresses](merkle-orchard.md#undefined) section) with the following args
  * `token` - the erc20 address of the token you'll distribute
  * `merkleRoot` - the last string in the `roots` JSON (in the example,&#x20;
    * `0xd89432c5e6dcd7c05fd9a2b3ce6f004dfdf6f56fad540f7d63236817408ed1e9)`
  * `amount` - the number of tokens (in wei) you'll distribute
  * `distributionId` - the last number in the `roots` JSON (in the example, `3`)
