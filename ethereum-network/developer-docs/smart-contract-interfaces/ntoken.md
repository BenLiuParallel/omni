# NToken

nTokens are tokens minted and burnt upon _supply_ and _withdraw_ of ERC721 assets to a Parallel market, which denote the amount of crypto assets supplied and the yield earned on those assets. The nTokens’ value is pegged to the value of the corresponding supplied asset at a 1:1 ratio and can be safely stored, transferred or traded. All yield collected by the nTokens' reserves are distributed to nToken holders directly by continuously increasing their wallet balance.

## Events

### BalanceTransfer

`event BalanceTransfer(address indexed from, address indexed to, uint256 tokenId)`

Emitted during the transfer action.

#### Call Params

| Name    | Type      | Description                                 |
| ------- | --------- | ------------------------------------------- |
| from    | `address` | The user whose tokens are being transferred |
| to      | `address` | The recipient                               |
| tokenId | `uint256` | The id of the token being transferred       |

### ClaimERC20Airdrop

`event ClaimERC20Airdrop(address indexed token, address indexed to, uint256 amount)`

Emitted during `claimERC20Airdrop()`

#### Call Params

| Name   | Type      | Description                                 |
| ------ | --------- | ------------------------------------------- |
| token  | `address` | The user whose tokens are being transferred |
| to     | `address` | The recipient                               |
| amount | `uint256` | The amount being claimed from the airdrop   |

### ClaimERC721Airdrop

`event ClaimERC721Airdrop(address indexed token, address indexed to, uint256[] ids)`

Emitted during `claimERC721Airdrop()`

#### Call Params

| Name  | Type        | Description                                          |
| ----- | ----------- | ---------------------------------------------------- |
| token | `address`   | The user whose tokens are being transferred          |
| to    | `address`   | The recipient                                        |
| ids   | `uint256[]` | The ids of the tokens being claimed from the airdrop |

### ClaimERC1155Airdrop

`event ClaimERC1155Airdrop(address indexed token, address indexed to, uint256[] ids, uint256[] amounts, bytes data)`

Emitted during `claimERC1155Airdrop`

#### Call Params

| Name    | Type        | Description                                                                       |
| ------- | ----------- | --------------------------------------------------------------------------------- |
| token   | `address`   | The user whose tokens are being transferred                                       |
| to      | `address`   | The recipient                                                                     |
| ids     | `uint256[]` | The ids of the tokens being claimed from the airdrop                              |
| amounts | `uint256[]` | The amount of NFTs being claimed from the airdrop for a specific id.              |
| data    | `bytes`     | The data of the tokens that is being claimed from the airdrop. Usually this is 0. |

### ExecuteAirdrop

`event ExecuteAirdrop(address indexed airdropContract)`

Emitted during `executeAirdrop`

#### Call Params

| Name            | Type      | Description                         |
| --------------- | --------- | ----------------------------------- |
| airdropContract | `address` | The address of the airdrop contract |

## Read Functions

### UNDERLYING\_ASSET\_ADDRESS

`function UNDERLYING_ASSET_ADDRESS() external view returns (address)`

Returns the address of the underlying asset of this xToken.

#### Return Value

| Type    | Description                         |
| ------- | ----------------------------------- |
| address | The address of the underlying asset |

### RESERVE\_TREASURY\_ADDRESS

`function RESERVE_TREASURY_ADDRESS() external view returns (address)`

Returns the address of the Parallel treasury, receiving the fees on this xToken.

#### Return Value

| Type    | Description                          |
| ------- | ------------------------------------ |
| address | The address of the Parallel treasury |

### DOMAIN\_SEPARATOR

`function DOMAIN_SEPARATOR() external view returns (bytes32)`

Get the domain separator for the token.

#### Return Value

| Type    | Description                                        |
| ------- | -------------------------------------------------- |
| bytes32 | The domain separator of the token at current chain |

### nonces

`function nonces(address owner) external view returns (uint256)`

Returns the nonce for owner.

#### Call Params

| Name  | Type      | Description              |
| ----- | --------- | ------------------------ |
| owner | `address` | The address of the owner |

#### Return Value

| Type    | Description            |
| ------- | ---------------------- |
| uint256 | The nonce of the owner |

## Write Functions

### mint

`function mint(address caller, address onBehalfOf, DataTypes.ERC721SupplyParams[] calldata tokenData, uint256 index)`

Mints `amount` xTokens to `user`.

#### Call Params

| Name       | Type                   | Description                                                                                                                                                                                                            |
| ---------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| caller     | `address`              | The address performing the mint                                                                                                                                                                                        |
| onBehalfOf | `address`              | The address of the user that will receive the minted xTokens                                                                                                                                                           |
| tokenData  | `ERC721SupplyParams[]` | <p>The list of the tokens getting minted and their collateral configs<br><br><code>struct ERC721SupplyParams {</code><br>  <code>uint256 tokenId;</code><br>  <code>bool useAsCollateral;</code><br><code>}</code></p> |
| index      | `uint256`              | The next liquidity index of the reserve                                                                                                                                                                                |

#### Return Value

| Type | Description                                      |
| ---- | ------------------------------------------------ |
| bool | `true` if the previous balance of the user was 0 |

### burn

`function burn(address from, address receiverOfUnderlying, uint256[] calldata tokenIds, uint256 index)`

Burns xTokens from `user` and sends the equivalent amount of underlying to `receiverOfUnderlying`.

#### Call Params

