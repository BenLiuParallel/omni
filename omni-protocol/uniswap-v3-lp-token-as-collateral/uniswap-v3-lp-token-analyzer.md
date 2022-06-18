# Uniswap V3 LP Token Analyzer

Uniswap V3 LP token is an NFT token that represents the liquidity provision position. Check [Uniswap V3 Whitepaper](https://uniswap.org/whitepaper-v3.pdf) for detail.

Specifically, the variable $$L$$ represents the liquidity given the relative price ($$P_0$$) of asset $$X$$ in the denomination of asset $$Y$$ at the time the position is created/last changed, the lower bound ($$P_a$$) and upper bound ($$P_b$$) of price in which the user chooses to provide liquidity.

1. **Define input parameters.** On the page of adding liquidity in Uniswap V3, three factors have to be defined, $$P_a$$, $$P_b$$ , and either one of $$x_0$$ and $$y_0$$, where $$x_0$$ and $$y_0$$ denote the number of $$X$$ and $$Y$$ tokens that will be injected into the liquidity provision position.
2.  **Calculate** $$L$$ **and** $$x_0$$ **or** $$y_0$$**.** Depending on which one of $$x_0$$ and $$y_0$$ is defined in step 1), the other one will be calculated. Detailed calculation follows formula 2.2 on [Uniswap V3 Whitepaper](https://uniswap.org/whitepaper-v3.pdf). For example, if $$x_0$$ is defined, we will first solve $$L$$ based on (1) and then calculate $$y_0$$ based on (2) below:

    $$
    \tag{1} x_0=\max\left(0,L*\left(\frac{1}{\sqrt{P_0}}-\frac{1}{\sqrt{P_b}}\right)\right)
    $$

    $$
    \tag{2} y_0=\max\left(0,L*\left({\sqrt{P_0}}-{\sqrt{P_a}}\right)\right)
    $$

    Note here $$\frac{y_0}{x_0}\ne P_0$$ in Uniswap V3.
3.  Then given price fluctuating to any $$P$$, $$x$$ and $$y$$ that represent the number of $$X$$ and $$Y$$ tokens redeemable from the liquidity provision position can be derived following formula 6.29 and 6.30 in Uniswap V3 Whitepaper, which are copied and pasted below:

    $$
    \tag{3} y=\begin{cases} 0 & P<P_a \\ L*\left(\sqrt{P}-\sqrt{P_a}\right) &P_a \le P < P_b \\ L*\left(\sqrt{P_b}-\sqrt{P_a}\right) & P\ge P_b \end{cases}
    $$

    $$
    \tag{4} x=\begin{cases} L*\left(\frac{1}{\sqrt{P_a}}-\frac{1}{\sqrt{P_b}}\right) & P<P_a \\ L*\left(\frac{1}{\sqrt{P}}-\frac{1}{\sqrt{P_b}}\right) &P_a \le P < P_b \\ 0 & P\ge P_b \end{cases}
    $$

**To get** $$x$$ **and** $$y$$ **in a given position as well as other information, function **<mark style="color:orange;">**`positions()`**</mark>** can be called. See details** [**here**](https://docs.uniswap.org/protocol/reference/periphery/interfaces/INonfungiblePositionManager)**.**
