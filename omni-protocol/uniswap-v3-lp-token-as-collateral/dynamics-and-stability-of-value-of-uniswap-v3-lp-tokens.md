# Dynamics and Stability of Value of Uniswap V3 LP Tokens

We will demonstrate the value dynamics of a generic Uniswap V3 LP position and illustrate its relatively higher stability of value than its underlying ERC20 token in the arch of following context: ETH is at $1000. User provides liquidity of 1 ETH plus 1596.12 USDT within 500-1500 price range.

1. If ETH falls down to $500, the LP position becomes 3.26 ETH + 0 USDT. **Note even if ETH continues to fall further from this point, the LP position will still be 3.26 ETH as the lower bound of the liquidity provision boundary is hit and all liquidity is depleted.**
2. If ETH jumps to $1500, the LP position becomes 0 ETH + 2820.86 USDT. Again, even if ETH continues to increase, the LP position will still be redeemable to 2820.86 USDT.

Comparison among providing liquidity to Uniswap V2, V3 and holding ETH is plotted below against ETH price movement spectrum.&#x20;

![](<../../.gitbook/assets/Untitled (1).png>)

It is clear from the plot above, that LP token is a safer and less volatile asset than its underlying risky asset (i.e. blue and orange line are above the grey line when ETH price drops), as the value of the LP token drops slower than its underlying risky asset. Therefore, LP token is a better class of collateral asset than general ERC20 tokens (such as ETH and BTC) in terms of value stability.

Note the above observation is generally true regardless of the liquidity provision range and/or spot price, as the LP position's Delta (i.e. value change rate with respect to unit change in the underlying ETH price) is always less than or equal to 1, thanks to the dilution of the potential stablecoin component of the LP position, which by nature has zero Delta.
