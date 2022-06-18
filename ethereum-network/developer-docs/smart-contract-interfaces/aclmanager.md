# ACLManager

_**Access Control List Manager**_ is the main registry of system roles and permissions.

ACLManager allows a _**Role Admin**_ to manage roles. _**Role Admin**_ is itself a role that is managed by the `DEFAULT_ADMIN_ROLE`.

`DEFAULT_ADMIN_ROLE` is held by the _ACLAdmin,_ which is initialized in `PoolAddressesProvider`

## Read Functions

### ADDRESSES\_PROVIDER

`function ADDRESSES_PROVIDER() external view returns (IPoolAddressesProvider)`

Returns the contract address of the PoolAddressesProvider.

### POOL\_ADMIN\_ROLE

`function POOL_ADMIN_ROLE() external view returns (bytes32)`

Returns the identifier of the PoolAdmin role.

### EMERGENCY\_ADMIN\_ROLE

`function EMERGENCY_ADMIN_ROLE() external view returns (bytes32)`

Returns the identifier of the EmergencyAdmin role.

### RISK\_ADMIN\_ROLE

`function RISK_ADMIN_ROLE() external view returns (bytes32)`

Returns the identifier of the RiskAdmin role.

### FLASH\_BORROWER\_ROLE

`function FLASH_BORROWER_ROLE() external view returns (bytes32)`

Returns the identifier of the FlashBorrower role.

### BRIDGE\_ROLE

`function BRIDGE_ROLE() external view returns (bytes32)`

Returns the identifier of the Bridge role.

### ASSET\_LISTING\_ADMIN\_ROLE

`function ASSET_LISTING_ADMIN_ROLE() external view returns (bytes32)`

Returns the identifier of the AssetListingAdmin role.

### isPoolAdmin

`function isPoolAdmin(address admin) external view returns (bool)`

Returns true if the address is PoolAdmin, false otherwise.

### isEmergencyAdmin

`function isEmergencyAdmin(address admin) external view returns (bool)`

Returns true if the address is EmergencyAdmin, false otherwise.

### isRiskAdmin

`function isRiskAdmin(address admin) external view returns (bool)`

Returns true if the address is RiskAdmin, false otherwise.

### isFlashBorrower

`function isFlashBorrower(address borrower) external view returns (bool)`

Returns true if the address is FlashBorrower, false otherwise.

### isBridge

`function isBridge(address bridge) external view returns (bool)`

Returns true if the address is Bridge, false otherwise.

### isAssetListingAdmin

`function isAssetListingAdmin(address admin) external view returns (bool)`

Returns true if the address is AssetListingAdmin, false otherwise.

## Write Functions

### setRoleAdmin

`function setRoleAdmin(bytes32 role, bytes32 adminRole) external`

Setup admin to manage Roles.

#### Call Params

| Name      | Type      | Description                                                                                                                                                                             |
| --------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| role      | `bytes32` | <p>keccak256 hash of one of the following:</p><ul><li>POOL_ADMIN</li><li>EMERGENCY_ADMIN</li><li>RISK_ADMIN</li><li>FLASH_BORROWER</li><li>BRIDGE</li><li>ASSET_LISTING_ADMIN</li></ul> |
| adminRole | `bytes32` | adminRole responsible for role. 0x00 is reserved for DEFAULT\_ADMIN\_ROLE                                                                                                               |

### addPoolAdmin

`function addPoolAdmin(address admin) external`

Add address to the list of members in `POOL_ADMIN` role. Holders of this role can update token implementations, drop, (un)pause and (de)activate reserves, update premiums and do everything the `ASSET_LISTING_ADMIN` and `RISK_ADMIN` can do.

#### Call Params

| Name  | Type      | Description                                     |
| ----- | --------- | ----------------------------------------------- |
| admin | `address` | address which will be granted POOL\_ADMIN role. |

### removePoolAdmin

`function removePoolAdmin(address admin) external`

Remove given address from the list of members in `POOL_ADMIN` role.

