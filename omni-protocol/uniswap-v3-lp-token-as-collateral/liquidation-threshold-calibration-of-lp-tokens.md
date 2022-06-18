# Liquidation Threshold Calibration of LP Tokens

Again, let’s discuss this section in the arch of the following scenario: ETH is at $1000. The user provides liquidity of 1 ETH and 1596.12 USDT within the $500-1500 price range. Furthermore, the liquidation threshold of ETH is 80%.

*   **First, we calculate the liquidation risk margin implied by the ETH liquidation threshold.** The liquidation risk margin denotes the margin that covers the potential loss in the case that actual liquidation proceeds are not enough to cover the loan. Therefore, the liquidation risk margin is calculated as:

    $$
    \begin{equation} LRM=\frac{100\%-liq\_thld}{liq\_thld} \end{equation}
    $$

    where $$liq\_thld$$ denotes its liquidation threshold. Therefore, we calculate the liquidation risk margin of ETH as:

    $$
    \begin{aligned} LRM_{ETH}&=\frac{100\%-80\%}{80\%} \\ &=25\% \end{aligned}
    $$

    This means, when liquidation is triggered for a loan collateralised by ETH, as long as the liquidation proceeds does not fall 25% below the ETH price when liquidation is triggered, the liquidation proceeds will be enough to cover the loan and the platform stays solvent.

    **Note here the numeraire is changed to the price of ETH when liquidation is triggered**, which is consistent with the measure under which the health factor is calculated at the time liquidation is triggered.
*   **Second, we calibrate the water level ETH price (**$$P_w$$**)**. The water level ETH price is defined as the ETH price such that the LP position value equals to that of the loan.

    $$
    \begin{equation} V_{LP}(P_w)-V_{loan}=0 \end{equation}
    $$

    $$
    \begin{equation} V_{LP}=X(P_w)*P_w+Y(P_w) \end{equation}
    $$

    where $$X(P_w)$$ and $$Y(P_w)$$ denote the numbers of $$X$$ and $$Y$$ tokens redeemable from the LP position when underlying X asset price is $$P_w$$. And as defined in [Uniswap V3 LP Token Analyzer](uniswap-v3-lp-token-analyzer.md), $$X(P_w)$$ and $$Y(P_w)$$ can be rearranged as below:

    $$
    \begin{equation} \begin{cases} Y(P_w)=\max\left(0,L*\left(\sqrt{\min(P_w,P_b)}-\sqrt{P_a}\right)\right) \\ X(P_w)=\max\left(0,L*\left(\frac{1}{\sqrt{\max(P_w,P_a)}}-\frac{1}{\sqrt{P_b}}\right)\right) \end{cases} \end{equation}
    $$

    where $$L$$ denotes the liquidity of the LP position, and $$P_a$$ and $$P_b$$ denote the lower and upper bound of the liquidity provision price range respectively.
*   **Third, we imply the liquidation price of ETH (**$$P_{liq}$$**) such that when the LP position is liquidated when ETH touches such price,  the liquidation of the LP position will be triggered, and the implied liquidation risk margin of the LP position is the same as that of ETH**:

    $$
    \begin{equation} \begin{aligned} {P_{liq}}&={P_w}*\left(1+LRM_{ETH}\right)\\ \end{aligned} \end{equation}
    $$

    **Note there is a sanity check that loans should only be allowed if** $$P_{liq} \le P_b$$**.** As the LP position has constant value when ETH price is above $$P_b$$, liquidating the LP position at $$P_{ETH}=P_{liq}>P_b$$ is equivalent to doing so at $$P_{ETH}=P_b$$. Therefore, the actual liquidation risk margin is lower than that of ETH and thus insufficient.
*   **Finally, we calculated the liquidation price of the LP position when ETH hits such liquidation price, and calculate the liquidation threshold (in percentage) of the LP position as:**

    $$
    \begin{equation} liq\_thld_{LP}=\frac{V(P_w)}{V(P_{liq})} \end{equation}
    $$

    Note the liquidation threshold is a useful metric to analyse the risk of the loan. However, **health factor calculation, which dictates the triggering of liquidation, should be based on the ratio between ETH price and liquidation price** $$P_{liq}$$ rather than basing the health factor calculation on the value of the LP itself. As when the ETH price moves, depending on the $$L$$, $$P_a$$ and $$P_b$$ of the LP position and ETH spot price, the LP position’s value could stay constant until ETH price drops below a critical level. Therefore, the conventional calculation of health factor may not appropriately reflect the health of a loan when collateralised by the LP token while its underlying ETH price is changing which lead to deterioration of the loan health. The health factor will be calculated as:

$$
\begin{equation} health\_factor=\frac{P_{ETH}}{P_{liq}} \end{equation}
$$

_``_
