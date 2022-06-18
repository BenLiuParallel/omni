# WETH Gateway

The WETH Gateway contract is a helper to easily wrap and unwrap ETH as necessary when interacting with the protocol.

### depositETH

`function depositETH(address pool, address onBehalfOf, uint16 referralCode) external payable`

Supplies the `msg.value` amount of ETH into the Parallel pool, minting the same amount of corresponding pWETH and transferring them to the `onBehalfOf` address.

#### Call Params

| Name         | Type      | Description                                                                                       |
| ------------ | --------- | ------------------------------------------------------------------------------------------------- |
| pool         | `address` | address of the targeted pool                                                                      |
| onBehalfOf   | `address` | address who will receive the pWETH. Use msg.sender when the pTokens should be sent to the caller. |
| referralCode | `uint16`  | <p>unique code for 3rd party referral program integration.<br>0 for no referral</p>               |

### withdrawETH

`function withdrawETH(address pool, uint256 amount, address onBehalfOf) external`

Withdraws `amount` of the WETH (or wrapped native chain token), unwraps it and transfers ETH to the `onBehalfOf` address.

#### Call Params

| Name       | Type      | Description                                                                                        |
| ---------- | --------- | -------------------------------------------------------------------------------------------------- |
| pool       | `address` | address of the targeted pool                                                                       |
| amount     | `uint256` | amount to be withdrawn, expressed in wei units. Use type(uint).max to withdraw the entire balance. |
| onBehalfOf | `address` | address that will receive the unwrapped ETH                                                        |

### repayETH

`function repayETH(address pool, uint256 amount, uint256 rateMode, address onBehalfOf) external payable`

Repays `onBehalfOf`'s debt `amount` of ETH () which has a `rateMode`.

#### Call Params

| Name       | Type      | Description                                                                                                                                                                                                                                                                                                  |
| ---------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| pool       | `address` | address of the targeted pool                                                                                                                                                                                                                                                                                 |
| amount     | `uint256` | <p>amount to be borrowed, expressed in wei units.<br>Use uint(-1) to repay the entire debt,  ONLY when the repayment is not executed on behalf of a 3rd party.<br>In case of repayments on behalf of another user, it's recommended to send an _amount slightly higher than the current borrowed amount.</p> |
| rateMode   | `uint256` | <p>the type of borrow debt.<br></p><p>Stable: 1, Variable: 2</p>                                                                                                                                                                                                                                             |
| onBehalfOf | `address` | <p>address of user who will incur the debt.<br>Use msg.sender when not calling on behalf of a different user.</p>                                                                                                                                                                                            |

### borrowETH

`function borrowETH(address pool, uint256 amount, uint256 interesRateMode, uint16 referralCode) external`

Borrows `amount` of WETH with `interestRateMode`, sending the `amount` of unwrapped WETH to `msg.sender`.

#### Call Params

| Name             | Type      | Description                                                                               |
| ---------------- | --------- | ----------------------------------------------------------------------------------------- |
| pool             | `address` | address of the targeted pool                                                              |
| amount           | `uint256` | amount to be borrowed, expressed in wei units                                             |
| interestRateMode | `uint256` | <p>the type of borrow debt. </p><p></p><p>Stable: 1, Variable: 2</p>                      |
| referralCode     | `uint16`  | <p>unique code for 3rd party referral program integration.<br>0 for no referral code.</p> |

### withdrawETHWithPermit

`function withdrawETHWithPermit(address pool, uint256 amount, address to, uint256 deadline, uint8 permitV, bytes32 permitR, bytes32 permitS)`

Withdraws `amount` of the WETH (or wrapped native chain token) without a separate approval tx. The ETH (or native chain token) is sent to the `to` address.

#### Call Params

| Name     | Type      | Description                                                                                                                   |
| -------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| pool     | `address` | address of the targeted pool                                                                                                  |
| amount   | `uint256` | amount of pWETH (or pToken corresponding to native token of chain) that will be burnt to withdraw ETH (or native chain token) |
| to       | `address` | address that will receive the ETH (or native chain token)                                                                     |
| deadline | `uint256` | unix timestamp till which the signature is valid                                                                              |
| permitV  | `uint8`   | Signature parameter v                                                                                                         |
| permitR  | `bytes32` | Signature parameter r                                                                                                         |
| permitS  | `bytes32` | Signature parameter s                                                                                                         |