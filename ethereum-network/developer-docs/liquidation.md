---
description: >-
  When the Health Factor of a position is below one. the position becomes
  subject to liquidation.
---

# Liquidation

Asset liquidation is divided into two different categories:&#x20;

* ERC20&#x20;
* ERC721

Liquidating each one these asset categories has its own prerequisites and requires calling a different smart contract function.

### ERC20 Liquidation

ERC20 Liquidation can be done through calling `liquidationCall()` from the `Pool` contract.

```solidity
function liquidationCall(
    address collateralAsset,
    address debtAsset, 
    address user, 
    uint256 debtToCover, 
    bool receivePToken 
) external;
```

#### Prerequisites

When making a `liquidationCall()`, you must:

* Know the account (i.e. the ethreum address: `user`) whose health factor is below 1.
* Supply and asset that the user is currently using in a borrow position (`debtAsset`)
* Know the valid debt amount and asset address (i.e. `debtToCover` & `debtAsset`)
  * &#x20;You can set the `debtToCover` to `uint(-1)` and the protocol will proceed with the highest possible liquidation allowed.
  * You must already have sufficient balance of the debt asset, which will be used by the `liquidationCall` to pay back the debt.
* Know the ERC20 collateral asset `collateralAsset` you closing, i.e. the asset that the user has `backing` their outstanding loan that you will receive as a `bonus`.
* Whether you want to receive p_Tokens_ or the underlying asset after a successful `liquidationCall()`&#x20;

#### **ERC20 Liquidation Flow Chart**

![](<../../.gitbook/assets/NFTFi General Architecture  - Liquidation.png>)

### ERC721 Liquidation



ERC721 Liquidation can be done through calling `liquidationERC721()` from the `Pool` contract.

```solidity
function liquidationERC721(
        address collateralAsset,
        address liquidationAsset,
        address user,
        uint256 collateralTokenId,
        uint256 liquidationAmount,
        bool receiveNToken
    ) external;
```

#### Prerequisites

When making a `liquidationERC721()`, you must:

* Know the account (i.e. the ethreum address: `user`) whose ERC721 health factor is below 1.
  * `ERC721 Health Factor` is the new health factor that is resulted after liquidating all ERC20 collateral. This is to protect ERC721 from getting liquidated when there are ERC20 assets that can be liquidated to save the health of the user's position.
* Supply any ERC20 asset that the protocol supports for liquidating ERC721.
  * If the supplied asset is being borrowed by the user, then a weighted liquidation bonus will be calculated as following: \
    `liquidation_bonus = (total_debt / global_total_debt) * collateral_liquidation_bonus`.\
    &#x20;Meaning that if the supplied asset is not being borrowed by the user, the bonus will be `0`&#x20;
* Know the collateral asset `collateralAsset` you closing.
* Know the discounted collateral ERC721 price in supplied asset, asset address (i.e. `liquidationAmount` & `liquidationAsset`) and `protocol_fees`
  * &#x20;Protocol fees are calculated as a percentage of the liquidation bonus:\
    _`protocol_fees = liquidation_bonus * protocol_fee_percentage`_
  * The discounted ERC721 price is calculated as the following:\
    `collateral_price`_`= collateral_floor_price / liquidation_bonus + protocol_fees`_
  * You can set the `liquidationAmount` to `uint(-1)` and the protocol will proceed with the highest possible liquidation allowed.
  * You must already have sufficient balance of the liquidation asset, which will be used by the `liquidationERC721` to support debt.
* Whether you want to receive n_Tokens_ or the underlying asset after a successful `liquidationERC721().`\
  ``

#### ERC721 Liquidation Flow Chart

![](<../../.gitbook/assets/NFTFi General Architecture  - Page 5 (2).png>)