#### Call Params

| Name  | Type      | Description                                                     |
| ----- | --------- | --------------------------------------------------------------- |
| admin | `address` | address for which POOL\_ADMIN role permissions must be revoked. |

### addEmergencyAdmin

`function addEmergencyAdmin(address admin) external`

Add address to the list of members in `EMERGENCY_ADMIN` role. Holders of this role can pause and unpause the pool or an individual reserve.

#### Call Params

| Name  | Type      | Description                                          |
| ----- | --------- | ---------------------------------------------------- |
| admin | `address` | address which will be granted EMERGENCY\_ADMIN role. |

### removeEmergencyAdmin

`function removeEmergencyAdmin(address admin)`

Remove given address from the list of members in `EMERGENCY_ADMIN` role.

#### Call Params

| Name  | Type      | Description                                                          |
| ----- | --------- | -------------------------------------------------------------------- |
| admin | `address` | address for which EMERGENCY\_ADMIN role permissions must be revoked. |

### addRiskAdmin

`function addRiskAdmin(address admin) external`

Add address to the list of members in `RISK_ADMIN` role. Holders of this role can update grace period of Oracle Sentinels, reserve params, unbacked mint cap, liquidation fee and eMode categories.

#### Call Params

| Name  | Type      | Description                                     |
| ----- | --------- | ----------------------------------------------- |
| admin | `address` | address which will be granted RISK\_ADMIN role. |

### removeRiskAdmin

`function removeRiskAdmin(address admin) external`

Remove given address from the list of members in `RISK_ADMIN` role.

#### Call Params

| Name  | Type      | Description                                                     |
| ----- | --------- | --------------------------------------------------------------- |
| admin | `address` | address for which RISK\_ADMIN role permissions must be revoked. |

### addFlashBorrower

`function addFlashBorrower(address borrower) external`

Add address to the list of members in `FLASH_BORROWER` role. Holders of this role do not pay premium for flash loan (Does not apply to `flashLoanSimple`.

#### Call Params

| Name     | Type      | Description                                         |
| -------- | --------- | --------------------------------------------------- |
| borrower | `address` | address which will be granted FLASH\_BORROWER role. |

### removeFlashBorrower

`function removeFlashBorrower(address borrower)`

Remove given address from the list of members in `FLASH_BORROWER` role.

#### Call Params

| Name     | Type      | Description                                                         |
| -------- | --------- | ------------------------------------------------------------------- |
| borrower | `address` | address for which FLASH\_BORROWER role permissions must be revoked. |

### addBridge

`function addBridge(address bridge) external`

Add contract address to the list of _**bridges**_. Holders of this role can leverage the Portal feature to seamlessly move supplied assets across Aave V3 markets on different networks.

#### Call Params

| Name   | Type      | Description                                |
| ------ | --------- | ------------------------------------------ |
| bridge | `address` | address which will be granted BRIDGE role. |

### removeBridge

`function removeBridge(address bridge) external`

Remove contract address from the list of _**bridges**_.

#### Call Params

| Name   | Type      | Description                                                        |
| ------ | --------- | ------------------------------------------------------------------ |
| bridge | `address` | address address for which BRIDGE role permissions must be revoked. |

### addAssetListingAdmin

`function addAssetListingAdmin(address admin) external`

Add address to the list of member in `ASSET_LISTING_ADMIN` role. Holder of this role can update oracles & add new asset to the market.

#### Call Params

| Name   | Type      | Description                                               |
| ------ | --------- | --------------------------------------------------------- |
| bridge | `address` | address which will be granted ASSET\_LISTING\_ADMIN role. |

### removeAssetListingAdmin

`function removeAssetListingAdmin(address admin) external`

Remove address from the list of members in `ASSET_LISTING_ADMIN` role.

#### Call Params

| Name   | Type      | Description                                                               |
| ------ | --------- | ------------------------------------------------------------------------- |
| bridge | `address` | address for which ASSET\_LISTING\_ADMIN role permissions must be revoked. |
