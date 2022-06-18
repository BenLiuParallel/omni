# Pool

The `pool.sol` contract is the main user facing contract of the protocol. It exposes the liquidity management methods that can be invoked using either _**Solidity**_ or _**Web3**_ libraries.

## Events

### Supply

`event Supply(address indexed reserve, address user, address indexed onBehalfOf, uint256 amount, uint16 indexed referralCode)`

Emitted on `supply()`

#### Call Params

| Name         | Type      | Description                                          |
| ------------ | --------- | ---------------------------------------------------- |
| reserve      | `address` | The address of the underlying asset of the reserve   |
| user         | `address` | The address initiating the supply                    |
| onBehalfOf   | `address` | The beneficiary of the supply, receiving the xTokens |
| amount       | `uint256` | The amount supplied                                  |
| referralCode | `uint16`  | The referral code used                               |

### SupplyERC721

`event SupplyERC721(address indexed reserve, address user, address indexed onBehalfOf, DataTypes.ERC721SupplyParams[] tokenData, uint16 indexed referralCode)`

Emitted on `supplyERC721()`

#### Call Params

| Name         | Type                   | Description                                                                                                                                                                   |
| ------------ | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| reserve      | `address`              | The address of the underlying asset of the reserve                                                                                                                            |
| user         | `address`              | The address initiating the supply                                                                                                                                             |
| onBehalfOf   | `address`              | The beneficiary of the supply, receiving the xTokens                                                                                                                          |
| tokenData    | `ERC721SupplyParams[]` | <p>Array of ERC721SupplyParams.</p><p><code>struct ERC721SupplyParams {</code><br>  <code>uint256 tokenId</code><br>  <code>bool useAsCollateral</code><br><code>}</code></p> |
| referralCode | `uint16`               | The referral code used                                                                                                                                                        |

### Withdraw

`event Withdraw(address indexed reserve, address indexed user, address indexed to, uint256 amount`

Emitted on `withdraw()`

#### Call Params

| Name    | Type      | Description                                             |
| ------- | --------- | ------------------------------------------------------- |
| reserve | `address` | The address of the underlying asset being withdrawn     |
| user    | `address` | The address initiating the withdrawal, owner of xTokens |
| to      | `address` | The address that will receive the underlying            |
| amount  | `uint256` | The amount to be withdrawn                              |

### WithdrawERC721

`event WithdrawERC721(address indexed reserve, address indexed user, address indexed to, uint256[] tokenIds`

Emitted on `withdrawERC721()`

#### Call Params

| Name     | Type        | Description                                             |
| -------- | ----------- | ------------------------------------------------------- |
| reserve  | `address`   | The address of the underlying asset being withdrawn     |
| user     | `address`   | The address initiating the withdrawal, owner of xTokens |
| to       | `address`   | The address that will receive the underlying            |
| tokenIds | `uint256[]` | The array of tokenIds to be withdrawn.                  |

### Borrow

`event Borrow(address indexed reserve, address user, address indexed onBehalfOf, uint256 amount, DataTypes.InterestRateMode interestRateMode, uint256 borrowRate, uint16 indexed referralCode`

Emitted on `borrow()` when debt needs to be opened.

#### Call Params

| Name             | Type               | Description                                                                      |
| ---------------- | ------------------ | -------------------------------------------------------------------------------- |
| reserve          | `address`          | The address of the underlying asset being borrowed                               |
| user             | `address`          | The address of the user initiating the borrow(), receiving the funds on borrow() |
| onBehalfOf       | `address`          | The address that will be getting the debt                                        |
| amount           | `uint256`          | The amount borrowed out                                                          |
| interestRateMode | `InterestRateMode` | The rate mode: 1 for Stable, 2 for Variable                                      |
| borrowRate       | `uint256`          | The numeric rate at which the user has borrowed                                  |
| referralCode     | `uint16`           | The referral code used                                                           |

### Repay

`event Repay(address indexed reserve, address indexed user, address indexed repayer, uint256 amount, bool usePTokens)`

Emitted on `repay()`

#### Call Params

