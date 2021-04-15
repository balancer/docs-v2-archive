# Asset Managers

```text
enum PoolBalanceOpKind { WITHDRAW, DEPOSIT, UPDATE }
    
struct PoolBalanceOp {
    PoolBalanceOpKind kind;
    bytes32 poolId;
    IERC20 token;
    uint256 amount;
}
    
function managePoolBalance(PoolBalanceOp[] ops);
```

Each token in the pool can be associated with an Asset Manager contract. \(Note: the core pools do not support asset managers - these will be generally available when Smart Pools are released.\)

Authorized Asset Managers can call the Vault's `managePoolBalance` function to perform batch operations on pools. They can withdraw tokens from the Vault \(and then "invest" them according to the strategy\), return them to the Vault with deposit, or update the total \(to report gains/losses\).

Asset Managers will subclass the base `AssetManager`, which is TBD, but likely to look something like this.

```text
getBalance(bytes32 poolId) returns (uint256 managedTokenBalance)

getInvestablePercent(bytes32 poolId) returns (uint256) 

setInvestablePercent(bytes32 poolId, uint256 investmentPercent)

maxInvestableBalance(bytes32 poolId) returns (int256 maxBalance)

// Called by anyone, to realize gains/losses
updateBalanceOfPool(bytes32 poolId)
```

