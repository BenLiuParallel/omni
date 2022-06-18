# PoolConfigurator

## Events

### ReserveInitialized

`event ReserveInitialized(address indexed asset, address indexed xToken, address stableDebtToken, address variableDebtToken, address interestRateStrategyAddress)`

Emitted when a reserve is initialized.

#### Call Params

| Name                        | Type      | Description                                               |
| --------------------------- | --------- | --------------------------------------------------------- |
| asset                       | `address` | The address of the underlying asset of the reserve        |
| xToken                      | `address` | The address of the associated xToken contract             |
| stableDebtToken             | `address` | The address of the associated stable rate debt token      |
| variableDebtToken           | `address` | The address of the associated variable rate debt token    |
| interestRateStrategyAddress | `address` | The address of the interest rate strategy for the reserve |

### ReserveBorrowing

`event ReserveBorrowing(address indexed asset, bool enabled)`

Emitted when borrowing is enabled or disabled on a reserve.

#### Call Params

| Name    | Type      | Description                                        |
| ------- | --------- | -------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve |
| enabled | `bool`    | True if borrowing is enabled, false otherwise      |

### CollateralConfigurationChanged

`event CollateralConfigurationChanged(address indexed asset, uint256 ltv, uint256 liquidationThreshold, uint256 liquidationBonus)`

Emitted when the collateralization risk parameters for the specified asset are updated.

#### Call Params

| Name                 | Type      | Description                                                                                        |
| -------------------- | --------- | -------------------------------------------------------------------------------------------------- |
| asset                | `address` | The address of the underlying asset of the reserve                                                 |
| ltv                  | `uint256` | The loan to value of the asset when used as collateral                                             |
| liquidationThreshold | `uint256` | The threshold at which loans using this asset as collateral will be considered undercollateralized |
| liquidationBonus     | `uint256` | The bonus liquidators receive to liquidate this asset                                              |

### ReserveStableRateBorrowing

`event ReserveStableRateBorrowing(address indexed asset, bool enabled)`

Emitted when stable rate borrowing is enabled or disabled on a reserve

#### Call Params

| Name    | Type      | Description                                                   |
| ------- | --------- | ------------------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve            |
| enabled | `bool`    | `true` if stable rate borrowing is enabled, `false` otherwise |

### ReserveActive

`event ReserveActive(address indexed asset, bool active)`

Emitted when a reserve is activated or deactivated

#### Call Params

| Name    | Type      | Description                                        |
| ------- | --------- | -------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve |
| enabled | `bool`    | `true` if reserve is active, `false` otherwise     |

### ReserveFrozen

`event ReserveFrozen(address indexed asset, bool frozen)`

Emitted when a reserve is frozen or unfrozen

#### Call Params

| Name    | Type      | Description                                        |
| ------- | --------- | -------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve |
| enabled | `bool`    | `true` if reserve is frozen, `false` otherwise     |

### ReservePaused

`event ReservePaused(address indexed asset, bool paused)`

Emitted when a reserve is paused or unpaused

#### Call Params

| Name    | Type      | Description                                        |
| ------- | --------- | -------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve |
| enabled | `bool`    | `true` if reserve is paused, `false` otherwise     |

### ReserveDropped

`event ReserveDropped(address indexed asset)`

Emitted when a reserve is dropped.

#### Call Params

| Name  | Type      | Description                                        |
| ----- | --------- | -------------------------------------------------- |
| asset | `address` | The address of the underlying asset of the reserve |

### ReserveFactorChanged

`event ReserveFactorChanged(address indexed asset, uint256 oldReserveFactor, uint256 newReserveFactor)`

Emitted when a reserve factor is updated.

#### Call Params

| Name             | Type      | Description                                        |
| ---------------- | --------- | -------------------------------------------------- |
| asset            | `address` | The address of the underlying asset of the reserve |
| oldReserveFactor | `uint256` | The old reserve factor, expressed in bps           |
| newReserveFactor | `uint256` | The new reserve factor, expressed in bps           |

### BorrowCapChanged