| Name                 | Type        | Description                                       |
| -------------------- | ----------- | ------------------------------------------------- |
| from                 | `address`   | The address from which the xTokens will be burned |
| receiverOfUnderlying | `address`   | The address that will receive the underlying      |
| tokenIds             | `uint256[]` | The ids of the tokens getting burned              |
| index                | `uint256`   | The next liquidity index of the reserve           |

#### Return Value

| Type | Description                      |
| ---- | -------------------------------- |
| bool | `true` if withdrawing all tokens |

### mintToTreasury

`function mintToTreasury(uint256 tokenId, uint256 index) external`

Mints xTokens to the reserve treasury.

#### Call Params

| Name    | Type      | Description                             |
| ------- | --------- | --------------------------------------- |
| tokenId | `uint256` | The id of the token getting minted      |
| index   | `uint256` | The next liquidity index of the reserve |

### transferOnLiquidation

`function transferOnLiquidation(address from, address to, uint256 tokenId) external`

Transfers xTokens in the event of a borrow being liquidated, in case the liquidators reclaims the xToken.

#### Call Params

| Name    | Type      | Description                                                  |
| ------- | --------- | ------------------------------------------------------------ |
| from    | `address` | The address getting liquidated, current owner of the xTokens |
| to      | `address` | The recipient                                                |
| tokenId | `uint256` | The id of the token getting transferred                      |

### transferUnderlyingTo

`function transferUnderlyingTo(address user, uint256 tokenId) external`

Transfers the underlying asset to `target`.

#### Call Params

| Name    | Type      | Description                             |
| ------- | --------- | --------------------------------------- |
| user    | `address` | The recipient of the underlying         |
| tokenId | `uint256` | The id of the token getting transferred |

### handleRepayment

`function handleRepayment(address user, uint256 tokenId) external`

Handles the underlying received by the xToken after the transfer has been completed.

#### Call Params

| Name    | Type      | Description                             |
| ------- | --------- | --------------------------------------- |
| user    | `address` | The user executing the repayment        |
| tokenId | `uint256` | The id of the token getting transferred |

### permit

`function permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external`

Allow passing a signed message to approve spending`.`

#### Call Params

| Name     | Type      | Description                                                |
| -------- | --------- | ---------------------------------------------------------- |
| owner    | `address` | The owner of the funds                                     |
| spender  | `address` | The spender                                                |
| value    | `uint256` | The amount                                                 |
| deadline | `uint256` | The deadline timestamp, type(uint256).max for max deadline |
| v        | `uint8`   | Signature param                                            |
| s        | `bytes32` | Signature param                                            |
| r        | `bytes32` | Signature param                                            |

### rescueTokens

`function rescueTokens(address token, address to, uint256 amount) external`

Rescue and transfer tokens locked in this contract.

#### Call Params

| Name   | Type      | Description                     |
| ------ | --------- | ------------------------------- |
| token  | `address` | The address of the token        |
| to     | `address` | The address of the recipient    |
| amount | `uint256` | The amount of token to transfer |

### claimERC20Airdrop

`function claimERC20Airdrop(address token, address to, uint256 amount) external`

Claims ERC20 Airdrops. Step 4 of snapshot balance type. Please see [`docs`](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/flash-claim) for more info. `onlyPoolAdmin` can call this function.

#### Call Params

| Name   | Type      | Description                               |
| ------ | --------- | ----------------------------------------- |
| token  | `address` | The address of the token                  |
| to     | `address` | The address of the recipient              |
| amount | `uint256` | The amount being claimed from the airdrop |

### claimERC721Airdrop

`function claimERC721Airdrop(address token, address to, uint256[] calldata ids) external`

Claims ERC721 Airdrops. Step 4 of snapshot balance type. Please see [`docs`](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/flash-claim) for more info. `onlyPoolAdmin` can call this function.

#### Call Params

| Name  | Type        | Description                                          |
| ----- | ----------- | ---------------------------------------------------- |
| token | `address`   | The address of the token                             |
| to    | `address`   | The address of the recipient                         |
| ids   | `uint256[]` | The ids of the tokens being claimed from the airdrop |

### claimERC1155Airdrop

`function claimERC1155Airdrop(address token, address to, uint256[] calldata ids, uint256[] calldata amounts, bytes calldata data) external`

Claims ERC1155 Airdrops. Step 4 of snapshot balance type. Please see [`docs`](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/flash-claim) for more info. `onlyPoolAdmin` can call this function.

#### Call Params

| Name    | Type        | Description                                                                       |
| ------- | ----------- | --------------------------------------------------------------------------------- |
| token   | `address`   | The address of the token                                                          |
| to      | `address`   | The address of the recipient                                                      |
| ids     | `uint256[]` | The ids of the tokens being claimed from the airdrop                              |
| amounts | `uint256[]` | The amount of NFTs being claimed from the airdrop for a specific id.              |
| data    | `bytes`     | The data of the tokens that is being claimed from the airdrop. Usually this is 0. |

### executeAirdrop

`function executeAirdrop(address airdropContract, bytes calldata airdropParams) external`

Executes airdrop. Step 2 of snapshot balance type. Please see [`docs`](https://parallelfi.gitbook.io/parallel-finance/ethereum-network/developer-docs/flash-claim) for more info. `onlyPoolAdmin` can call this function.

#### Call Params

| Name            | Type      | Description                                                                      |
| --------------- | --------- | -------------------------------------------------------------------------------- |
| airdropContract | `address` | The address of the airdrop contract                                              |
| airdropParams   | `bytes`   | Third party airdrop abi data. You need to get this from the third party airdrop. |
