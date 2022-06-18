# PoolAddressesProvider

Addresses register of the protocol for a particular market. This contract is immutable and the address will never change.

## Events

### MarketIdSet

`event MarketIdSet(string indexed oldMarketId, string indexed newMarketId)`

Emitted when the market identifier is updated.

#### Call Params

| Name        | Type     | Description              |
| ----------- | -------- | ------------------------ |
| oldMarketId | `string` | The old id of the market |
| newMarketId | `string` | The new id of the market |

### PoolUpdated

`event PoolUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the pool is updated.

#### Call Params

| Name       | Type      | Description                 |
| ---------- | --------- | --------------------------- |
| oldAddress | `address` | The old address of the Pool |
| newAddress | `address` | The new address of the Pool |

### PoolConfiguratorUpdated

`event PoolConfiguratorUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the pool configurator is updated.

#### Call Params

| Name       | Type      | Description                             |
| ---------- | --------- | --------------------------------------- |
| oldAddress | `address` | The old address of the PoolConfigurator |
| newAddress | `address` | The new address of the PoolConfigurator |

### PriceOracleUpdated

`event PriceOracleUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the price oracle is updated.

#### Call Params

| Name       | Type      | Description                        |
| ---------- | --------- | ---------------------------------- |
| oldAddress | `address` | The old address of the PriceOracle |
| newAddress | `address` | The new address of the PriceOracle |

### ACLManagerUpdated

`event ACLManagerUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the ACL manager is updated.

#### Call Params

| Name       | Type      | Description                       |
| ---------- | --------- | --------------------------------- |
| oldAddress | `address` | The old address of the ACLManager |
| newAddress | `address` | The new address of the ACLManager |

### ACLAdminUpdated

`event ACLAdminUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the ACL admin is updated.

#### Call Params

| Name       | Type      | Description                     |
| ---------- | --------- | ------------------------------- |
| oldAddress | `address` | The old address of the ACLAdmin |
| newAddress | `address` | The new address of the ACLAdmin |

### PriceOracleSentinelUpdated

`event PriceOracleSentinelUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the price oracle sentinel is updated.

#### Call Params

| Name       | Type      | Description                                |
| ---------- | --------- | ------------------------------------------ |
| oldAddress | `address` | The old address of the PriceOracleSentinel |
| newAddress | `address` | The new address of the PriceOracleSentinel |

### PoolDataProviderUpdated

`event PoolDataProviderUpdated(address indexed oldAddress, address indexed newAddress)`

Emitted when the pool data provider is updated.

#### Call Params

| Name       | Type      | Description                             |
| ---------- | --------- | --------------------------------------- |
| oldAddress | `address` | The old address of the PoolDataProvider |
| newAddress | `address` | The new address of the PoolDataProvider |

### ProxyCreated

`event ProxyCreated(bytes32 indexed id, address indexed proxyAddress, address indexed implementationAddress)`

Emitted when a new proxy is created.

#### Call Params

| Name                  | Type      | Description                                |
| --------------------- | --------- | ------------------------------------------ |
| id                    | `bytes32` | The identifier of the proxy                |
| proxyAddress          | `address` | The address of the created proxy contract  |
| implementationAddress | `address` | The address of the implementation contract |

### AddressSet

`event AddressSet(bytes32 indexed id, address indexed oldAddress, address indexed newAddress)`

Emitted when a new non-proxied contract address is registered.

#### Call Params

| Name       | Type      | Description                     |
| ---------- | --------- | ------------------------------- |
| id         | `bytes32` | The identifier of the contract  |
| oldAddress | `address` | The address of the old contract |
| newAddress | `address` | The address of the new contract |

### AddressSetAsProxy

`event AddressSetAsProxy(bytes32 indexed id, address indexed proxyAddress, address oldImplementationAddress, address indexed newImplementationAddress)`

Emitted when the implementation of the proxy registered with id is updated

#### Call Params

| Name                     | Type      | Description                                    |
| ------------------------ | --------- | ---------------------------------------------- |
| id                       | `bytes32` | The identifier of the contract                 |
| proxyAddress             | `address` | The address of the proxy contract              |
| oldImplementationAddress | `address` | The address of the old implementation contract |
| newImplementationAddress | `address` | The address of the new implementation contract |

## Read Functions

### getMarketId

`function getMarketId() external view returns (string memory)`

Fetch the market id of the associated Aave market.

#### Return Value

| Type   | Description                           |
| ------ | ------------------------------------- |
| string | A string representation of the market |

### getAddress

`function getAddress(bytes32 id) external view returns (address)`

Fetch the address of protocol contract stored at given id.

#### Call Params

| Name | Type      | Description                                         |
| ---- | --------- | --------------------------------------------------- |
| id   | `bytes32` | id. Example, the Protocol Data Provider uses id 0x1 |

#### Return Value

| Type    | Description                                       |
| ------- | ------------------------------------------------- |
| address | The address associated with the bytes32 id passed |

### getPool

`function getPool() external view returns (address)`

Fetch the contract of latest pool

#### Return Value

| Type    | Description                        |
| ------- | ---------------------------------- |
| address | The address of the associated Pool |

