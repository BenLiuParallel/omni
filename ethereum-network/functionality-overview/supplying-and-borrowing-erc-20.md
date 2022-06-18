# Supplying and Borrowing ERC-20

## What assets can I supply and borrow?

At launch, you will be able to both supply and borrow ETH, stablecoins (USDC, USDT, DAI), APE, stETH, and wBTC.

Over time we will add more assets to the lending pool that you will be able to supply and borrow.

## How do I earn interest?

When you supply your ERC-20 assets, you will earn interest as a share of the interest paid by borrowers. Borrowers of the ERC-20 assets pay interest based on the balance between the amount of the asset that is supplied and borrowed in the pool aka the utilization rate. Borrowers will also receive interest rewards in the form of sOMNI token.&#x20;

When assets are supplied to the protocol, you will receive an equivalent amount of pTokens (pETH, pUSDC, pUSDT, pDAI, pAPE, pSTETH, pWBTC) tokens. These tokens account for the interest earned from the pool paid by borrowers. Interest accrues on a per-block basis and can be realized once the assets are withdrawn. When assets are borrowed, you receive an equivalent amount of dTokens (dETH, dUSDC, dUSDT, dDAI, dAPE, dSTETH, dWBTC) which track the amount of interest owed per-block. The interest owed from borrowing is added onto the overall borrow amount and can be repaid at any time.

For more details on the interest rate see the [Liquidity and Interest Rates](../risk-framework/liquidity-and-interest-rates.md) section.

## How much can I borrow?

The maximum amount you can borrow is based on the weighted collateral factor i.e. the amount of assets supplied and collateralized and their corresponding collateral values. For example, if you have supplied and collateralized 1 BAYC (USD price = $300,000), 4 ETH (USD price = $12,000), and 800 USDC (USD price = $800), then your borrow limit would be equal to the collateral factor of each asset \* the total value of the assets. Given collateral factors of 30% for BAYC, 80% for ETH, 80% for USDC, the total amount you borrow in the above example would be (30% \* $300,000) + (80% \* $12,000) + (80% + 800) = **$100,240**.

Note, as the value of your supplied assets changes, the max borrow amount will also change. If you reach or surpass the max borrow amount, you will not be able to borrow more assets.

## How can I repay?

You can repay your borrowed position at any time by clicking the 'Repay' button on the 'My Borrowed Positions' menu. You will be able to repay in the same token that you borrowed in. By repaying, you will increase your borrow limit.

## How can I withdraw my assets?

You can withdraw your assets from the 'My Supplied Positions' menu by clicking the 'withdraw' button. You will be able to withdraw your assets as long as you do not exceed the borrow limit if the transaction takes place. If you are unable to withdraw, then you can repay your debt or supply more assets to withdraw.