`event BorrowCapChanged(address indexed asset, uint256 oldBorrowCap, uint256 newBorrowCap)`

Emitted when the borrow cap of a reserve is updated.

#### Call Params

| Name         | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| asset        | `address` | The address of the underlying asset of the reserve |
| oldBorrowCap | `uint256` | The old borrow cap                                 |
| newBorrowCap | `uint256` | The new borrow cap                                 |

### SupplyCapChanged

`event SupplyCapChanged(address indexed asset, uint256 oldSupplyCap, uint256 newSupplyCap)`

Emitted when the supply cap of a reserve is updated.

#### Call Params

| Name         | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| asset        | `address` | The address of the underlying asset of the reserve |
| oldSupplyCap | `uint256` | The old supply cap                                 |
| newSupplyCap | `uint256` | The new supply cap                                 |

### LiquidationProtocolFeeChanged

`event LiquidationProtocolFeeChanged(address indexed asset, uint256 oldFee, uint256 newFee)`

Emitted when the liquidation protocol fee of a reserve is updated.

#### Call Params

| Name   | Type      | Description                                        |
| ------ | --------- | -------------------------------------------------- |
| asset  | `address` | The address of the underlying asset of the reserve |
| oldFee | `uint256` | The old liquidation protocol fee, expressed in bps |
| newFee | `uint256` | The new liquidation protocol fee, expressed in bps |

### ReserveInterestRateStrategyChanged

`event ReserveInterestRateStrategyChanged(address indexed asset, address oldStrategy, address newStrategy)`

Emitted when a reserve interest strategy contract is updated.

#### Call Params

| Name        | Type      | Description                                        |
| ----------- | --------- | -------------------------------------------------- |
| asset       | `address` | The address of the underlying asset of the reserve |
| oldStrategy | `address` | The address of the old interest strategy contract  |
| newStrategy | `address` | The address of the new interest strategy contract  |

### XTokenUpgraded

`event XTokenUpgraded(address indexed asset, address indexed proxy, address indexed implementation)`

Emitted when an xToken implementation is upgraded.

#### Call Params

| Name           | Type      | Description                                        |
| -------------- | --------- | -------------------------------------------------- |
| asset          | `address` | The address of the underlying asset of the reserve |
| proxy          | `address` | The xToken proxy address                           |
| implementation | `address` | The new xToken implementation                      |

### StableDebtTokenUpgraded

`event StableDebtTokenUpgraded(address indexed asset, address indexed proxy, address indexed implementation)`

Emitted when the implementation of a stable debt token is upgraded.

#### Call Params

| Name           | Type      | Description                                        |
| -------------- | --------- | -------------------------------------------------- |
| asset          | `address` | The address of the underlying asset of the reserve |
| proxy          | `address` | The stable debt token proxy address                |
| implementation | `address` | The new xToken implementation                      |

### VariableDebtTokenUpgraded

`event VariableDebtTokenUpgraded(address indexed asset, address indexed proxy, address indexed implementation)`

Emitted when the implementation of a variable debt token is upgraded.

#### Call Params

| Name           | Type      | Description                                                    |
| -------------- | --------- | -------------------------------------------------------------- |
| asset          | `address` | The address of the underlying asset of the reserve             |
| proxy          | `address` | The variable debt token proxy address debt token proxy address |
| implementation | `address` | The new xToken implementation                                  |

### SiloedBorrowingChanged

`event SiloedBorrowingChanged(address indexed asset, bool oldState, bool newState)`

Emitted when the the siloed borrowing state for an asset is changed.

#### Call Params

| Name     | Type      | Description                                        |
| -------- | --------- | -------------------------------------------------- |
| asset    | `address` | The address of the underlying asset of the reserve |
| oldState | `bool`    | The old siloed borrowing state                     |
| newState | `bool`    | The new siloed borrowing state                     |

### BorrowableInIsolationChanged

`event BorrowableInIsolationChanged(address asset, bool borrowable)`

Emitted when the reserve is set as borrowable/non borrowable in isolation mode.

#### Call Params

