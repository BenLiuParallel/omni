# WPunk Gateway

The WPunk Gateway contract is a helper to easily wrap and unwrap the Punk NFT as necessary when interacting with the protocol.

### supplyPunk

`function supplyPunk(address pool, DataTypes.ERC721SupplyParams[] calldata punkIndexes, address onBehalfOf, uint16 referralCode)`

Supplies the punk indexes into the Parallel pool, minting the same amount of corresponding nWPunks and transferring them to the `onBehalfOf` address.

The punk owner must put their punk up for sale so the WPunk Gateway contract can purchase it.

#### Call Params

| Name         | Type                   | Description                                                                         |
| ------------ | ---------------------- | ----------------------------------------------------------------------------------- |
| pool         | `address`              | address of the targeted pool                                                        |
| punkIndexes  | `ERC721SupplyParams[]` | indexes of the punks you want to deposit into the pool.                             |
| onBehalfOf   | `address`              | address of the user who will receive the xTokens representing the supply            |
| referralCode | `uint16`               | <p>unique code for 3rd party referral program integration.<br>0 for no referral</p> |

### withdrawPunk

`function withdrawPunk(address pool, uint256[] calldata punkIndexes, address to)`

Withdraws punk indexes of the nWPunks, unwraps them and transfers original punks to the `onBehalfOf` address.

#### Call Params

| Name        | Type        | Description                                             |
| ----------- | ----------- | ------------------------------------------------------- |
| pool        | `address`   | address of the targeted pool                            |
| punkIndexes | `uint256[]` | indexes of nWPunks to withdraw and receive native WPunk |
| to          | `address`   | address of the user who will receive native Punks       |
