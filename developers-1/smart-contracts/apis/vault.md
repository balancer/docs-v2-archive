# Vault

### `getAuthorizer`

```
getAuthorizer() 
returns (IAuthorizer) 
```

Returns the Vault's Authorizer \(Balancer governance contract\). Implemented in `VaultAuthorization`

### `changeAuthorizer`

```
getAuthorizer(IAuthorizer newAuthorizer) 
```

Sets a new Authorizer for the Vault. The caller must be allowed by the current Authorizer to do this. Implemented in `VaultAuthorization`

### `hasAllowedRelayer`

```text
hasAllowedRelayer(
    address user, 
    address relayer) 
returns(bool)
```

 Returns true if `user` has allowed `relayer` to act as a relayer for them.  Implemented in `VaultAuthorization`

### `changeRelayerAllowance`

```text
changeRelayerAllowance(
    address sender, 
    address relayer,
    bool allowed)
```

 Returns true if `user` has allowed `relayer` to act as a relayer for them.  Implemented in `VaultAuthorization`

### **`getInternalBalance`**

```text
getInternalBalance(
    address user, 
    IERC20[] tokens) 
returns (uint256[])
```

Get a user's internal "wallet" balances. This is called the UserBalance in external interfaces, and "internal balance" in the internal functions. Implemented in `UserBalance`.

### `manageUserBalance`

```text
manageUserBalance(UserBalanceOp[] ops)
```

There are four possible operations in `manageUserBalance`: each designates a sender/receiver, asset, and amount. The asset is either a token address, or the zero address \(meaning ETH\). The Vault does not store ETH, but you can use ETH when interacting with internal balances; the Vault will do any necessary wrapping/unwrapping.

You can deposit, withdraw, or transfer internal balance. There is also an external transfer, which allows a relayer to transfer between external accounts, using the Vault's token allowance. Implemented in `UserBalance`.

### **`registerPool`**

```text
registerPool(PoolSpecialization specialization) 
returns(bytes32)
```

Called from the pool contract to generate a  Pool ID, and enter it in the Vault's pool data structures. Implemented in `PoolAssets`.

### **`getPool`**

```text
getPool(bytes32 poolId) 
returns (
    address, 
    PoolSpecialization)
```

Returns a Pool's contract address and specialization setting. Implemented in `PoolAssets`.

### **`registerTokens`**

```text
registerTokens(
    bytes32 poolId, 
    IERC20[] tokens, 
    address[] assetManagers)
```

Called from the pool contract to tell the Vault which tokens are valid for this pool \(i.e., which can be used to swap, join, or exit\). An asset manager can also be assigned to each token at this step, which is thereafter immutable \(unless you deregister and register again\). Implemented in `PoolAssets`.

### **`deregisterTokens`**

```text
deregisterTokens(
    bytes32 poolId, 
    IERC20[] tokens)
```

Remove tokens from the pool \(must have zero balance\). Implemented in `PoolAssets`.

### `getPoolTokens`

```text
getPoolTokens(bytes32 poolId)
returns (IERC20[] tokens, 
    uint256[] balances,
    uint256 maxBlockNumber)
```

Returns a Pool's registered tokens, the total balance for each, and the most recent block in which any of the tokens were updated. Implemented by PoolAssets. Implemented in `PoolAssets`.

### **`getPoolTokenInfo`**

```text
getPoolTokenInfo(bytes32 poolId, 
    IERC20 token) 
returns (uint256 cash, 
    uint256 managed, 
    uint256 blockNumber, 
    address assetManager)
```

Return details of a particular token. While `getPoolTokens` gives the total balance, `getPoolTokenInfo` returns each component of the balance, as well as the time \(block\) it was last modified, and the asset manager. Implemented in `PoolAssets`.

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

JoinPoolRequest takes a userData argument, which specifies exactly how the pool should be joined \(e.g., the token addresses and balances transferred to the Vault, and expected number of pool tokens to be minted\). Implemented by `PoolAssets`.

### `exitPool`

```text
exitPool(
    bytes32 poolId, 
    address sender, 
    address recipient, 
    ExitPoolRequest request)
```

ExitPoolRequest takes a userData argument, which specifies exactly how the pool should be exited \(e.g., the token addresses and balances transferred from the Vault, and expected number of pool tokens to be burned\). Implemented by `PoolAssets`.

## Single Swaps

The vault supports "single swaps," a way to perform exactly one trade directly and gas-efficiently with a particular pool \(e.g., for token sale GUIs\). You can still use the internal balance.

### **`swap`**

```text
swap(
    SingleSwap request, 
    FundManagement funds, 
    uint256 limit, 
    uint256 deadline) 
returns (uint256 assetDelta)
```

Implemented in `Swaps`.

## Batch Swaps

Batch swap "steps" specify the assets involved, "many-to-many" sources and destinations, and min/max token limits to guard against slippage. There is also an optional deadline, after which the swap will timeout and revert. These return the token "deltas" - the net result of executing each swap sequentially.

### **`batchSwap`**

```text
batchSwap(
    SwapKind kind,
    BatchSwapStep[] swaps, 
    IAsset[] assets, 
    FundManagement funds, 
    int256[] limits, 
    uint256 deadline) 
returns (int256[] assetDeltas)
```

Implemented in `Swaps.`

### `queryBatchSwap`

```text
queryBatchSwap(
    SwapKind kind, 
    BatchSwapStep[] swaps, 
    IAsset[] assets, 
    FundManagement funds) 
returns (int256[] assetDeltas)
```

The `queryBatchSwap` method executes the exact same code as `batchSwap` - but reverts at the end. This is for GUIs or scripts to calculate a "dry run" of a sequence of swaps.

Implemented in `Swaps.`

## Flash Loan

### **`flashLoan`**

```text
flashLoan(
    IFlashLoanReceiver receiver, 
    IERC20[] tokens, 
    uint256[] amounts, 
    bytes receiverData)
```

Execute a flash loan. This sends the given token amounts to the flash loan receiver contract; all borrowed funds - plus the protocol flash loan fee - must be returned to the vault in the same transaction, or it will revert. Implemented by a `FlashLoanProvider` subclass.

## Asset Management

This can only be called by the asset manager of a token in a pool.

### `managePoolBalance`

```text
managePoolBalance(
    bytes32 poolId, 
    AssetManagerOpKind kind, 
    AssetManagerTransfer[] transfers)
```

 Deposit or withdraw funds from the pool \(i.e., move funds between _cash_ and _managed_ balances\), or update the total balance \(i.e., reporting a gain or loss from management activities\). Implemented in `PoolAssets`.

### **`getProtocolFeesCollector`** 

```text
getProtocolFeesCollector() 
returns (ProtocolFeesCollector) 
```

The external contract authorized to collect protocol fees. Implemented by `Fees`.

### **`setEmergencySwitch`** 

```text
setEmergencySwitch(bool active)  
```

Safety mechanism to halt most Vault operations in the event of an emergency. The only functions allowed involve withdrawing funds \(e.g., from internal balances, or proportional pool exits\). Implemented by `Vault`.

### **`WETH`** 

```text
WETH()  
returns (IWETH)
```

The Vault's address for WETH. Implemented by `Vault`.