| Name       | Type      | Description                                                                                   |
| ---------- | --------- | --------------------------------------------------------------------------------------------- |
| reserve    | `address` | The address of the underlying asset of the reserve                                            |
| user       | `address` | The beneficiary of the repayment, getting his debt reduced                                    |
| repayer    | `address` | The address that will be gThe address of the user initiating the repay(), providing the funds |
| amount     | `uint256` | The amount repaid                                                                             |
| usePTokens | `bool`    | `true` if the repayment is done using xTokens, `false` if done with underlying asset directly |

### SwapBorrowRateMode

`event SwapBorrowRateMode(address indexed reserve, address indexed user, DataTypes.InterestRateMode interestRateMode)`

Emitted on `swapBorrowRateMode()`

#### Call Params

| Name             | Type               | Description                                                                                |
| ---------------- | ------------------ | ------------------------------------------------------------------------------------------ |
| reserve          | `address`          | The address of the The address of the underlying asset of the reserve                      |
| user             | `address`          | The address of the user swapping his/her rate mode                                         |
| interestRateMode | `InterestRateMode` | The current interest rate mode of the position being swapped: 1 for Stable, 2 for Variable |

### ReserveUsedAsCollateralEnabled

`event ReserveUsedAsCollateralEnabled(address indexed reserve, address indexed user)`

Emitted on `setUserUseReserveAsCollateral()`

#### Call Params

| Name    | Type      | Description                                              |
| ------- | --------- | -------------------------------------------------------- |
| reserve | `address` | The address of the underlying asset of the reserve       |
| user    | `address` | The address of the user enabling the usage as collateral |

### ReserveUsedAsCollateralDisabled

`event ReserveUsedAsCollateralDisabled(address indexed reserve, address indexed user)`

Emitted on `setUserUseReserveAsCollateral()`

#### Call Params

| Name    | Type      | Description                                              |
| ------- | --------- | -------------------------------------------------------- |
| reserve | `address` | The address of the underlying asset of the reserve       |
| user    | `address` | The address of the user enabling the usage as collateral |

### RebalanceStableBorrowRate

`event RebalanceStableBorrowRate(address indexed reserve, address indexed user)`

Emitted on `rebalanceStableBorrowRate()`

#### Call Params

| Name    | Type      | Description                                                       |
| ------- | --------- | ----------------------------------------------------------------- |
| reserve | `address` | The address of the underlying asset of the reserve                |
| user    | `address` | The address of the user for which the rebalance has been executed |

### LiquidationCall

`event LiquidationCall(address indexed collateralAsset, address indexed debtAsset, address indexed user, uint256 debtToCover, uint256 liquidatedCollateralAmount, address liquidator, bool receivePToken`

Emitted when a borrower is liquidated.

#### Call Params

| Name                       | Type      | Description                                                                                                                                       |
| -------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| collateralAsset            | `address` | The address of the underlying asset used as collateral, to receive as result of the liquidation                                                   |
| debtAsset                  | `address` | The address of the underlying borrowed asset to be repaid with the liquidation                                                                    |
| user                       | `address` | The address of the borrower getting liquidated                                                                                                    |
| debtToCover                | `uint256` | The debt amount of borrowed `asset` the liquidator wants to cover                                                                                 |
| liquidatedCollateralAmount | `uint256` | The amount of collateral received by the liquidator                                                                                               |
| liquidator                 | `address` | The address of the liquidator                                                                                                                     |
| receivePToken              | `bool`    | `true` if the liquidator wants to receive the collateral xTokens, `false` if liquidator wants to receive the underlying collateral asset directly |

### ReserveDataUpdated

`event ReserveDataUpdated(address indexed reserve, uint256 liquidityRate, uint256 stableBorrowRate, uint256 variableBorrowRate, uint256 liquidityIndex, uint256 variableBorrowIndex)`

Emitted when the state of a reserve is updated.

#### Call Params

| Name                | Type      | Description                                        |
| ------------------- | --------- | -------------------------------------------------- |
| reserve             | `address` | The address of the underlying asset of the reserve |
| liquidityRate       | `uint256` | The next liquidity rate                            |
| stableBorrowRate    | `uint256` | The next stable borrow rate                        |
| variableBorrowRate  | `uint256` | The next variable borrow rate                      |
| liquidityIndex      | `uint256` | The next liquidity index                           |
| variableBorrowIndex | `uint256` | The next variable borrow index                     |

### MintedToTreasury

`event MintedToTreasury(address indexed reserve, uint256 amountMinted)`

Emitted when the protocol treasury receives minted xTokens from the accrued interest.

