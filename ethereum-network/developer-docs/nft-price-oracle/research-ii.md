---
description: >-
  Backtesting historical NFT prices to find the best TWAP period. Based on the
  responsiveness (measure of freshness) and stabilization (measure of max
  drawdown protection).
---

# Research II

## Overview

The main goal of our Oracle is to provide stable and fresh price data for the Omni money market.&#x20;

In this research article we'll be determining the optimal TWAP period that meets the criteria for Omni.&#x20;

An optimal period should provides both a stable price (reduce jitter and anomalies) and a reactive price (match realtime marketplace data and track changes in price trends).

Since these two metrics are directly competing there is not an explicit "best" value, but there is some preferred trade off of `reactiveness` and `stabilization` that should satisfy our requirements.&#x20;

#### &#x20;Target Question

What TWAP period will best maximize our reactiveness and stability?

### **Breakdown of metrics**

* Reactiveness&#x20;
* Stabilization&#x20;

#### Reactiveness ****&#x20;

Reactiveness is related to how closely we track the price. A 100% reactive price would track realtime floor price 1:1. However 100% reactive is undesirable because we want to avoid extreme changes and price manipulation.

$$
Reactiveness = \sum_{i=1}^{D}(x_i-y_i)^2
$$

#### Stabilization

Stabilization is related to how much short fall protection is provided to a collateral provider. A completely stable price would have 100% short fall protection, meaning that the TWAP period would avoid all historical liquidations for users who borrowed 100% of their borrow limit for a period of time.

$$
Stabilization = \sum_{i = 1}^n [\frac{x_{t}}{max(x_{[t - p]})} < \frac{LTV}{LiqThres}  ]/n
$$

### Exploring the indicators

We can start by exploring the historical data of a couple projects, and plot the TWAP values to help shape an intuitive understanding of the implications of TWAP period width.

**Projects**

* Azuki
* Bored Ape
* Cryptopunks
* Doodle

### Responsiveness&#x20;

We can visualize the **reactiveness** of a TWAP window by plotting the TWAP in comparison to the realtime price. Since a short window will only look at recent prices, the width of the window directly correlates to how much we want to smooth (reduce reactiveness) our prices.&#x20;

In the following examples the lines are

| Color  | TWAP Period |
| ------ | ----------- |
| Orange | 6 hours     |
| Green  | 24 hours    |
| Red    | 72 hours    |

![Azuki (top) and Bored Ape (bottom)](<../../../.gitbook/assets/image (132).png>)

![Cryptopunks (top) and Doodles (bottom)](<../../../.gitbook/assets/image (88).png>)

### Stabilization

We can visualize the impact of larger TWAP window on the max drawdown. Looking at the chart below we can see the blue line that represents the max drawdown for a 30 day window.&#x20;

The blue line describes the **currently twap value** divided by the **max value within the window.** Which simulates the scenario of a user providing and NFT at the top of the recent market and supplying collateral for at least 30 days.

In the following examples the lines are

| Color  | TWAP Period |
| ------ | ----------- |
| Orange | 6 hours     |
| Green  | 24 hours    |
| Red    | 72 hours    |

![Azuki (top) and Bored Ape (bottom)](<../../../.gitbook/assets/image (105).png>)

Above we can see in both the Azuki backtest (top) and the bored apes (bottom) that widening the TWAP period results in a lifted line, and more short fall protection. We can also see that by utilizing wider a TWAP we can be more robust to short term market trends.&#x20;

![Cryptopunks (top) and Doodles (bottom)](<../../../.gitbook/assets/image (167).png>)

### Optimizing

We can search for an optimal set of values by iterating our metrics over a handful of NFT projects and different TWAP period widths.&#x20;

For the case of this research we will not be exhaustive and we will only explore a subset of possible solutions.&#x20;

However our research is ongoing, and not only limited to TWAP, so we can revisit these numbers in later research.&#x20;

**TWAP windows**

* 1 hour
* 3 hours
* 6 hours
* 12 hours
* 18 hours
* 24 hours
* 30 hours
* 36 hours
* 42 hours
* 48 hours

**Key indicators**

* Relative Increase of shortfall protection
* Relative responsiveness&#x20;

#### Responsiveness results

The values shown represent the negative mean squared error between our TWAP values and the realtime price for all historical data points. This results in an error of 0 when there is no TWAP applied since we are 1:1 with the real time price. Results get larger as the error increases, meaning the values are less in sync with the realtime price.

We can see how as we widen the TWAP period we lower our responsiveness.&#x20;

