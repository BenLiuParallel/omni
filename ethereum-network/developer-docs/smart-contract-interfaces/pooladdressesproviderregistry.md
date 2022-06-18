# PoolAddressesProviderRegistry

A register of the active `[PoolAddressesProvider](./pooladdressesprovider.md)` contracts, covering all markets. This contract is immutable and the address will never change.

## Events

### AddressProviderRegistered

`event AddressesProviderRegistered(address indexed addressesProvider, uint256 indexed id)`

Emitted when a new AddressesProvider is registered.

#### Call Params

| Name              | Type      | Description                                         |
| ----------------- | --------- | --------------------------------------------------- |
| addressesProvider | `address` | The address of the registered PoolAddressesProvider |
| id                | `uint256` | The id of the registered PoolAddressesProvider      |

### AddressesProviderUnregistered

`event AddressesProviderUnregistered(address indexed addressesProvider, uint256 indexed id)`

Emitted when an AddressesProvider is unregistered.

#### Call Params

| Name              | Type      | Description                                           |
| ----------------- | --------- | ----------------------------------------------------- |
| addressesProvider | `address` | The address of the unregistered PoolAddressesProvider |
| id                | `uint256` | The id of the unregistered PoolAddressesProvider      |

## Read Functions

### getAddressesProvidersList

`function getAddressesProvidersList() external view returns (address[] memory)`

Returns a list of active PoolAddressesProvider contracts for the registered protocol markets.

#### Return Value

| Type       | Description                          |
| ---------- | ------------------------------------ |
| address\[] | List of active PoolAddressesProvider |

### getAddressesProviderIdByAddress

`function getAddressesProviderIdByAddress(address addressesProvider) external view returns (uint256)`

Returns the id of a registered `PoolAddressesProvider`.

#### Call Params

| Name              | Type      | Description                          |
| ----------------- | --------- | ------------------------------------ |
| addressesProvider | `address` | Address of the PoolAddressesProvider |

#### Return Value

| Type    | Description                                                                                       |
| ------- | ------------------------------------------------------------------------------------------------- |
| uint256 | Id of the associated PoolAddressesProvider. 0 indicates not a valid PoolAddressesProvider address |

### getAddressesProviderAddressById

`function getAddressesProviderAddressById(uint256 id) external view returns (address)`

Returns the address of a registered `PoolAddressesProvider`.

#### Call Params

| Name | Type      | Description                   |
| ---- | --------- | ----------------------------- |
| id   | `uint256` | Id of the PoolAddressProvider |

#### Return Value

| Type    | Description                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------- |
| address | address of the PoolAddressesProvider with the given id or zero address if it is not registered |

## Write Functions

### registerAddressesProvider

`function registerAddressesProvider(address provider, uint256 id) external`

Registers an addresses provider. The PoolAddressesProvider must not already be registered in the registry. The id must not be used by an already registered PoolAddressesProvider.

#### Call Params

| Name     | Type      | Description                                                                      |
| -------- | --------- | -------------------------------------------------------------------------------- |
| provider | `address` | The address of the new PoolAddressesProvider                                     |
| id       | `uint256` | The id for the new PoolAddressesProvider, referring to the market it belongs to. |

### unregisterAddressesProvider

`function unregisterAddressesProvider(address provider) external`

Removes an addresses provider from the list of registered addresses providers.

#### Call Params

| Name     | Type      | Description                       |
| -------- | --------- | --------------------------------- |
| provider | `address` | The PoolAddressesProvider address |
