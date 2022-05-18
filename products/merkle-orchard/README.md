---
cover: ../../.gitbook/assets/purple.png
coverY: 0
---

# Merkle Orchard

## Overview

Liquidity Mining distributions are available to claim weekly through the [`MerkleOrchard`](https://github.com/balancer-labs/balancer-v2-monorepo/blob/346ffdc995b709df2bd9e66f4e15ca22b2fc2c94/pkg/distributors/contracts/MerkleOrchard.sol) contract. Liquidity Providers can claim tokens from this contract by submitting claims to the tokens. These claims are checked against a Merkle root of the accrued token balances which are stored in a Merkle tree. Claiming through the MerkleOrchard is much more gas-efficient than the previous generation of claiming contracts, especially when claiming multiple weeks of rewards, and when claiming multiple tokens.&#x20;

A Merkle tree is a data structure that makes it easy to check data validity, in this case token balances. On each level of a balanced binary tree, elements are hashed together so it’s possible to verify that data exists in the tree by submitting hashes from leaf to root, a “Merkle Proof”.

### Claiming Tokens

{% content-ref url="claiming-tokens.md" %}
[claiming-tokens.md](claiming-tokens.md)
{% endcontent-ref %}

### Creating Distributions

{% content-ref url="creating-distributions.md" %}
[creating-distributions.md](creating-distributions.md)
{% endcontent-ref %}

## Addresses

| Network          | Address                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Ethereum Mainnet | [`0xdAE7e32ADc5d490a43cCba1f0c736033F2b4eFca`](https://etherscan.io/address/0xdAE7e32ADc5d490a43cCba1f0c736033F2b4eFca)``           |
| Polygon          | ``[`0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e`](https://polygonscan.com/address/0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e)``      |
| Arbitrum         | ``[`0x751A0bC0e3f75b38e01Cf25bFCE7fF36DE1C87DE`](https://arbiscan.io/address/0x751A0bC0e3f75b38e01Cf25bFCE7fF36DE1C87DE)``          |
| Kovan            | ``[`0xc33e0fE411322009947931c32d2273ee645cDb5B`](https://kovan.etherscan.io/address/0xc33e0fE411322009947931c32d2273ee645cDb5B)``   |
| Rinkeby          | ``[`0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e`](https://rinkeby.etherscan.io/address/0x0F3e0c4218b7b0108a3643cFe9D3ec0d4F57c54e)`` |
