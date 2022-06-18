# PToken

pTokens are tokens minted and burnt upon _supply_ and _withdraw_ of ERC20 assets to a Parallel market, which denote the amount of crypto assets supplied and the yield earned on those assets. The pTokens’ value is pegged to the value of the corresponding supplied asset at a 1:1 ratio and can be safely stored, transferred or traded. All yield collected by the pTokens' reserves are distributed to pToken holders directly by continuously increasing their wallet balance.

## Events

### BalanceTransfer

`event BalanceTransfer(address indexed from, address indexed to, uint256 value, uint256 index)`

Emitted during the transfer action.

#### Call Params

| Name  | Type      | Description                                 |
| ----- | --------- | ------------------------------------------- |
| from  | `address` | The user whose tokens are being transferred |
| to    | `address` | The recipient                               |
| value | `uint256` | The amount being transferred                |
| index | `uint256` | The next liquidity index of the reserve     |

## Read Functions

### UNDERLYING\_ASSET\_ADDRESS

`function UNDERLYING_ASSET_ADDRESS() external view returns (address)`

Returns the address of the underlying asset of this xToken (E.g. WETH for pWETH).

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

`function mint(address caller, address onBehalfOf, uint256 amount, uint256 index)`

Mints `amount` xTokens to `user`.

#### Call Params

| Name       | Type      | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| caller     | `address` | The address performing the mint                              |
| onBehalfOf | `address` | The address of the user that will receive the minted xTokens |
| amount     | `uint256` | The amount of tokens getting minted                          |
| index      | `uint256` | The next liquidity index of the reserve                      |

#### Return Value

| Type | Description                                      |
| ---- | ------------------------------------------------ |
| bool | `true` if the previous balance of the user was 0 |

### burn

`function burn(address from, address receiverOfUnderlying, uint256 amount, uint256 index)`

Burns xTokens from `user` and sends the equivalent amount of underlying to `receiverOfUnderlying`.

#### Call Params

| Name                 | Type      | Description                                       |
| -------------------- | --------- | ------------------------------------------------- |
| from                 | `address` | The address from which the xTokens will be burned |
| receiverOfUnderlying | `address` | The address that will receive the underlying      |
| amount               | `uint256` | The amount being burned                           |
| index                | `uint256` | The next liquidity index of the reserve           |

### mintToTreasury

`function mintToTreasury(uint256 amount, uint256 index) external`

Mints xTokens to the reserve treasury.

#### Call Params

| Name   | Type      | Description                             |
| ------ | --------- | --------------------------------------- |
| amount | `uint256` | The amount of tokens getting minted     |
| index  | `uint256` | The next liquidity index of the reserve |

### transferOnLiquidation

`function transferOnLiquidation(address from, address to, uint256 value) external`

Transfers xTokens in the event of a borrow being liquidated, in case the liquidators reclaims the xToken.

#### Call Params

| Name  | Type      | Description                                                  |
| ----- | --------- | ------------------------------------------------------------ |
| from  | `address` | The address getting liquidated, current owner of the xTokens |
| to    | `address` | The recipient                                                |
| value | `uint256` | The amount of tokens getting transferred                     |

### transferUnderlyingTo

`function transferUnderlyingTo(address user, uint256 amount) external`

Transfers the underlying asset to `target`.

#### Call Params

| Name   | Type      | Description                     |
| ------ | --------- | ------------------------------- |
| user   | `address` | The recipient of the underlying |
| amount | `uint256` | The amount getting transferred  |

### handleRepayment

`function handleRepayment(address user, uint256 amount) external`

Handles the underlying received by the xToken after the transfer has been completed.

#### Call Params

| Name   | Type      | Description                      |
| ------ | --------- | -------------------------------- |
| user   | `address` | The user executing the repayment |
| amount | `uint256` | The amount getting repaid        |

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