| Name       | Type      | Description                                                     |
| ---------- | --------- | --------------------------------------------------------------- |
| asset      | `address` | The address of the underlying asset of the reserve              |
| borrowable | `bool`    | True if the reserve is borrowable in isolation, false otherwise |

## Write Functions

### initReserves

`function initReserves(ConfiguratorInputTypes.InitReserveInput[] calldata input) external`

Initializes multiple reserves.

#### Call Params

| Name  | Type                 | Description                            |
| ----- | -------------------- | -------------------------------------- |
| input | `InitReserveInput[]` | The array of initialization parameters |

### updatePToken

`function updatePToken(ConfiguratorInputTypes.UpdateXTokenInput calldata input) external`

Updates the xToken implementation for the reserve.

#### Call Params

| Name  | Type                | Description                  |
| ----- | ------------------- | ---------------------------- |
| input | `UpdateXTokenInput` | The xToken update parameters |

### updateStableDebtToken

`function updateStableDebtToken(ConfiguratorInputTypes.UpdateDebtTokenInput calldata input) external`

Updates the stable debt token implementation for the reserve.

#### Call Params

| Name  | Type                   | Description                           |
| ----- | ---------------------- | ------------------------------------- |
| input | `UpdateDebtTokenInput` | The stableDebtToken update parameters |

### updateVariableDebtToken

`function updateVariableDebtToken(ConfiguratorInputTypes.UpdateDebtTokenInput calldata input) external`

Updates the variable debt token implementation for the asset.

#### Call Params

| Name  | Type                   | Description                             |
| ----- | ---------------------- | --------------------------------------- |
| input | `UpdateDebtTokenInput` | The variableDebtToken update parameters |

### setReserveBorrowing

`function setReserveBorrowing(address asset, bool enabled) external`

Configures borrowing on a reserve. Can only be disabled (set to false) if stable borrowing is disabled.

#### Call Params

| Name    | Type      | Description                                            |
| ------- | --------- | ------------------------------------------------------ |
| asset   | `address` | The address of the underlying asset of the reserve     |
| enabled | `bool`    | True if borrowing needs to be enabled, false otherwise |

### configureReserveAsCollateral

`function configureReserveAsCollateral(address asset, uint256 ltv, uint256 liquidationThreshold, uint256 liquidationBonus) external`&#x20;

Configures the reserve collateralization parameters. All the values are expressed in bps. A value of 10000, results in 100.00%. The `liquidationBonus` is always above 100%. A value of 105% means the liquidator will receive a 5% bonus.

#### Call Params

| Name                 | Type      | Description                                                                                        |
| -------------------- | --------- | -------------------------------------------------------------------------------------------------- |
| asset                | `address` | The address of the underlying asset of the reserve                                                 |
| ltv                  | `uint256` | The loan to value of the asset when used as collateral                                             |
| liquidationThreshold | `uint256` | The threshold at which loans using this asset as collateral will be considered undercollateralized |
| liquidationBonus     | `uint256` | The bonus liquidators receive to liquidate this asset                                              |

### setReserveStableRateBorrowing

`function setReserveStableRateBorrowing(address asset, bool enabled) external`

Enable or disable stable rate borrowing on a reserve. Can only be enabled (set to true) if borrowing is enabled.

#### Call Params

| Name    | Type      | Description                                                            |
| ------- | --------- | ---------------------------------------------------------------------- |
| asset   | `address` | The address of the underlying asset of the reserve                     |
| enabled | `bool`    | `true` if stable rate borrowing needs to be enabled, `false` otherwise |

### setReserveActive

`function setReserveActive(address asset, bool active) external`

Activate or deactivate a reserve.

#### Call Params

| Name   | Type      | Description                                                            |
| ------ | --------- | ---------------------------------------------------------------------- |
| asset  | `address` | The address of the underlying asset of the reserve                     |
| active | `bool`    | `true` if stable rate borrowing needs to be enabled, `false` otherwise |

### setReserveFreeze

`function setReserveFreeze(address asset, bool freeze) external`

Freeze or unfreeze a reserve. A frozen reserve doesn't allow any new supply, borrow or rate swap but allows repayments, liquidations, rate rebalances and withdrawals.

