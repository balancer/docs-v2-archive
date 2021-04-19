# Events

```text
// Issued when Vault or Pools set or clear the emergency paused state
event PausedStateChanged(bool paused)
```

```text
// Record a change to the AccessControl role Admin
event RoleAdminChanged(bytes32 indexed role,
                       bytes32 indexed previousAdminRole,
                       bytes32 indexed newAdminRole)

// Grant or Revoke permission for an account to perform a given role
// (i.e., call a specific function)
// If sender is set, restrict to specific contract                       
event RoleGranted(bytes32 indexed role,
                  address indexed account,
                  address indexed sender)
                  
event RoleRevoked(bytes32 indexed role,
                  address indexed account,
                  address indexed sender)                

// Emitted when governance changes the Authorizer contract                  
event AuthorizerSet(IAuthorizer indexed newAuthorizer)

// Approve or Revoke relayer privileges
event RelayerApprovalChanged(address indexed relayer,
                             address indexed sender,
                             bool approved)
```

```text
// When associated with a Pool, records a change to the Pool's swap fee
// When emitted from the ProtocolFeeCollector, records a change to the
//   Protocol Swap Fee
event SwapFeePercentageChanged(uint256 swapFeePercentage)

// Records a change to the Protocol Flash Loan Fee
event FlashLoanFeePercentageChanged(uint256 newFlashLoanFeePercentage)
```

```text
// Emitted by BasePoolFactory when a new pool is deployed
event PoolCreated(address indexed pool)

event PoolRegistered(bytes32 indexed poolId,
                     address indexed poolAddress,
                     PoolSpecialization specialization)
                     
// Add a set of tokens to a Pool
event TokensRegistered(bytes32 indexed poolId,
                       IERC20[] tokens,
                       address[] assetManagers)
 
// Remove a set of tokens from a Pool
event TokensDeregistered(bytes32 indexed poolId, IERC20[] tokens)

```

```text
// Record Internal (User) Balance transaction
event InternalBalanceChanged(address indexed user,
                             IERC20 indexed token,
                             int256 delta)
                             
// Record transfer between external accounts, using Vault allowance
event ExternalBalanceTransfer(IERC20 indexed token,
                              address indexed sender,
                              address recipient,
                              uint256 amount)

```

```text
// Emitted when an LP joins or exits a Pool
event PoolBalanceChanged(bytes32 indexed poolId,
                         address indexed liquidityProvider,
                         IERC20[] tokens,
                         int256[] deltas,
                         uint256[] protocolFeeAmounts)
```

```text
// Records an individual swap with a Pool (might be part of a batch swap)
event Swap(bytes32 indexed poolId,
           IERC20 indexed tokenIn,
           IERC20 indexed tokenOut,
           uint256 amountIn,
           uint256 amountOut)
```

```text
// Records an Asset Manager interaction with a Pool
// (Deposit, Withdrawal, or Update)
event PoolBalanceManaged(bytes32 indexed poolId,
                         address indexed assetManager,
                         IERC20 indexed token,
                         int256 cashDelta,
                         int256 managedDelta)

```

```text
// Records a FlashLoan 
event FlashLoan(IFlashLoanRecipient indexed recipient,
                IERC20 indexed token,
                uint256 amount,
                uint256 feeAmount)
```

