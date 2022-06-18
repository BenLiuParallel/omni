# Supplying NFTs

## How do I supply my NFTs?

Connect your wallet on which you have your NFTs. Browse to the 'Supply NFTs' section and click on the "Supply" button for the collection which you want to supply. Select the NFT(s) from the collection that you want to supply and click the Supply NFT button to submit the transaction\*. Once the transaction is confirmed, your asset(s) will be supplied and collateralized. You will then be able to borrow ERC-20 tokens.

You will see your supplied NFT positions above the 'Supply NFTs' menu. In this menu, you can choose to turn off collateralization and initiate the redeem flow.

\*The first time you supply an asset from a collection will require an additional approval transaction

## What kind of NFTs can I supply?

In the initial launch, Omni will support supplying and collateralized loans of NFTs from 4 collections: Bored Ape Yacht Club, Mutant Ape Yacht Club, CryptoPunks, and Doodles. Over time we plan to support more collections and types of NFTs. In the future, decisions on what collections to support will be decided via Governance.

## Why supply my NFTs?

By supplying your NFTs in Omni, you can get access to funds via borrowing of ERC-20 tokens without selling. You can use this capital to buy more NFTs or spend in any way you please. You are able to keep borrowing against the NFT so long as you are within the borrow limit. The borrow limit (or LTV) is equal to the weighted average of the max borrow %'s of all the assets you have supplied and collateralized in the Omni protocol.

### How is the NFT borrow limit calculated?

The borrow limit of an NFT can be represented by the following formula: Borrow Limit = Price of NFT \* Collateral Factor (LTV) of NFT. NFTs are priced based on the [Omni NFT Price Oracle](../developer-docs/nft-price-oracle/). Currently, the price oracle uses NFT floor price data from OpenSea and LarvaLabs (for CryptoPunks). As such the price used to calculate the borrow limit is the same across all assets in the collection. The collateral factor or LTV is set on a per collection basis. You can see the collateral factors in the [Asset Risk](../risk-framework/asset-risk.md) section.

## What happens when I supply? How are they secured?

When you complete the transaction to supply your NFT it is transferred to an escrow contract. In return, you receive a nNFT token (nBAYC, nMAYC, nPUNK, nDOODLE). The nNFT token is a mirror version of the token you supplied, it contains the same metadata. Holders of nNFT token can redeem the original NFT provided debt is repaid sufficiently.

The escrow contract to which your NFT is transferred ensures the NFT can only be transferred in certain conditions. Specifically, NFTs can only be transferred to the owner of the corresponding nNFT token upon a successful redeem transaction and transferred to the liquidation contract in the case of a liquidation. This contract itself provides security from theft.

The protocol also will launch and maintain an insurance reserve which will be used to pay out users  in the NFT price oracle value of the NFT in the event of a protocol shortfall.

## How can I redeem my NFT?

You can redeem your NFT from the protocol from the 'My Supply Positions' menu. You will be able to redeem your NFT as long as you do not exceed the borrow limit if the transaction takes place. If you are unable to redeem due to having a debt position greater than the borrow limit, then you can repay your debt or supply more assets to redeem.

If you are able to redeem then you can select the NFT(s) from the collection you want to redeem and click the 'Redeem' button. Once the transaction is successful, your NFT will be transferred back to your wallet and the nNFT token will be burned.

## How can I use my supplied NFT to claim an airdrop?

You can use the Flash Claim feature to claim airdrops in a single transaction without repaying any debt. The flash claim feature utilizes Flash Loan functionality and integrates directly with the supported collections airdrop contracts to enable you to transfer your supplied NFT from Omni to your wallet, claim the airdrop, and supply the NFT back to Omni within the same transaction.

For more details see [Flash Claim](../developer-docs/flash-claim.md).
