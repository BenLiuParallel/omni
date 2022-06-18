# Major Issues to Solve

However, there are two issues related to accepting Uniswap V3 LP tokens as collateral on our platform and their respective solution:

#### **Issue #1:** Each LP token represents a unique position expressed as a function of liquidity provision range and liquidity, and it is impossible to include every Uniswap V3 LP token into the price oracle directly. How would we manage loan origination and liquidation triggering, while both of which require accurate price quote of the LP token?

**Solution: Updating Uniswap V3 LP token value by updating the numbers of each asset in the LP position and the sum of their values as underlying risky asset price updates.** As documented in the [Uniswap V3 LP Token Analyzer](https://www.notion.so/Uniswap-V3-LP-Token-Analyzer-0caa7b151d26446eab70a1f38ed17d6b) page, the numbers of the two assets in the LP position can be called on-chain. Then the value of the LP position can be derived by:

$$
\begin{equation} V(LP)=x*P_{ETH}+y*P_{USDT} \end{equation}
$$

where $$x$$ is the number of risky asset tokens (ETH) in the LP position, $$y$$ is the number of stablecoins in the position (USDT), and $$P_{ETH}$$ and $$P_{USDT}$$ is the price of ETH and USDT respectively.

Alternatively, to reduce on-chain transactions and gas fee, the position parameters (liquidity, lower and upper bounds of liquidity provision) of staked LP tokens can be called once when it is staked and stored off-chain. On-chain price update of the underlying asset will trigger an off-chain update on x and y and subsequently the value of the LP position, such that only when the updated LP position value deviates from its previous update would that trigger an on-chain update of the LP position value.

#### **Issue #2:** Each LP token represents a unique risk profile. Therefore, it is inefficient to set a universal collateral factor and liquidation threshold for all LP tokens.

Solution: We unify the risk margin implied from the liquidation threshold of widely adopted ERC20 tokens and that implied from the LP tokens. Specifically, for loans collateralised by Uniswap V3 LP tokens, rather than calculating the “health factor” solely based on the total value of COLLATERAL and loan assets and determining liquidation based on such metric, the health factor is edited to consider the **risk profile of the collateralised LP token relative to the loan amount that is made,** **such that each loan collateralised by Uniswap V3 LP token has a unique liquidation threshold that is subject to change as loan amount changes. In this way, the loans collateralised by V3 LP tokens are exposed to very similar liquidation risk as those collateralised by commonly seen ERC20 assets (e.g. ETH, BTC, USDT etc.). We will discuss more details in the next sections.**
