# Single Swaps

```text
enum SwapKind { GIVEN_IN, GIVEN_OUT }

struct SingleSwap {
   bytes32 poolId;
   SwapKind kind;
   IAsset assetIn;
   IAsset assetOut;
   uint256 amount;
   bytes userData;
}

struct FundManagement {
    address sender;
    bool fromInternalBalance;
    address payable recipient;
    bool toInternalBalance;
}

swap(SingleSwap singleSwap,
     FundManagement funds,
     uint256 limit,
     uint256 deadline) returns (uint256 amountCalculated[In/Out])
```

"Given In" means the caller knows the exact amount of the incoming token, and is asking the pool to calculate the tokenOut amount. The opposite is true of "Given Out."

The system supports multi-hop "batch" swaps - but in most cases there is only one pool involved. If both tokens involved are in the same pool, it is possible to optimize the data structures to save gas.

In this simple case, the amount is the "given" token, and the return value is the calculated result.