#### Call Params

| Name         | Type      | Description                       |
| ------------ | --------- | --------------------------------- |
| reserve      | `address` | The address of the reserve        |
| amountMinted | `uint256` | The amount minted to the treasury |

### FlashClaim

`event FlashClaim(address indexed target, address indexed initiator, address indexed nftAsset, uint256 tokenId`

Emitted on `flashClaim()`

#### Call Params

| Name      | Type      | Description                                     |
| --------- | --------- | ----------------------------------------------- |
| target    | `address` | The address of the flash loan receiver contract |
| initiator | `address` | The address initiating the flash claim          |
| nftAsset  | `address` | address of the underlying asset of NFT          |
| tokenId   | `uint256` | The token id of the asset being flash borrowed  |

## Read Functions

### getUserAccountData

`function getUserAccountData(address user)`

Returns the user account data across all the reserves

#### Call Params

| Name | Type      | Description         |
| ---- | --------- | ------------------- |
| user | `address` | address of the user |

#### Return Values

| Name                        | Type      | Description                                                 |
| --------------------------- | --------- | ----------------------------------------------------------- |
| totalCollateralBase         | `uint256` | total collateral of the user, in market’s base currency     |
| totalDebtBase               | `uint256` | total debt of the user, in market’s base currency           |
| availableBorrowsBase        | `uint256` | borrowing power left of the user, in market’s base currency |
| currentLiquidationThreshold | `uint256` | liquidation threshold of the user                           |
| ltv                         | `uint256` | Loan To Value of the user                                   |
| healthFactor                | `uint256` | current health factor of the user                           |

### getConfiguration

`function getConfiguration(address asset)`

Returns the configuration of the reserve.

#### Call Params

| Name  | Type      | Description                             |
| ----- | --------- | --------------------------------------- |
| asset | `address` | address of the underlying reserve asset |

#### Return Values

| Name          | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| configuration | `uint256` | <p>Reserve configuration. </p><p>bit 0-15: LTV </p><p>bit 16-31: Liquidation threshold </p><p>bit 32-47: Liquidation bonus </p><p>bit 48-55: Decimals </p><p>bit 56: reserve is active </p><p>bit 57: reserve is frozen </p><p>bit 58: borrowing is enabled </p><p>bit 59: stable rate borrowing enabled </p><p>bit 60: asset is paused </p><p>bit 61: borrowing in isolation mode is enabled </p><p>bit 62-63: reserved </p><p>bit 64-79: reserve factor </p><p>bit 80-115: borrow cap in whole tokens, 0 ⇒ no cap </p><p>bit 116-151: supply cap in whole tokens, 0 ⇒ no cap </p><p>bit 152-167: liquidation protocol fee </p><p>bit 168-175: eMode category </p><p>bit 176-211: unbacked mint cap in whole tokens, 0 ⇒ no cap </p><p>bit 212-251: debt ceiling for isolation mode with decimals </p><p>bit 252-255: unused</p> |

### getUserConfiguration

`function getUserConfiguration(address user)`

Returns the configuration of the user across all the reserves.

#### Call Params

| Name | Type      | Description         |
| ---- | --------- | ------------------- |
| user | `address` | address of the user |

#### Return Values

| Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| uint256 | <p>Bitmap of the users collaterals and borrows. Its divided into pairs of bits, one pair for each asset.<br>The first bit of the pair indicates if it is being used as collateral by the user, the second bit indicates if it is being borrowed. The corresponding assets are in the same position as getReservesList() For example, if the hex value returned is 0x40020, which represents a decimal value of 262176, then in binary it is 1000000000000100000. If we format the binary value into pairs, starting from the right, we get 1 00 00 00 00 00 00 10 00 00. If we start from the right and move left in the above binary pairs, the third pair is 10. Therefore the 1 indicates that third asset from the reserveList is used as collateral, and 0 indicates it has not been borrowed by this user.</p> |

### getReserveNormalizedIncome

`function getReserveNormalizedIncome(address asset)`

Returns the ongoing normalized income for the reserve.

#### Call Params

| Name  | Type      | Description          |
| ----- | --------- | -------------------- |
| asset | `address` | address of the asset |

#### Return Value

| Type    | Description                         |
| ------- | ----------------------------------- |
| uint256 | Normalized income, expressed in ray |

