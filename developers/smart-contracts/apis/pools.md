# Pools

Most pool operations are conducted through the Vault. See the [Vault API](vault.md) for the following functions.

```text
registerPool(PoolSpecialization specialization) returns (bytes32 poolID)

getPool(bytes32 poolId) returns (address pool, PoolSpecialization)

getPoolTokens(bytes32 poolId) returns (
    IERC20[] tokens,
    uint256[] balances,
    uint256 maxBlockNumber)
    
getPoolTokenInfo(bytes32 poolId, IERC20 token) returns (
    uint256 cash,
    uint256 managed,
    uint256 blockNumber,
    address assetManager)
 
joinPool(bytes32 poolId,
         address sender,
         address recipient,
         JoinPoolRequest request)
         
exitPool(bytes32 poolId,
         address sender,
         address payable recipient,
         ExitPoolRequest request)
```

Pools are token contracts, with the base class `BalancerPoolToken`. New pools do not necessarily need to do tokenization this way \(or at all\). `BasePoolFactory` emits a `PoolCreated` event, while the Vault emits a `PoolRegistered` event.

The class hierarchy for pools is designed to allow for extension at multiple levels, and handle a lot of the housekeeping duties to keep the most derived pool classes short and readable.

![](../../../.gitbook/assets/v2-pools%20%281%29.png)

The BasePool level defines constants, and contains storage for the Vault, Pool ID, swap fee, token addresses, and scaling factors. The Vault does not perform any scaling \(e.g., adjusting for decimals in balances\), so this class calls `decimal` on each token contract and stores the multiplication factor necessary to convert it to 18 decimals for the Vault \(i.e., 1 if it is already 18 decimals\). Generally, all incoming balances are "up scaled" before being sent to the Vault, and "down scaled" before being returned to the caller.

This level also contains the callbacks for joining and exiting - and enforces that these can only be called **from** the Vault.

Finally, `setSwapFeePercentage` allows for dynamic fees. If the Authorizer contract approves this function for a relayer \(e.g., Gauntlet\), that relayer is then allowed to set the swap fee for the pool. Otherwise, the swap fee is immutable.

```text
getVault() returns (IVault vaultAddress)

getPoolId() returns (bytes32 poolID)

getSwapFeePercentage() returns (uint256 swapFeePercentage) 

// Can only be called by an authorized account
setSwapFeePercentage(uint256 swapFeePercentage)

// Can only be called by an authorized account (emergency stop)
function setPaused(bool paused)

onJoinPool(
        bytes32 poolId,
        address sender,
        address recipient,
        uint256[] currentBalances,
        uint256 latestBlockNumberUsed,
        uint256 protocolSwapFeePercentage,
        bytes userData
    ) returns (uint256[] amountsIn, uint256[] dueProtocolFeeAmounts)
    
onExitPool(
        bytes32 poolId,
        address sender,
        address recipient,
        uint256[] currentBalances,
        uint256 latestBlockNumberUsed,
        uint256 protocolSwapFeePercentage,
        bytes userData
    ) returns (uint256[] amountsOut, uint256[] dueProtocolFeeAmounts) {
```

The two core pools \(StablePool coming soon!\), use different math, and also different price calculations. Stable Pools need all the token balances to quote a price during a swap, while Weighted Pools need only the balances of the two tokens being swapped. Weighted Pools can take advantage of this fact to save bytes and gas by using more efficient data structures. Any such pools can inherit from BaseMinimalSwapInfoPool.

```text
// BaseMinimalSwapInfoPool
onSwap(SwapRequest request,
       uint256 balanceTokenIn,
       uint256 balanceTokenOut) returns (uint256 amount[In/Out])
```

Stable Pools inherit from BaseGeneralPool, and have a different swap interface. They take all the balances, along with pointers to the offsets of the two tokens being swapped.

```text
// BaseGeneralPool
onSwap(SwapRequest swapRequest,
       uint256[] balances,
       uint256 indexIn,
       uint256 indexOut) returns (uint256 amount[In/Out])
```

Each level contains internal callbacks \(e.g., `_initializePool`, `_doJoin`\), that need to be implemented by the most derived pools - in this case, the core pools.

