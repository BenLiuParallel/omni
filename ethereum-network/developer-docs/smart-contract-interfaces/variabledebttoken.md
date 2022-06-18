# VariableDebtToken

## Read Functions

### UNDERLYING\_ASSET\_ADDRESS

`function UNDERLYING_ASSET_ADDRESS() external view returns (address)`

Returns the address of the underlying asset of this debtToken (E.g. WETH for variableDebtWETH)

#### Return Value

| Type    | Description                         |
| ------- | ----------------------------------- |
| address | The address of the underlying asset |

## Write Functions

### mint

`function mint(address user, address onBehalfOf, uint256 amount, uint256 index) external returns (bool, uint256)`

Mints debt token to the `onBehalfOf` address.

#### Call Params

| Name       | Type      | Description                                                                                                                      |
| ---------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| user       | `address` | The address receiving the borrowed underlying, being the delegatee in case of credit delegate, or same as `onBehalfOf` otherwise |
| onBehalfOf | `address` | The address receiving the debt tokens                                                                                            |
| amount     | `uint256` | The amount of debt being minted                                                                                                  |
| index      | `uint256` | The variable debt index of the reserve                                                                                           |

#### Return Values

| Type    | Description                                                        |
| ------- | ------------------------------------------------------------------ |
| bool    | `true` if the previous balance of the user is 0, `false` otherwise |
| uint256 | The scaled total debt of the reserve                               |

### burn

`function burn(address from, uint256 amount, uint256 index) external returns (uint256)`

Burns user variable debt.

#### Call Params

| Name   | Type      | Description                                    |
| ------ | --------- | ---------------------------------------------- |
| from   | `address` | The address from which the debt will be burned |
| amount | `uint256` | The amount getting burned                      |
| index  | `uint256` | The variable debt index of the reserve         |

#### Return Value

| Type    | Description                          |
| ------- | ------------------------------------ |
| uint256 | The scaled total debt of the reserve |