### getReserveNormalizedVariableDebt

`function getReserveNormalizedVariableDebt(address asset)`

Returns the ongoing normalized variable debt for the reserve.

#### Call Params

| Name  | Type      | Description          |
| ----- | --------- | -------------------- |
| asset | `address` | address of the asset |

#### Return Value

| Type    | Description                       |
| ------- | --------------------------------- |
| uint256 | Normalized debt, expressed in ray |

### getReserveData

`function getReserveData(address asset)`

Returns the state and configuration of the reserve.

#### Call Params

| Name  | Type      | Description                             |
| ----- | --------- | --------------------------------------- |
| asset | `address` | address of the underlying reserve asset |

#### Return Values

| Name                        | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| configuration               | `uint256`   | <p>Reserve configuration. </p><p>bit 0-15: LTV </p><p>bit 16-31: Liquidation threshold </p><p>bit 32-47: Liquidation bonus </p><p>bit 48-55: Decimals </p><p>bit 56: reserve is active </p><p>bit 57: reserve is frozen </p><p>bit 58: borrowing is enabled </p><p>bit 59: stable rate borrowing enabled </p><p>bit 60: asset is paused </p><p>bit 61: borrowing in isolation mode is enabled </p><p>bit 62-63: reserved </p><p>bit 64-79: reserve factor </p><p>bit 80-115: borrow cap in whole tokens, 0 ⇒ no cap </p><p>bit 116-151: supply cap in whole tokens, 0 ⇒ no cap </p><p>bit 152-167: liquidation protocol fee </p><p>bit 168-175: eMode category </p><p>bit 176-211: unbacked mint cap in whole tokens, 0 ⇒ no cap </p><p>bit 212-251: debt ceiling for isolation mode with decimals </p><p>bit 252-255: unused</p> |
| liquidityIndex              | `uint128`   | yield generated by reserve during time interval since lastUpdatedTimestamp. Expressed in ray                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| currentLiquidityRate        | `uint128`   | current supply rate. Expressed in ray                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| variableBorrowIndex         | `uint128`   | yield accrued by reserve during time interval since lastUpdatedTimestamp. Expressed in ray                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| currentVariableBorrowRate   | `uint128`   | current variable borrow rate. Expressed in ray                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| currentStableBorrowRate     | `uint128`   | current stable borrow rate. Expressed in ray                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| lastUpdateTimestamp         | `uint40`    | timestamp of when reserve data was last updated. Used for yield calculation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| id                          | `uint16`    | reserve’s position in the list of active reserves.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| assetType                   | `AssetType` | <p>0: ERC20<br>1: ERC721<br>2: ERC1155</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| xTokenAddress               | `address`   | address of associated PToken or NToken                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| stableDebtTokenAddress      | `address`   | address of associated stable debt token                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| variableDebtTokenAddress    | `address`   | address of associated variable debt token                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| interestRateStrategyAddress | `address`   | address of interest rate strategy.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| accruedToTreasury           | `uint128`   | the current treasury balance (scaled)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### getReservesList

`function getReservesList()`

Returns the list of initialized reserves.

### getReserveAddressById

`function getReserveAddressById(uint16 id)`

Returns the address of the underlying asset of a reserve by the reserve id as stored in the DataTypes.ReserveData struct

#### Call Params

| Name | Type     | Description                                                         |
| ---- | -------- | ------------------------------------------------------------------- |
| id   | `uint16` | The id of the reserve as stored in the DataTypes.ReserveData struct |

#### Return Value

| Type    | Description                                   |
| ------- | --------------------------------------------- |
| address | The address of the reserve associated with id |

### ADDRESSES\_PROVIDER

`function ADDRESSES_PROVIDER()`

Returns the PoolAddressesProvider connected to this contract.

#### Return Value

| Type    | Description                              |
| ------- | ---------------------------------------- |
| address | The address of the PoolAddressesProvider |

### MAX\_STABLE\_RATE\_BORROW\_SIZE\_PERCENT

`function MAX_STABLE_RATE_BORROW_SIZE_PERCENT()`

Returns the percentage of available liquidity that can be borrowed at once at stable rate.

#### Return Value

| Type    | Description                                                       |
| ------- | ----------------------------------------------------------------- |
| uint256 | The percentage of available liquidity to borrow, expressed in bps |

