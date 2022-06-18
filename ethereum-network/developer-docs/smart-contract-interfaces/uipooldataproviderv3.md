# UiPoolDataProviderV3

Contract used by Aave UI to collect and pre-process Pool data.

## Data Structures

### AggregatedReserveData

View fields of `AggregatedReserveData`

### UserReserveData

| Name                            | Type      | Description                                                                            |
| ------------------------------- | --------- | -------------------------------------------------------------------------------------- |
| underlyingAsset                 | `address` | Address of the underlying asset supplied/borrowed                                      |
| scaledXTokenBalance             | `uint256` | <p>scaled balance of xToken<br><br><em>scaledBalance = balance/liquidityIndex</em></p> |
| collaterizedBalance             | `uint256` | balance of collateral                                                                  |
| usageAsCollateralEnabledOnUser  | `bool`    | `true` if supplied asset is enabled to be used as collateral                           |
| stableBorrowRate                | `uint256` | Stable rate at which underlying asset is borrowed by the user. 0 ⇒ no debt             |
| scaledVariableDebt              | `uint256` | <p>scaled balance of vToken<br><br><em>scaledBalance = balance/liquidityIndex</em></p> |
| principalStableDebt             | `uint256` | Principal amount borrowed at stable rate                                               |
| stableBorrowLastUpdateTimestamp | `uint256` | unix timestamp of last update on user’s stable borrow position.                        |

### BaseCurrencyInfo

| Name                              | Type      | Description                                        |
| --------------------------------- | --------- | -------------------------------------------------- |
| marketReferenceCurrencyUnit       | `uint256` | Reference aka base currency of the Parallel market |
| marketReferenceCurrencyPriceInUsd | `int256`  | Price of reference aka base currency in USD        |
| networkBaseTokenPriceInUsd        | `int256`  | Price of native token of the network/chain in USD  |
| networkBaseTokenPriceDecimals     | `uint8`   | Decimals of native token of the network/chain      |

## Read Functions

### getReservesList

`function getReservesList(IPoolAddressesProvider provider)`

Returns the list of initialized reserves in the Pool associated with the given provider.

### getReservesData

`function getReservesData(IPoolAddressesProvider provider)`

Returns `BaseCurrencyInfo` of the Pool and `AggregatedReserveData[]` for all the initialized reserves in the Pool associated with the given provider.

### getUserReservesData

`function getUserReservesData(IPoolAddressesProvider provider, address user)`

Returns `UserReserveData[]` for all user reserves in the Pool associated with the given provider.

### getNTokenData

`function getNTokenData(address user, address[] memory nTokenAddresses, uint256[][] memory tokenIds)`

Returns `ERC721SupplyParams[][]` for associated nTokenAddresses and tokenIds.