| Minutes | azuki | boredapeyachtclub | cryptopunks | doodles-official | Average |
| ------- | ----- | ----------------- | ----------- | ---------------- | ------- |
| 1       | 0.00  | 0.00              | 0.00        | 0.00             | 0.00    |
| 60      | -0.08 | -0.42             | -0.12       | -0.01            | -0.16   |
| 180     | -0.16 | -0.92             | -0.36       | -0.04            | -0.37   |
| 360     | -0.28 | -1.60             | -0.70       | -0.08            | -0.66   |
| 720     | -0.50 | -2.99             | -1.32       | -0.15            | -1.24   |
| 1080    | -0.76 | -4.36             | -1.92       | -0.22            | -1.82   |
| 1440    | -1.05 | -5.73             | -2.52       | -0.30            | -2.40   |
| 1800    | -1.38 | -7.18             | -3.13       | -0.39            | -3.02   |
| 2160    | -1.70 | -8.66             | -3.76       | -0.47            | -3.65   |
| 2520    | -2.05 | -10.10            | -4.41       | -0.55            | -4.28   |
| 2880    | -2.41 | -11.44            | -5.07       | -0.63            | -4.89   |

#### Stabilization results

The values shown represent the percent of minutes that a user would be liquidated if they took out 100% collateral at the highest price in the last 30 days. A value of 0 represent a collection that would have never resulted in a liquidation.

We can see how as we widen the TWAP period we reduce the maximum drawdown, and in some cases reduce the value to 0 when the original short fall likelihood is already very low.

| minutes | azuki | boredapeyachtclub | cryptopunks | doodles-official | Average |
| ------- | ----- | ----------------- | ----------- | ---------------- | ------- |
| 1       | 0.24  | 0.00              | 0.00        | 0.00             | 0.06    |
| 60      | 0.17  | 0.00              | 0.00        | 0.00             | 0.04    |
| 180     | 0.16  | 0.00              | 0.00        | 0.00             | 0.04    |
| 360     | 0.16  | 0.00              | 0.00        | 0.00             | 0.04    |
| 720     | 0.16  | 0.00              | 0.00        | 0.00             | 0.04    |
| 1080    | 0.15  | 0.00              | 0.00        | 0.00             | 0.04    |
| 1440    | 0.15  | 0.00              | 0.00        | 0.00             | 0.04    |
| 1800    | 0.14  | 0.00              | 0.00        | 0.00             | 0.04    |
| 2160    | 0.13  | 0.00              | 0.00        | 0.00             | 0.03    |
| 2520    | 0.13  | 0.00              | 0.00        | 0.00             | 0.03    |
| 2880    | 0.13  | 0.00              | 0.00        | 0.00             | 0.03    |

#### Summary

Finally we can summarize our findings by simply calculating the mean value across the projects. This should give us an average impact on our metric for each time period we're interested in.

| minutes | responsiveness | stabilization |
| ------- | -------------- | ------------- |
| 1       | 0.000000       | 0.061120      |
| 60      | -0.161703      | 0.041279      |
| 180     | -0.371128      | 0.041174      |
| 360     | -0.663773      | 0.040791      |
| 720     | -1.240942      | 0.039170      |
| 1080    | -1.815482      | 0.038040      |
| ⭐️ 1440 | -2.400869      | 0.036583      |
| 1800    | -3.019885      | 0.035586      |
| 2160    | -3.649925      | 0.032839      |
| 2520    | -4.279159      | 0.031971      |
| 2880    | -4.885476      | 0.031445      |

Using the table above we can quantify the tradeoff when we widen our TWAP period. We can see that without any period we are extremely responsive (a score of 0) and we have an average rate of 6% liquidation likelihood as a maximum drawdown for 30 day holders.&#x20;

By widening our period to a value greater than 720 minutes or 12 hours, we can see that we gain almost 2.5% more shortfall safety in our stabilization metric.&#x20;

At 720 minutes we still have some room for improvement, we can reduce our liquidation likelihood to 3.65% if we extend our period to 1440 minutes or 24 hours. 1440 minute window does reduce our average responsiveness, but this is still within an acceptable range.&#x20;

### Conclusions

We should set our TWAP period to a value close to **24 hours or 1440 minutes**. This period should provide us with enough reaction to closely follow the realtime market and also provide enough added stability so NFT providers can be confident they will not be liquidated in a flash drawdown.

We're dedicated to improving our pricing mechanism over time and provide more research about the best way to price NFTs. This insight will help us continue to improve our Oracle and bring the best service and experience to all Omni users.&#x20;

**Resources**

* [https://www.investopedia.com/ask/answers/021015/what-best-measure-given-stocks-volatility.asp](https://www.investopedia.com/ask/answers/021015/what-best-measure-given-stocks-volatility.asp)
* [https://en.wikipedia.org/wiki/Mean\_squared\_error](https://en.wikipedia.org/wiki/Mean\_squared\_error)