### MAX\_NUMBER\_RESERVES

`function MAX_NUMBER_RESERVES()`

Returns the maximum number of reserves supported to be listed in this Pool.

#### Return Value

| Type   | Description                              |
| ------ | ---------------------------------------- |
| uint16 | The maximum number of reserves supported |

## Write Functions

### flashClaim

`function flashClaim(address receiverAddress, address nftAsset, uint256[] calldata nftTokenIds, bytes calldata params) external`

Allows smart contracts to access the tokens within one transaction, as long as the tokens taken is returned.

#### Call Params

| Name            | Type        | Description                                                                                      |
| --------------- | ----------- | ------------------------------------------------------------------------------------------------ |
| receiverAddress | `address`   | The address of the contract receiving the tokens, implementing the IFlashClaimReceiver interface |
| nftAsset        | `address`   | address of the underlying asset of NFT                                                           |
| nftTokenIds     | `uint256[]` | token ids of the underlying asset                                                                |
| params          | `bytes`     | Variadic packed params to pass to the receiver as extra information                              |

### supply

`function supply(address asset, uint256 amount, address onBehalfOf, uint16 referralCode) external`

The `referralCode` is emitted in Supply event and can be for third party referral integrations.

#### Call Params

| Name         | Type      | Description                                                                                                                                        |
| ------------ | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| asset        | `address` | address of the asset being supplied to the pool.                                                                                                   |
| amount       | `uint256` | amount of asset being supplied.                                                                                                                    |
| onBehalfOf   | `address` | <p>address that will receive the corresponding pTokens.<br><br>Note: only the onBehalfOf address will be able to withdraw asset from the pool.</p> |
| referralCode | `uint16`  | <p>unique code for 3rd party referral program integration. </p><p></p><p>Use 0 for no referral.</p>                                                |

### supplyERC721

`function supplyERC721(address asset, DataTypes.ERC721SupplyParams[] calldata tokenData, address onBehalfOf, uint16 referralCode) external`

Supplies multiple `tokenIds` of underlying ERC721 asset into the reserve, receiving in return overlying nTokens.

#### Call Params

| Name         | Type                   | Description                                                                                                                                                                                                                 |
| ------------ | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| asset        | `address`              | The address of the underlying asset to supply                                                                                                                                                                               |
| tokenData    | `ERC721SupplyParams[]` | <p>The list of tokenIds and their collateral configs to be supplied.<br><br><code>struct ERC721SupplyParams {</code> <br>  <code>uint256 tokenId;</code> <br>  <code>bool useAsCollateral;</code> <br><code>}</code></p>    |
| onBehalfOf   | `address`              | address that will receive the The address that will receive the xTokens, same as msg.sender if the user wants to receive them on his own wallet, or a different address if the beneficiary of xTokens is a different wallet |
| referralCode | `uint16`               | Code used to register the integrator originating the operation, for potential rewards. 0 if the action is executed directly by the user, without any middle-man                                                             |

### supplyWithPermit

`function supplyWithPermit(address asset, uint256 amount, address onBehalfOf, uint16 referralCode, uint256 deadline, uint8 permitV, permitR, bytes32 permitS)`

Supply with transfer approval of supplied asset via permit function. This method removes the need for separate approval tx before supplying asset to the pool.

#### Call Params

| Name         | Type      | Description                                                                                  |
| ------------ | --------- | -------------------------------------------------------------------------------------------- |
| asset        | `address` | Address of underlying asset being supplied. Same asset as used in permit s,v,r               |
| amount       | `uint256` | Amount of asset to be supplied and signed for approval. Same amount as used in permit s,v,r  |
| onBehalfOf   | `address` | Address that will receive the pTokens.                                                       |
| referralCode | `uint16`  | <p>unique code for 3rd party referral program integration.<br><br>Use 0 for no referral.</p> |
| deadline     | `uint256` | unix timestamp up-till which signature will be valid                                         |
| permitV      | `uint8`   | Signature parameter v                                                                        |
| permitR      | `bytes32` | Signature parameter r                                                                        |
| permitS      | `bytes32` | Signature parameter s                                                                        |

### withdraw

`function withdraw(address asset, uint256 amount, address to)`

Withdraws `amount` of the underlying `asset`, i.e. redeems the underlying token and burns the pTokens.

