# Composable Stable Pools Use Cases

### **The Lido wstETH/WETH Liquidity Pool**

[Lido](https://lido.fi/) is a liquid staking solution for ETH 2.0 backed by industry-leading staking providers. Lido lets users stake their ETH - without locking assets or maintaining their own infrastructure. The goal is to solve problems associated with initial ETH 2.0 staking: illiquidity, immovability and accessibility by making staked ETH liquid and allowing for participation with any amount of ETH to improve the security of the Ethereum network.

stETH is a token that represents **Staked Ether**, combining the value of deposited ETH with staking returns. As an ERC20, stETH tokens can be traded as one would swap WETH, allowing the benefits of ETH 2.0 staking rewards while allowing users to continue using their staked Ether on decentralized finance products.

Balancer Composable Stable Pools are ideal for the wstETH-WETH pair as the stETH asset is highly correlated but not pegged 1:1 to ETH as it accrues staking returns.

Note: To make stETH compatible with Balancer's streaming/rebasing tokens, stETH must be wrapped into wstETH. This is done through a relayer contract.

<figure><img src="../../../.gitbook/assets/Screenshot 2022-11-10 at 01.48.10.png" alt=""><figcaption></figcaption></figure>