### getPoolConfigurator

`function getPoolConfigurator() external view returns (address)`

Fetch the `PoolConfigurator` is used for configuration methods, like init reserves or update token implementation etc, of the market.

#### Return Value

| Type    | Description                                         |
| ------- | --------------------------------------------------- |
| address | The address of associated market’s PoolConfigurator |

### getPriceOracle

`function getPriceOracle() external view returns (address)`

Fetch Price Oracle used by the market.

#### Return Value

| Type    | Description                                                |
| ------- | ---------------------------------------------------------- |
| address | The address of the price oracle used by associated market. |

### getACLManager

`function getACLManager() external view returns (address)`

Fetch ACLManger that manages the system role of the market

#### Return Value

| Type    | Description                                                                              |
| ------- | ---------------------------------------------------------------------------------------- |
| address | The address of the ACLManger contract managing the system role of the associated market. |

### getACLAdmin

`function getACLAdmin() external view returns (address)`

Fetch ACLAdmin of the market which holds the `DEFAULT_ADMIN_ROLE` in ACLManager.

#### Return Value

| Type    | Description                                                            |
| ------- | ---------------------------------------------------------------------- |
| address | The address of the access control list admin of the associated market. |

### getPriceOracleSentinel

`function getPriceOracleSentinel() external view returns (address)`

#### Return Value

| Type    | Description                                                        |
| ------- | ------------------------------------------------------------------ |
| address | The address of the Price oracle sentinel of the associated market. |

### getPoolDataProvider

`function getPoolDataProvider() external view returns (address)`&#x20;

Fetch address of latest pool data provider.

#### Return Value

| Type    | Description                                                     |
| ------- | --------------------------------------------------------------- |
| address | The address of the pool data provider of the associated market. |

## Write Functions

### setMarketId

`function setMarketId(string calldata newMarketId) external`

Updates the identifier of the Aave market.

#### Call Params

| Name        | Type     | Description              |
| ----------- | -------- | ------------------------ |
| newMarketId | `string` | The new id of the market |

### setAddress

`function setAddress(bytes32 id, address newAddress) external`

Sets the address of protocol contract stored at given id.

#### Call Params

| Name       | Type      | Description                                              |
| ---------- | --------- | -------------------------------------------------------- |
| id         | `bytes32` | keccak256 hash of UTF8Bytes string representing Contract |
| newAddress | `address` | The new address to be set corresponding to the `id`      |

### setAddressAsProxy

`function setAddressAsProxy(bytes32 id, address newImplementationAddress) external`

Sets/updates the implementation address of a specific proxied protocol contract.

#### Call Params

| Name                     | Type      | Description                                                           |
| ------------------------ | --------- | --------------------------------------------------------------------- |
| id                       | `bytes32` | id of Proxy contract                                                  |
| newImplementationAddress | `address` | The address of new implementation contract corresponding to the proxy |

### setPoolImpl

`function setPoolImpl(address newPoolImpl) external`

Sets/update the implementation of the POOL proxy contract.

#### Call Params

| Name        | Type      | Description                                     |
| ----------- | --------- | ----------------------------------------------- |
| newPoolImpl | `address` | The address of new Pool implementation contract |

### setPoolConfiguratorImpl

`function setPoolConfiguratorImpl(address newPoolConfiguratorImpl) external`

Sets/updates the implementation of the POOL\_CONFIGURATOR proxy contract.

#### Call Params

| Name                    | Type      | Description                                                 |
| ----------------------- | --------- | ----------------------------------------------------------- |
| newPoolConfiguratorImpl | `address` | The address of new PoolConfigurator implementation contract |

### setPriceOracle

`function setPriceOracle(address newPriceOracle) external`

Sets/updates address of the PriceOracle contract.

#### Call Params

| Name           | Type      | Description                             |
| -------------- | --------- | --------------------------------------- |
| newPriceOracle | `address` | The address of new PriceOracle contract |

### setACLManager

`function setACLManager(address newAclManager) external`

Sets/updates address of the ACL Manager.

#### Call Params

| Name          | Type      | Description                             |
| ------------- | --------- | --------------------------------------- |
| newAclManager | `address` | The adThe address of the new ACLManager |

### setACLAdmin

`function setACLAdmin(address newAclAdmin) external`

Sets/updates address of the AclAdmin.

#### Call Params

| Name        | Type      | Description                 |
| ----------- | --------- | --------------------------- |
| newAclAdmin | `address` | The address of new AclAdmin |

### setPriceOracleSentinel

`function setPriceOracleSentinel(address newPriceOracleSentinel) external`

Sets/updates address of the Price oracle sentinel.

#### Call Params

| Name                   | Type      | Description                            |
| ---------------------- | --------- | -------------------------------------- |
| newPriceOracleSentinel | `address` | The address of new PriceOracleSentinel |

### setPoolDataProvider

`function setPoolDataProvider(address newDataProvider) external`

Sets/updates address of PoolDataProvider.

#### Call Params

| Name            | Type      | Description                         |
| --------------- | --------- | ----------------------------------- |
| newDataProvider | `address` | The address of new PoolDataProvider |