If user has any existing debt backed by the underlying token, then the max _amount_ available to withdraw is the _amount_ that will not leave user health factor < 1 after withdrawal.

#### Call Params

| Name   | Type      | Description                                                                                   |
| ------ | --------- | --------------------------------------------------------------------------------------------- |
| asset  | `address` | address of the underlying asset, not the pToken                                               |
| amount | `uint256` | amount deposited, expressed in wei units. Use `type(uint).max` to withdraw the entire balance |
| to     | `address` | address that will receive the `asset`                                                         |

#### Return Value

| Type    | Description                |
| ------- | -------------------------- |
| uint256 | The final amount withdrawn |

### withdrawERC721

`function withdraw(address asset, uint256[] calldata tokenIds, address to)`

Withdraws multiple `tokenIds` of underlying ERC721 asset from the reserve, burning the equivalent nTokens owned.

#### Call Params

| Name     | Type        | Description                                     |
| -------- | ----------- | ----------------------------------------------- |
| asset    | `address`   | address of the underlying asset, not the nToken |
| tokenIds | `uint256[]` | The underlying tokenIds to be withdrawn.        |
| to       | `address`   | address that will receive the `asset`           |

#### Return Value

| Type    | Description                |
| ------- | -------------------------- |
| uint256 | The final amount withdrawn |

### borrow

`function borrow(address asset, uint256 amount, uint256 interestRateMode, uint16 referralCode, address onBehalfOf)`

Borrows `amount` of `asset` with `interestRateMode`, sending the `amount` to `msg.sender`, with the debt being incurred by `onBehalfOf`.

#### Call Params

| Name             | Type      | Description                                                                                                           |
| ---------------- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| asset            | `address` | address of the underlying asset                                                                                       |
| amount           | `uint256` | amount to be borrowed, expressed in wei units                                                                         |
| interestRateMode | `uint256` | <p>the type of borrow debt.<br><br>Stable: 1, Variable: 2</p>                                                         |
| referralCode     | `uint16`  | referral code for our referral program. Use 0 for no referral code.                                                   |
| onBehalfOf       | `address` | <p>address of user who will incur the debt.<br><br>Use msg.sender when not calling on behalf of a different user.</p> |

### repay

`function repay(address asset, uint256 amount, uint256 rateMode, address onBehalfOf)`

Repays `onBehalfOf`'s debt `amount` of `asset` which has a `rateMode`.

#### Call Params

| Name       | Type      | Description                                                                                                                                                                                                                                                                                              |
| ---------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| asset      | `address` | address of the underlying asset                                                                                                                                                                                                                                                                          |
| amount     | `uint256` | <p>amount to be repaid, expressed in wei units.<br>Use uint(-1) to repay the entire debt, ONLY when the repayment is not executed on behalf of a 3rd party.<br>In case of repayments on behalf of another user, it's recommended to send an _amount slightly higher than the current borrowed amount</p> |
| rateMode   | `uint256` | <p>the type of debt being repaid.<br><br>Stable: 1, Variable: 2</p>                                                                                                                                                                                                                                      |
| onBehalfOf | `address` | <p>address of user who will incur the repaid debt.<br><br>Use msg.sender when not calling on behalf of a different user.</p>                                                                                                                                                                             |

#### Return Value

| Type    | Description             |
| ------- | ----------------------- |
| uint256 | The final amount repaid |

### repayWithPermit

`function repayWithPermit(address asset, uint256 amount, uint256 interestRateMode, address onBehalfOf, uint256 deadline, uint8 permitV, permitR, bytes32 permitS)`

Repay with transfer approval of borrowed asset via permit function. This method removes the need for separate approval tx before repaying asset to the pool.

#### Call Params

| Name             | Type      | Description                                                                               |
| ---------------- | --------- | ----------------------------------------------------------------------------------------- |
| asset            | `address` | Address of underlying asset being repaid. Same asset as used in permit s,v,r              |
| amount           | `uint256` | Amount of asset to be repaid and signed for approval. Same amount as used in permit s,v,r |
| interestRateMode | `uint256` | <p>the type of debt being repaid.<br>Stable: 1, Variable: 2</p>                           |
| onBehalfOf       | `address` | Address that will receive the pTokens.                                                    |
| deadline         | `uint256` | unix timestamp up-till which signature will be valid                                      |
| permitV          | `uint8`   | Signature parameter v                                                                     |
| permitR          | `bytes32` | Signature parameter r                                                                     |
| permitS          | `bytes32` | Signature parameter s                                                                     |

