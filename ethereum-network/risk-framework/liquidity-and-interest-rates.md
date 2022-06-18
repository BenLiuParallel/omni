# Liquidity and Interest Rates

## Introduction

The liquidity of the the Omni protocol represents the availability of capital to support borrowing amounts and redeeming nTokens and pTokens. The liquidity of the protocol can be measured via the utilization rate, which is the share of reserve that is currently borrowed for each asset.

## Interest Rate Model

Interest rates are charged to borrowers i.e. the borrow interest rate based on the Utilization Rate, _**U**_. At a high level, the interest model helps incentivize what is needed to support liquidity. When there is capital available, borrowers pay less interest to borrow and when capital is scarce, high interest rates encourage more supply and repayments on loans.

As U gets closer to 100% the liquidity risk increases. There is an inflection point before which the interest rate changes, i.e. slope, are small and after which slope starts rising sharply. This inflection point is represented as U\<sub>optimal\</sub>

The interest rate$$R_t$$follows the model:

$$if \hspace{1mm} U < U_{optimal}:  \hspace{1cm}  R_t = R_0 + \frac{U_t}{U_{optimal}} R_{slope1}$$  &#x20;

$$if \hspace{1mm} U \geq  U_{optimal}:  \hspace{1cm} R_t = R_0 + R_{slope1} + \frac{U_t-U_{optimal}}{1-U_{optimal}}R_{slope2}$$



In the borrow rate technical implementation, the [calculateCompoundedInterest](https://github.com/aave/protocol-v2/blob/baeb455fad42d3160d571bd8d3a795948b72dd85/contracts/protocol/libraries/math/MathUtils.sol#L45) method relies on an approximation that mostly affects high interest rates. The resulting actual borrow rate can is:

&#x20;$$Actual APY = (1+Theoretical APY/secsperyear)^{secsperyear}-1$$

## Model Parameters

| Asset | UOptimal | Slope 1 | Slope 2 |
| ----- | -------- | ------- | ------- |
| ETH   | 65%      | 8%      | 100%    |
| USDC  | 90%      | 4%      | 60%     |
| USDT  | 80%      | 4%      | 75%     |
| DAI   | 80%      | 4%      | 75%     |
| stETH | 65%      | 8%      | 100%    |
| WBTC  | 65%      | 7%      | 100%    |
| APE   | 45%      | 7%      | 300%    |

