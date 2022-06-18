# Liquidation

## What is a liquidation?

Liquidation is a process in which collateralized assets are sold in order to pay down an outstanding debt position. Liquidations take place when the total amount of borrowed assets (debt position) reach a high enough percentage of the total amount of collateralized assets (asset position). This percentage is known as the liquidation threshold. Each asset has its own liquidation threshold (see [Asset Risk](../risk-framework/asset-risk.md)) and the overall liquidation threshold is based on the weighted average of collateralized assets.

## In what order are assets put into liquidation?

When the overall liquidation threshold is reached, assets will be sold via liquidation. There is a precedence for first selling ERC-20 and ETH before NFTs so long as selling ERC-20 and ETH can result in reaching a healthy debt / asset position.&#x20;

When the debt / asset position is not significantly higher than the liquidation threshold, liquidators can claim ETH and ERC-20 before NFTs. NFTs are liquidated on an asset basis i.e. no fractionalized liquidations. Liquidators receive bonuses for each collateralized asset they claim as defined in the [Asset Risk](../risk-framework/asset-risk.md) section.

## Can you give me an example?

Alice has 1 Doodle ($48,000), 5,400 USDC ($5,400), and 2.2 ETH ($6,600) supplied for total supplied USD value of $60,000. The overall liquidation threshold occurs when debt position is $50,000. Alice's debt position reaches $50,000 and is all in ETH. Liquidating ETH and/or USDC will get her below the liquidation threshold so those collaterals are sent for liquidation.  A liquidators comes and pays the value of USDC i.e. $5,400 in ETH to claim 5,400 USDC + 270 USDC (5% liquidation bonus).



Alice has 1 Doodle ($48,000) as her total supplied position. Liquidation threshold occurs when debt is $30,000. Alice borrows over $30,000 in USDC. The Doodle is liquidated at the current floor price of $48,000 minus the liquidation bonus of $2,400 = $45,600. $30,000 worth of USDC is used to repay the debt position and the remaining $15,600 USDC is repaid to Alice.

## Why are liquidations needed?

Liquidations are needed in order to protect the protocol. Those who supply assets and collateralize them are adding assets to a lending pool from which borrowing happens. If the value of the total borrow comes to close or exceeds the value of the lending pool then the lenders are at risk of not being able to redeem / withdraw their assets. The liquidation process serves as way to pay down debt when an individual user is unable to do so.

## How can I avoid getting liquidated?

You can avoid getting liquidated by staying within your borrow limit. If you are close to reaching your borrow limit, then you can repay your borrowed amount and/or supply more collateral. By default, repaying has more of an impact. Be mindful about price fluctuations of your supplied assets including stablecoins. When the price of your supplied assets decreases you get closer to the liquidation threshold.

## Can I participate in the liquidations ecosystem?

Liquidations are open to everyone. Currently, you must interact directly with the liquidator through the liquidation smart contract. You can find more details in the [developers liquidation section](liquidation.md).