#### Return Value

| Type    | Description             |
| ------- | ----------------------- |
| uint256 | The final amount repaid |

### repayWithPTokens

`function repayWithATokens(address asset,uint256 amount,uint256 interestRateMode)`

Allows user to repay with _pTokens_ of the underlying debt asset without any approvals eg. Pay DAI debt using pDAI tokens.

#### Call Params

| Name             | Type      | Description                                                                                           |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------- |
| asset            | `address` | Address of the underlying asset to be repaid                                                          |
| amount           | `uint256` | <p>Amount of underlying asset being repaid.<br>Use uint256(-1) to pay without leaving pToken dust</p> |
| interestRateMode | `uint256` | <p>Interest rate mode of the debt position<br><br>Stable: 1, Variable: 2</p>                          |

#### Return Value

| Type    | Description             |
| ------- | ----------------------- |
| uint256 | The final amount repaid |

### swapBorrowRateMode

`function swapBorrowRateMode(address asset, uint256 interestRateMode)`

Swaps msg.sender's borrow rate mode between stable and variable.

#### Call Params

| Name             | Type      | Description                                                                   |
| ---------------- | --------- | ----------------------------------------------------------------------------- |
| asset            | `address` | address of the underlying asset                                               |
| interestRateMode | `uint256` | <p>the rate mode the user is swapping from.<br><br>Stable: 1, Variable: 2</p> |

### rebalanceStableBorrowRate

`function rebalanceStableBorrowRate(address asset, address user)`

Rebalances stable borrow rate of the `user` for given `asset`. In case of liquidity crunches on the protocol, stable rate borrows might need to be rebalanced to bring back equilibrium between the borrow and supply rates.

#### Call Params

| Name  | Type      | Description                                                                                        |
| ----- | --------- | -------------------------------------------------------------------------------------------------- |
| asset | `address` | Address of the underlying token that has been borrowed for which the position is being rebalanced. |
| user  | `address` | Address of the user being rebalanced.                                                              |

### setUserUseReserveAsCollateral

`function setUserUseReserveAsCollateral(address asset, bool useAsCollateral)`

Sets the `asset` of `msg.sender` to be used as collateral or not.

#### Call Params

| Name            | Type      | Description                                              |
| --------------- | --------- | -------------------------------------------------------- |
| asset           | `address` | address of the underlying asset to be used as collateral |
| useAsCollateral | `bool`    | `true` if the asset should be used as collateral         |

### setUserUseERC721AsCollateral

`function setUserUseERC721AsCollateral(address asset, uint256 tokenId, bool useAsCollateral)`

Allows suppliers to enable/disable a specific supplied ERC721 asset with a tokenID as collateral.

#### Call Params

| Name            | Type      | Description                                              |
| --------------- | --------- | -------------------------------------------------------- |
| asset           | `address` | address of the underlying asset to be used as collateral |
| tokenId         | `uint256` | the id of the supplied ERC721 token                      |
| useAsCollateral | `bool`    | `true` if the asset should be used as collateral         |

### liquidationCall

`function liquidationCall(address collateralAsset, address debtAsset, address user, uint256 debtToCover, bool receivePToken)`

