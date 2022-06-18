---
description: >-
  The OMNI token is an ERC-20 compatible token with the addition of EIP 2612
  permit function, allowing gas-less transactions and one transaction
  approval/transfer.
---

# OMNI Token

Besides the standard ERC20 token features (`transfer()`, `balanceOf()`, `allowance()`, etc), the following features are also available.

### permit

**`function permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s ) external`**

Allows a user to permit another account (or contract) to use their funds using a signed message. This enables gas-less transactions and single approval/transfer transactions.

#### Call Params

| Name     | Type    | Description                                                                      |
| -------- | ------- | -------------------------------------------------------------------------------- |
| owner    | address | The owner of the funds                                                           |
| spender  | address | The spender for the funds                                                        |
| value    | uint256 | The amount the `spender` is permitted to use                                     |
| deadline | uint256 | The deadline timestamp that the permit is valid. Use `uint(-1)` for no deadline. |
| v        | uint8   | Signature parameter                                                              |
| r        | bytes32 | Signature parameter                                                              |
| s        | bytes32 | Signature parameter                                                              |

### \_nonces

**`function _nonces(address owner) public`**

Returns the next valid nonce to submit when calling `permit()`

