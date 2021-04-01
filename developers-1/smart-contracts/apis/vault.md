# Vault

**WETH**\(\) external view returns \(IWETH\) - the Vault's address for WETH

**getAuthorizer**\(\) ****external view returns \(IAuthorizer\) - the Balancer governance contract

**getProtocolFeesCollector**\(\) external view returns \(ProtocolFeesCollector\) - the external contract authorized to collect protocol fees. _This functionality might get merged back into the Vault._

**hasAllowedRelayer**\(address user, address relayer\) external view returns\(bool\) - checks permission for an external contract

**getInternalBalance**\(address user, IERC20\[\] tokens\) external view returns \(uint256\[\]\) - get a user's internal "wallet" balances

The internal balance functions use AssetBalanceTransfer/TokenBalanceTransfer structures, which support many-to-many operations: i.e., they have independent senders and receivers \(not necessarily the transaction sender\)

**depositToInternalBalance**\(AssetBalanceTransfer\[\] transfers\) - deposit to vault "wallet"

**withdrawFromInternalBalance**\(AssetBalanceTransfer\[\] transfers\) - withdraw from vault "wallet"

**transferInternalBalance**\(TokenBalanceTransfer\[\] transfers\) - transfer between internal "wallets"

**transferToExternalBalance**\(TokenBalanceTransfer\[\] transfers\) - use the Vault's allowance to transfer between external accounts

**getPool**\(bytes32 poolId\) external view returns \(address, PoolSpecialization\)

These functions are only called by pool contracts

**registerPool**\(PoolSpecialization specialization\) external returns\(bytes32\) - called from the pool to generate a  Pool ID, and enter it in the Vault's pool data structures

**registerTokens**\(bytes32 poolId, IERC20\[\] tokens, address\[\] assetManagers\) - called from the pool to tell the Vault which tokens are valid for this pool \(i.e., which can be used to swap, join, or exit\). An asset manager can also be assigned to each token at this step, which is thereafter immutable \(unless you deregister and register again\).

**deregisterTokens**\(bytes32 poolId, IERC20\[\] tokens\) - remove a token from the pool \(must have zero balance\)

**getPoolTokens**\(bytes32 poolId\) external view returns \(IERC20\[\] tokens, uint256\[\] balances\) - return the token addresses and total balances of the given pool

**getPoolTokenInfo**\(bytes32 poolId, IERC20 token\) external view returns \(uint256 cash, uint256 managed, uint256 blockNumber, address assetManager\) - return details of a particular token. While `getPoolTokens` gives the total balance, `getPoolTokenInfo` returns each component of the balance, as well as the time it was last modified, and the asset manager

For the join and exit calls, the request structures contain an array of assets \(where the zero address is ETH\), the minimum/maximum token amounts \(to guard against front-running/slippage\), and flags indicating whether the assets should be transferred to/from the Vault, or taken from the corresponding internal balances. Note that using internal balances, it is possible to join and exit pools with zero token transfers.

**joinPool**\(bytes32 poolId, address sender, address recipient, JoinPoolRequest request\)

**exitPool**\(bytes32 poolId, address sender, address recipient, ExitPoolRequest request\)

The batch routines specify the assets involved, "many-to-many" sources and destinations, and min/max token limits to guard against slippage. There is also an optional deadline, after which the swap will timeout and revert. These return the token "deltas" - the net result of executing each swap sequentially.

"GivenIn" means the caller knows the exact amount of the incoming token, and is asking the pool to calculate the tokenOut amount. The opposite is true of "GivenOut." The `queryBatchSwap` method executes the exact same code - but reverts at the end. This is for GUIs or scripts to calculate a "dry run" of a sequence of swaps.

**batchSwapGivenIn**\(SwapIn\[\] swaps, IAsset\[\] assets, FundManagement funds, int256\[\] limits, uint256 deadline\) external returns \(int256\[\]\)

**batchSwapGivenOut**\(SwapOut\[\] swaps, IAsset\[\] assets, FundManagement funds, int256\[\] limits, uint256 deadline\) external returns \(int256\[\]\)

**queryBatchSwap**\(SwapKind kind, SwapRequest\[\] swaps, IAsset\[\] assets, FundManagement funds\) external returns \(int256\[\] memory assetDeltas\)

The vault also supports "single swaps," a way to perform exactly one trade directly and gas-efficiently with a particular pool \(e.g., for token sale GUIs\). You can still use the internal balance.

**swap**\(SingleSwap request, FundManagement funds, uint256 limit, uint256 deadline\) external returns \(uint256\)

This can only be called by the asset manager of a token in a pool.

**managePoolBalance**\(bytes32 poolId, AssetManagerOpKind kind, AssetManagerTransfer\[\] transfers\) - deposit or withdraw funds from the pool \(i.e., move funds between _cash_ and _managed_ balances\), or update the total balance \(i.e., reporting a gain or loss from management activities\).

**flashLoan**\(IFlashLoanReceiver receiver, IERC20\[\] tokens, uint256\[\] amounts, bytes receiverData\) - execute a flash loan. This sends the given token amounts to the flash loan receiver contract; all borrowed funds - plus the protocol flash loan fee - must be returned to the vault in the same transaction, or it will revert

