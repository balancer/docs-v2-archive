# Pool Creation

There will eventually be a pool creation UI, but for now the focus is on [migrating liquidity](../../getting-started/faqs/v1-to-v2-migration.md), and reducing fragmentation by concentrating liquidity in a smaller number of large pools, vs a large number of small pools.

Toward this end, since the majority of liquidity \(and all the "seed" pools\) are two-token pools, the migration UI only supports migrating two-token V1 pools to corresponding \(or every close\) seed pools on V2. Furthermore, liquidity mining on V2 will be focused on pools chosen by governance, vs just any pool with whitelisted tokens.

Nevertheless, we need breadth as well as depth, and core pools still support up to 8 tokens. The V2 Vault architecture makes fragmentation and support for lower-cap tokens less costly overall, since it performs multi-hop swaps without needing to transfer tokens between pools. \(With User balance, it's even possible to avoid token transfers altogether.\) So if you do wish to create V2 pools, here's how to do it.

{% hint style="warning" %}
The Vault and core pool factories are currently within the "emergency period," during which they are pausable in the event of a security incident. After this period expires \(in July\), the Vault and WeightedPools will become trustless. Because they were deployed after launch, WeightedPool2Token \(Oracle\) pools will remain pausable for an additional two weeks.

Any new pool types should also follow this pattern. When Stable Pools are released, they will likewise be pausable during the first three months after deployment.

If the Vault or a pool is paused, all operations are blocked except withdrawals.
{% endhint %}

#### So you want to deploy a pool...

The first question is, which pool? There are two:

* **WeightedPool -** V1-like pool with up to 8 tokens
* **WeightedPool2Tokens** - 2-token pool with V1 math, and support for resilient oracles

If you need more than two tokens, WeightedPool is the only option. If you have a two-token pool, we recommend the oracle pool. Pool operations are slightly more expensive with the oracle turned on \(especially the first 1k swaps, until the oracle is fully initialized\), so you might deploy it with the oracle off initially, then turn it on later. \(Note that it cannot be turned off again.\)

The high liquidity "seed" pools on Balancer all have the oracle enabled: they are intended to serve as the "official" oracles for those pairs. Eventually the plan is to have a registry of oracle pools, controlled by governance. So a newly launched token could create an oracle pool on Balancer \(perhaps paired with WETH or DAI\), with the oracle on. Given high enough liquidity, and volume sufficient to fully initialize the oracle, the pool could then apply to governance to be included in the registry.

Before creating a new pool, make sure there isn't already a similar pool! There's no advantage to fragmenting liquidity - especially on V2, where liquidity mining is per pool, with the pools chosen by governance \(i.e., "duplicate" pools would not be approved for mining incentives\).

The next question is how you want to handle swap fees. As in V1, pool swap fees can range from 0.0001% to 10%. In V2, there are three options:

* Fixed fees
* Owner-controlled fees \(like V1 smart pools with the changeSwapFee right enabled\)
* Dynamic fees \(initially fixed, but can be actively managed by Gauntlet per governance vote\)

You can theoretically create pools through Etherscan or MEW, but the complex arguments required make this very difficult. It's best to use a script. This tutorial uses hardhat and ethers; modify according if you're in JS, Buidler, Truffle, etc. \(At some point soon there will be package support to make importing abi/artifacts easier than it currently is, including with helper functions, etc.\)

First, let's define some addresses we'll need: the Vault, the two currently available factories, and the special "delegate owner" address used to allow a governance-appointed third party \(currently Gauntlet\) to control swap fees.

```text
// Addresses are the same on all networks

const VAULT = '0xBA12222222228d8Ba445958a75a0704d566BF2C8';

const WEIGHTED_POOL_FACTORY = '0x8E9aa87E45e92bad84D5F8DD1bff34Fb92637dE9';
const ORACLE_POOL_FACTORY = '0xA5bf2ddF098bb0Ef6d120C98217dD6B141c74EE0';

const DELEGATE_OWNER = '0xBA1BA1ba1BA1bA1bA1Ba1BA1ba1BA1bA1ba1ba1B';
```

Next we'll define the token addresses. Say we want to make a pool with MKR, WETH, and USDT.

```text
// Mainnet addresses; adjust for testnets

const MKR = '0x9f8F72aA9304c8B593d555F12eF6589cC3A579A2';
const WETH = '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2';
const USDT = '0xdac17f958d2ee523a2206206994597c13d831ec7';

const tokens = [MKR, WETH, USDT];
```

{% hint style="warning" %}
Note that tokens must be sorted in numerical order
{% endhint %}

In this example, we want the weights to be 70/15/15. In V1, pool weights were given denormalized, in the range of 1-49, with the total denormalized weight capped at 50. This allowed for a 2%-98% normalized weight range.

In V2, we supply the normalized weights directly, in the range 0.01 to 0.99 \(so, 1%-99%\). By definition, the normalized weights must sum to exactly 1. We use the same 1e18 "base" as in V1 \(i.e., "1" = 1e18\).

The weights are then:

```text
const weights = [0.7e18, 0.15e18, 0.15e18];
```

Next we need to define the name, symbol, and swap fee handling. Since this is a three-token pool, it has to use the WeightedPool factory. Let's make this a fixed fee pool, at 0.5%

```text
const NAME = 'Three-token Test Pool';
const SYMBOL = '70MKR-15WETH-15USDT';
const swapFeePercentage = 0.5e16; // 0.5%

const ZERO_ADDRESS = '0x0000000000000000000000000000000000000000';    
```

To deploy the pool, we call `create` on the `WeightedPoolFactory`. \(Make sure you have at least 0.5 ETH; should cost ~ 0.33.\)

```text
const factory = await ethers.getContractAt('WeightedPoolFactory',
                                           WEIGHTED_POOL_FACTORY);
const vault = await ethers.getContractAt('Vault', VAULT);

// ZERO_ADDRESS owner means fixed swap fees
// DELEGATE_OWNER grants permission to governance for dynamic fee management
// Any other address lets that address directly set the fees
const tx = await factory.create(NAME, SYMBOL, tokens, weights,
                                swapFeePercentage, ZERO_ADDRESS);
const receipt = await tx.wait();

// We need to get the new pool ID out of the PoolRegistered event
// (Or just grab it from Etherscan)
const events = receipt.events.filter((e) => e.event === 'PoolRegistered');
const poolId = events[0].args.poolId;
```

At this point you have a new pool contract that is configured, but not initialized/funded. \(It will not show up on the Balancer UI until it's funded.\)

Now here's the tricky part! You need to do a special "init" join, supplying the initial balances. This requires encoding userData, which is what makes this very hard \(maybe impossible\) to do through Etherscan.

First, let's figure out the balances. You need to make the "internal" prices match the external market, or your pool would be immediately drained. Let's say market prices are: MKR = $2,100; ETH = $2,100; USDT = $1 \(that's the easy one\), and you want to seed it with $50,000. At 70/15/15, that means $35,000 of MKR \(16.667\), and $7,500 each of ETH \(3.5714\) and USDT \(7,500\).

```text
// Tokens must be in the same order
// Values must be decimal-normalized! (USDT has 6 decimals)
const initialBalances = [16.667e18, 3.5714e18, 7500e6];
```

All joins and exits are done on the Vault, using the poolId. The userData specifies the type of join \(in this case, the special "Init" join\).

```text
const JOIN_KIND_INIT = 0;

// Construct magic userData
const initUserData =
    ethers.utils.defaultAbiCoder.encode(['uint256', 'uint256[]'], 
                                        [JOIN_KIND_INIT, initialBalances]);
const joinPoolRequest = {
  assets: tokens,
  maxAmountsIn: initialBalances,
  userData: initUserData,
  fromInternalBalance: false
} 

// Caller is "you". joinPool takes a sender (source of initialBalances)
// And a receiver (where BPT are sent). Normally, both are the caller.
// If you have a User Balance of any of these tokens, you can set
// fromInternalBalance to true, and fund a pool with no token transfers
// (well, except for the BPT out)

// Need to approve the Vault to transfer the tokens!
// Can do through Etherscan, or programmatically
const mkr = await ethers.getContractAt('ERC20', MKR);
await mkr.approve(VAULT, 17e18);
// ... same for other tokens

// joins and exits are done on the Vault, not the pool
const tx = await vault.joinPool(poolId, caller, caller, joinPoolRequest);
// You can wait for it like this, or just print the tx hash and monitor
const receipt = await tx.wait();
```

At this point you should have a funded `WeightedPool`, visible on the Balancer UI.

If you wanted to make a two-token pool with delegated fee handling, it would be very similar. Just use the oracle factory instead, and call create with the initial oracle state and the delegate owner.

```text
const factory = await ethers.getContractAt('WeightedPool2TokenFactory',
                                           ORACLE_POOL_FACTORY);
...

const oracleEnabled = false;
const tx = await factory.create(NAME, SYMBOL, tokens, weights,
                                swapFeePercentage, oracleEnabled,
                                DELEGATE_OWNER);
```

