# Creating Distributions

## Creating Distributions&#x20;

Anyone can add their tokens to the `MerkleOrchard` to be claimed. We hope people use it to incentivize liquidity mining on pools of interest or use it as a general utility for distributing ERC20 tokens to any number of recipients!

Currently, the `MerkleOrchard` is used to distribute BAL and other tokens from a number of projects that incentivize pool liquidity on balancer.&#x20;

## How Merkle Trees Are Built&#x20;

Each distribution has a Merkle tree built from the `sha3(address, balance)` of each token recipient and the balance that they are due. The Merkle trees are built with [this library](https://github.com/balancer-labs/bal-mining-scripts/blob/master/js/src/merkle.ts).

Merkle trees for distributions of BAL and other tokens are computed, and published each week to [GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports).

* `_current*.json` files contain IPFS links to distributions that have been made available for liquidity mining on both the legacy Merkle redeem contracts, and the new Merkle orchard contracts. They contain the full details of accounts and balances.
* `_roots*.json` files contain the Merkle roots of the trees for each distributionId. These roots are stored in the MerkleRedeem and MerkleOrchard contracts to enable claims.

Projects that wish to use the `MerkleOrchard` to distribute tokens can build their own roots using the scripts above. To be added to the frontend, they should contact Balancer Labs to be added so that users can easily claim tokens. We also invite projects to build their own claim interfaces best suited to their needs.&#x20;

## Publishing a Merkle Root To The Contract&#x20;

#### To issue a distribution of tokens&#x20;

* Approve the number of tokens you will be distributing to the MerkleOrchard contract. The MerkleOrchard will pull the tokens it needs in the next step.&#x20;
*   Call `createDistribution` on the MerkleOrchard contract with the following args

    * `token` - erc20 token being distributed
    * `merkleRoot` - the root of the Merkle tree (generated in step 1)&#x20;
    * `amount` - the number of tokens (in wei) being distributed. While this is not strictly enforced, this should be the total of the balances in the tree to avoid running out of tokens&#x20;
    * `distributionId` - the id of the distribution. Generally this should start at 1 but an initial offset is allowed. Ids must be sequential in each distribution



    ### Instructions for teams providing dual incentives

    Teams that reach out to the Liquidity Mining Committee looking to provide incentives to Balancer pools can have their distributions computed within the context of the [BAL distributions](https://github.com/balancer-labs/bal-mining-scripts), in which case the merkle roots will have been computed an published [to GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports).&#x20;

    Teams are advised to use a Gnosis Safe to interact with the Merkle Orchard, so as to always seed the contract from the same address, thus reducing gas costs for recipients claiming their distributions.

    * [On GitHub](https://github.com/balancer-labs/bal-mining-scripts/tree/master/reports), find the JSON file that starts with `_roots` that corresponds to your token/network. For example, [`_roots-mcdex-arbitrum.json`](creating-distributions.md#overview)``

![](<../../.gitbook/assets/image (1) (1).png>)

* Take note of the number and the string in the last line of that file - in the example above, `3` and `0xd89432c5e6dcd7c05fd9a2b3ce6f004dfdf6f56fad540f7d63236817408ed1e9`
* Approve the number of tokens you will be distributing to the MerkleOrchard contract.
* Call `createDistribution` on the MerkleOrchard contract (see the [Addresses](creating-distributions.md#undefined) section) with the following args
  * `token` - the erc20 address of the token you'll distribute
  * `merkleRoot` - the last string in the `roots` JSON (in the example,&#x20;
    * `0xd89432c5e6dcd7c05fd9a2b3ce6f004dfdf6f56fad540f7d63236817408ed1e9)`
  * `amount` - the number of tokens (in wei) you'll distribute
  * `distributionId` - the last number in the `roots` JSON (in the example, `3`)