#### Call Params

| Name   | Type      | Description                                                 |
| ------ | --------- | ----------------------------------------------------------- |
| asset  | `address` | The address of the underlying asset of the reserve          |
| freeze | `bool`    | `true` if the reserve needs to be frozen, `false` otherwise |

### setBorrowableInIsolation

`function setBorrowableInIsolation(address asset, bool borrowable) external`

Sets the borrowable in isolation flag for the reserve.

#### Call Params

| Name       | Type      | Description                                                              |
| ---------- | --------- | ------------------------------------------------------------------------ |
| asset      | `address` | The address of the underlying asset of the reserve                       |
| borrowable | `bool`    | `true` if the asset should be borrowable in isolation, `false` otherwise |

### setReservePause

`function setReservePause(address asset, bool paused) external`

Pauses a reserve. A paused reserve does not allow any interaction (supply, borrow, repay, swap interest rate, liquidate, atoken transfers).

#### Call Params

| Name   | Type      | Description                                        |
| ------ | --------- | -------------------------------------------------- |
| asset  | `address` | The address of the underlying asset of the reserve |
| paused | `bool`    | `true` if pausing the reserve, `false` otherwise   |

### setReserveFactor

`function setReserveFactor(address asset, uint256 newReserveFactor) external`

Updates the reserve factor of a reserve.

#### Call Params

| Name             | Type      | Description                                        |
| ---------------- | --------- | -------------------------------------------------- |
| asset            | `address` | The address of the underlying asset of the reserve |
| newReserveFactor | `uint256` | The new reserve factor of the reserve              |

### setReserveInterestRateStrategyAddress

`function setReserveInterestRateStrategyAddress(address asset, address newRateStrategyAddress) external`

Sets the interest rate strategy of a reserve.

#### Call Params

| Name                   | Type      | Description                                        |
| ---------------------- | --------- | -------------------------------------------------- |
| asset                  | `address` | The address of the underlying asset of the reserve |
| newRateStrategyAddress | `address` | The address of the new interest strategy contract  |

### setPoolPaused

`function setPoolPause(bool paused) external`

Pauses or unpauses all the protocol reserves. In the paused state all the protocol interactions are suspended.

#### Call Params

| Name   | Type   | Description                                              |
| ------ | ------ | -------------------------------------------------------- |
| paused | `bool` | `true` if protocol needs to be paused, `false` otherwise |

### setBorrowCap

`function setBorrowCap(address asset, uint256 newBorrowCap) external`

Updates the borrow cap of a reserve.

#### Call Params

| Name         | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| asset        | `address` | The address of the underlying asset of the reserve |
| newBorrowCap | `uint256` | The new borrow cap of the reserve                  |

### setSupplyCap

`function setSupplyCap(address asset, uint256 newSupplyCap) external`

Updates the supply cap of a reserve.

#### Call Params

| Name         | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| asset        | `address` | The address of the underlying asset of the reserve |
| newBorrowCap | `uint256` | The new supply cap of the reserve                  |

### setLiquidationProtocolFee

`function setLiquidationProtocolFee(address asset, uint256 newFee) external`

Updates the liquidation protocol fee of reserve.

#### Call Params

| Name   | Type      | Description                                                       |
| ------ | --------- | ----------------------------------------------------------------- |
| asset  | `address` | The address of the underlying asset of the reserve                |
| newFee | `uint256` | The new liquidation protocol fee of the reserve, expressed in bps |

### dropReserve

`function dropReserve(address asset) external`

Drops a reserve entirely.

#### Call Params

| Name  | Type      | Description                        |
| ----- | --------- | ---------------------------------- |
| asset | `address` | The address of the reserve to drop |

### setSiloedBorrowing

`function setSiloedBorrowing(address asset, bool siloed) external`

Sets siloed borrowing for an asset

#### Call Params

| Name   | Type      | Description                             |
| ------ | --------- | --------------------------------------- |
| asset  | `address` | The address of the asset to set siloed. |
| siloed | `bool`    | The new siloed borrowing state          |
