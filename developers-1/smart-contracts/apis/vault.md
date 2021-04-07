# Vault

### **`WETH`** 

```text
WETH()  
returns (IWETH)
```

The Vault's address for WETH

### `getAuthorizer`

```
getAuthorizer() 
returns (IAuthorizer) 
```

The Balancer governance contract

### **`getProtocolFeesCollector`** 

```text
getProtocolFeesCollector() 
returns (ProtocolFeesCollector) 
```

The external contract authorized to collect protocol fees. _This functionality might get merged back into the Vault._

### `hasAllowedRelayer`

```text
hasAllowedRelayer(
    address user, 
    address relayer) 
returns(bool)
```

 Checks permission for an external contract

### **`getInternalBalance`**

```text
getInternalBalance(
    address user, 
    IERC20[] tokens) 
returns (uint256[])
```

 Get a user's internal "wallet" balances

The internal balance functions use AssetBalanceTransfer/TokenBalanceTransfer structures, which support many-to-many operations: i.e., they have independent senders and receivers \(not necessarily the transaction sender\)

### **`depositToInternalBalance`**

```text
depositToInternalBalance(AssetBalanceTransfer[] transfers)
```

Deposit to vault "wallet"

### `withdrawFromInternalBalance`

```text
withdrawFromInternalBalance(AssetBalanceTransfer[] transfers)
```

 Withdraw from vault "wallet"

### **`transferInternalBalance`**

```text
transferInternalBalance(TokenBalanceTransfer[] transfers)
```

Transfer between internal "wallets"

### **`transferToExternalBalance`**

```text
transferToExternalBalance(TokenBalanceTransfer[] transfers)
```

 Use the Vault's allowance to transfer between external accounts

### **`getPool`**

```text
getPool(
    bytes32 poolId) 
returns (address, 
    PoolSpecialization)
```

These functions are only called by pool contracts

### **`registerPool`**

```text
registerPool(
    PoolSpecialization specialization) 
returns(bytes32)
```

 Called from the pool to generate a  Pool ID, and enter it in the Vault's pool data structures

### **`registerTokens`**

```text
registerTokens(
    bytes32 poolId, 
    IERC20[] tokens, 
    address[] assetManagers)
```

Called from the pool to tell the Vault which tokens are valid for this pool \(i.e., which can be used to swap, join, or exit\). An asset manager can also be assigned to each token at this step, which is thereafter immutable \(unless you deregister and register again\).

### **`deregisterTokens`**

```text
deregisterTokens(
    bytes32 poolId, 
    IERC20[] tokens)
```

Remove tokens from the pool \(must have zero balance\)

### `getPoolTokens`

```text
getPoolTokens(bytes32 poolId)
returns (IERC20[] tokens, 
    uint256[] balances)
```

External view  - return the token addresses and total balances of the given pool

### **`getPoolTokenInfo`**

```text
getPoolTokenInfo(bytes32 poolId, 
    IERC20 token) 
returns (uint256 cash, 
    uint256 managed, 
    uint256 blockNumber, 
    address assetManager)
```

 Return details of a particular token. While `getPoolTokens` gives the total balance, `getPoolTokenInfo` returns each component of the balance, as well as the time \(block\) it was last modified, and the asset manager

## Joins and Exits

For the join and exit calls, the request structures contain an array of assets \(where the zero address is ETH\), the minimum/maximum token amounts \(to guard against front-running/slippage\), and flags indicating whether the assets should be transferred to/from the Vault, or taken from the corresponding internal balances. Note that using internal balances, it is possible to join and exit pools with zero token transfers.

### `joinPool`

```text
joinPool(
    bytes32 poolId, 
    address sender, 
    address recipient, 
    JoinPoolRequest request)
```

### `exitPool`

```text
exitPool(
    bytes32 poolId, 
    address sender, 
    address recipient, 
    ExitPoolRequest request)
```

## Batch Routines

The batch routines specify the assets involved, "many-to-many" sources and destinations, and min/max token limits to guard against slippage. There is also an optional deadline, after which the swap will timeout and revert. These return the token "deltas" - the net result of executing each swap sequentially.

"GivenIn" means the caller knows the exact amount of the incoming token, and is asking the pool to calculate the tokenOut amount. The opposite is true of "GivenOut." The `queryBatchSwap` method executes the exact same code - but reverts at the end. This is for GUIs or scripts to calculate a "dry run" of a sequence of swaps.

### **`batchSwapGivenIn`**

```text
batchSwapGivenIn(
    SwapIn[] swaps, 
    IAsset[] assets, 
    FundManagement funds, 
    int256[] limits, 
    uint256 deadline) 
returns (int256[])
```

### **`batchSwapGivenOut`**

```text
batchSwapGivenOut(
    SwapOut[] swaps, 
    IAsset[] assets, 
    FundManagement funds, 
    int256[] limits, 
    uint256 deadline) 
returns (int256[])
```

### `queryBatchSwap`

```text
queryBatchSwap(
    SwapKind kind, 
    SwapRequest[] swaps, 
    IAsset[] assets, 
    FundManagement funds) 
returns (int256[] memory assetDeltas)
```

## Single Swaps

The vault also supports "single swaps," a way to perform exactly one trade directly and gas-efficiently with a particular pool \(e.g., for token sale GUIs\). You can still use the internal balance.

### **`swap`**

```text
swap(
    SingleSwap request, 
    FundManagement funds, 
    uint256 limit, 
    uint256 deadline) 
returns (uint256)
```

## Asset Management

This can only be called by the asset manager of a token in a pool.

### `mangePoolBalance`

```text
managePoolBalance(
    bytes32 poolId, 
    AssetManagerOpKind kind, 
    AssetManagerTransfer[] transfers)
```

 Deposit or withdraw funds from the pool \(i.e., move funds between _cash_ and _managed_ balances\), or update the total balance \(i.e., reporting a gain or loss from management activities\).

## Flash Loan

### **`flashLoan`**

```text
flashLoan(
    IFlashLoanReceiver receiver, 
    IERC20[] tokens, 
    uint256[] amounts, 
    bytes receiverData)
```

Execute a flash loan. This sends the given token amounts to the flash loan receiver contract; all borrowed funds - plus the protocol flash loan fee - must be returned to the vault in the same transaction, or it will revert.