Liquidates ERC20 position. For more information please see the [docs](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/liquidation#erc20-liquidation).

#### Call Params

| Name            | Type      | Description                                                                                                                               |
| --------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| collateralAsset | `address` | address of the collateral reserve                                                                                                         |
| debtAsset       | `address` | address of the debt reserve                                                                                                               |
| user            | `address` | address of the borrower                                                                                                                   |
| debtToCover     | `uint256` | amount of asset debt that the liquidator will repay                                                                                       |
| receivePToken   | `bool`    | if true, the user receives the pTokens equivalent of the purchased collateral. If false, the user receives the underlying asset directly. |

### liquidationERC721

`function liquidationERC721Call(address collateralAsset, address liquidationAsset, address user, uint256 collateralTokenId, uint256 liquidationAmount, bool receiveNToken)`

Liquidates ERC721 position. For more information please see the [docs](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/liquidation#erc721-liquidation).

#### Call Params

| Name              | Type      | Description                                                                                                                                   |
| ----------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| collateralAsset   | `address` | address of the collateral reserve                                                                                                             |
| liquidationAsset  | `address` | address of the asset used for liquidation                                                                                                     |
| user              | `address` | address of the borrower                                                                                                                       |
| collateralTokenId | `uint256` | the id of the NFT to liquidate                                                                                                                |
| liquidationAmount | `uint256` | amount to liquidate with                                                                                                                      |
| receiveNToken     | `bool`    | if `true`, the user receives the nTokens equivalent of the purchased collateral. If `false`, the user receives the underlying asset directly. |

### initReserve

`function initReserve(address asset, DataTypes.AssetType assetType, address xTokenAddress, address stableDebtAddress, address variableDebtAddress, address interestRateStrategyAddress`

Initializes a reserve, activating it, assigning an xToken and debt tokens and an interest rate strategy. Only callable by the PoolConfigurator contract.

#### Call Params

| Name                        | Type        | Description                                                                                                                                                |
| --------------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| asset                       | `address`   | The address of the underlying asset of the reserve                                                                                                         |
| assetType                   | `AssetType` | <p>The type of asset<br><code>enum AssetType {</code> <br>  <code>ERC20,</code><br>  <code>ERC721,</code><br>  <code>ERC1155</code> <br><code>}</code></p> |
| xTokenAddress               | `address`   | The address of the xToken that will be assigned to the reserve                                                                                             |
| stableDebtAddress           | `address`   | The address of the StableDebtToken that will be assigned to the reserve                                                                                    |
| variableDebtAddress         | `address`   | The address of the VariableDebtToken that will be assigned to the reserve                                                                                  |
| interestRateStrategyAddress | `address`   | The address of the interest rate strategy contract                                                                                                         |

### dropReserve

`function dropReserve(address asset)`

Drop a reserve. Only callable by the PoolConfigurator contract.

#### Call Params

| Name  | Type      | Description                                        |
| ----- | --------- | -------------------------------------------------- |
| asset | `address` | The address of the underlying asset of the reserve |

### setReserveInterestRateStrategyAddress

`function setReserveInterestRateStrategyAddress(address asset, address rateStrategyAddress) external`

Updates the address of the interest rate strategy contract. Only callable by the PoolConfigurator contract.

#### Call Params

| Name                | Type      | Description                                        |
| ------------------- | --------- | -------------------------------------------------- |
| asset               | `address` | The address of the underlying asset of the reserve |
| rateStrategyAddress | `address` | The address of the interest rate strategy contract |

### setConfiguration

`function setConfiguration(address asset, DataTypes.ReserveConfigurationMap calldata configuration) external`

#### Call Params

| Name          | Type                      | Description                                        |
| ------------- | ------------------------- | -------------------------------------------------- |
| asset         | `address`                 | The address of the underlying asset of the reserve |
| configuration | `ReserveConfigurationMap` | The new configuration bitmap                       |

### finalizeTransfer

`function finalizeTransfer(address asset, address from, address to, bool usedAsCollateral, uint256 amount, uint256 balanceFromBefore, uint256 balanceToBefore) external`

Validates and finalizes an xToken transfer. Only callable by the overlying xToken of the `asset`

#### Call Params

| Name              | Type      | Description                                               |
| ----------------- | --------- | --------------------------------------------------------- |
| asset             | `address` | The address of the underlying asset of the xToken         |
| from              | `address` | The user from which the xTokens are transferred           |
| to                | `address` | The user receiving the xTokens                            |
| usedAsCollateral  | `bool`    | `true` for use as collateral                              |
| amount            | `uint256` | The amount being transferred/withdrawn                    |
| balanceFromBefore | `uint256` | The xToken balance of the `from` user before the transfer |
| balanceToBefore   | `uint256` | The xToken balance of the `to` user before the transfer   |

### mintToTreasury

`function mintToTreasury(address[] calldata assets) external`

Mints reserve income accrued to treasury (as per the reserve factor) for the given list of assets.

#### Call Params

| Name  | Type        | Description                                       |
| ----- | ----------- | ------------------------------------------------- |
| asset | `address[]` | List of assets for which accrued income is minted |

### rescueTokens

`function rescueTokens(address token, address to, uint256 amount) external`

Rescue and transfer tokens locked in this contract.
