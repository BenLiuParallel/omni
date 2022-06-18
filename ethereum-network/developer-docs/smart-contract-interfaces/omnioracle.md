# OmniOracle

## Events

### BaseCurrencySet

`event BaseCurrencySet(address indexed baseCurrency, uint256 baseCurrencyUnit)`

Emitted after the base currency is set.

#### Call Params

| Name             | Type      | Description                                |
| ---------------- | --------- | ------------------------------------------ |
| baseCurrency     | `address` | The base currency of used for price quotes |
| baseCurrencyUnit | `uint256` | The unit of the base currency              |

### AssetSourceUpdated

`event AssetSourceUpdated(address indexed asset, address indexed source)`

Emitted after the price source of an asset is updated.

#### Call Params

| Name   | Type      | Description                   |
| ------ | --------- | ----------------------------- |
| asset  | `address` | The address of the asset      |
| source | `address` | The price source of the asset |

### FallbackOracleUpdated

`event FallbackOracleUpdated(address indexed fallbackOracle)`

Emitted after the address of fallback oracle is updated.

#### Call Params

| Name           | Type      | Description                        |
| -------------- | --------- | ---------------------------------- |
| fallbackOracle | `address` | The address of the fallback oracle |

## Read Functions

### ADDRESSES\_PROVIDER

`function ADDRESSES_PROVIDER()`

Returns the PoolAddressesProvider.

#### Return Value

| Type    | Description                                       |
| ------- | ------------------------------------------------- |
| address | The address of the PoolAddressesProvider contract |

### getAssetsPrices

`function getAssetsPrices(address[] calldata assets)`

Returns a list of prices from a list of assets addresses.

#### Call Params

| Name   | Type      | Description                  |
| ------ | --------- | ---------------------------- |
| assets | `address` | The list of assets addresses |

#### Return Value

| Type       | Description                    |
| ---------- | ------------------------------ |
| address\[] | The prices of the given assets |

### getSourceOfAsset

`function getSourceOfAsset(address asset) external view returns (address)`

Returns the address of the source for an asset address.

#### Call Params

| Name   | Type      | Description              |
| ------ | --------- | ------------------------ |
| assets | `address` | The address of the asset |

#### Return Value

| Type    | Description               |
| ------- | ------------------------- |
| address | The address of the source |

### getFallbackOracle

`function getFallbackOracle() external view returns (address)`

The address of the fallback oracle.

#### Return Value

| Type    | Description                        |
| ------- | ---------------------------------- |
| address | The address of the fallback oracle |

## Write Functions

### setAssetSources

`function setAssetSources(address[] calldata assets, address[] calldata sources) external`

Sets or replaces price sources of assets.

#### Call Params

| Name    | Type        | Description                        |
| ------- | ----------- | ---------------------------------- |
| assets  | `address[]` | The addresses of the assets        |
| sources | `address[]` | The addresses of the price sources |

### setFallbackOracle

`function setFallbackOracle(address fallbackOracle) external`

Sets the fallback oracle.

#### Call Params

| Name           | Type      | Description                        |
| -------------- | --------- | ---------------------------------- |
| fallbackOracle | `address` | The address of the fallback oracle |
