# NFT Price Oracle

Parallel Omni requires NFT prices from an off chain Oracle. Currently we are using a customized Oracle implementation that consists of an off-chain client and an on-chain contract.

### On**-**Chain (Contract)

The Omni money market can make use of prices by interacting with the following contracts

| Name            | Network | Address                                    |
| --------------- | ------- | ------------------------------------------ |
| PriceOracle.sol | Rinkby  | 0x536a49361dea6dd01353732a88fc4040720a4694 |
| PriceOracle.sol | Kovan   | 0x54e1e8f85145e952167ba4acd11dbe97128bb540 |

**Simple Contract Interface**&#x20;

```solidity
interface NFTOracle {
    function getPrice(address token) external view returns(uint256 price);
    function getTwap(address token) external view returns(uint256 twap);
    function getEma(address token) external view returns(uint256 ema);
    function getBlockLast(address token) external view returns(uint256 price);
}
```

### Off-Chain (Client)

The off chain client collects NFT prices from various marketplaces to get a "Floor Price" this price is the lowest ask price that a NFT holder is willing to sell their asset.&#x20;

The off-chain client collects these prices and uses them in the "pricing algorithm".&#x20;

After the most recent values have been calculated we "conditionally write" the updates on chain.&#x20;

_A simplified visualization of the data can be seen below_

![](<../../../.gitbook/assets/image (115).png>)

### Pricing Algorithm&#x20;

&#x20;Parallel Omni uses two primary pricing metrics to help stabilize the prices we report.&#x20;

1. Time Weighted Average Price (TWAP)
2. Exponential Moving Average (EMA)

**Time Weighted Average Price**

$$
TWAP = \frac{a_{t2} - a_{t1}}{t_{2}-t_{1}}
$$

Where `a_t` is the cumulative price at time `t`, and `t_2` is the time at time `2`. Currently we are using a time frame of 1440 minutes (24 hours) to calculate TWAP. The rational for this value can be seen on the research page

Exponential Moving Average

$$
EMA = v_{t1} * \frac{s}{1+d} + ema_{t0} * (1 - \frac{s}{1+d})
$$

Where `s` is the smoothing value and `d` is the number of periods. Currently we are using a period of 4000 minutes and a smoothing factor of 2 (standard practice) to calculate EMA. The rational for this period can be seen on this [research page](research.md).

### **Conditional Write**

In order to be responsive and optimize gas, we want to minimize the number of on chain updates possible. Therefore we only update the on chain prices conditionally, when at least one of the following statements are true:&#x20;

1. The last update was greater than or equal to 60 minutes ago
2. The current values deviate greater than 3% from the values stored on chain&#x20;

### **Access Control**

Currently our Oracle is controlled uses Role based access control to control the accounts that can make updates to the prices on chain.  This role is only granted to a small set of highly secured accounts.



Resources

* [https://docs.openzeppelin.com/contracts/4.x/api/access](https://docs.openzeppelin.com/contracts/4.x/api/access)
* [https://uniswap.org/whitepaper.pdf](https://uniswap.org/whitepaper.pdf)
* [https://docs.uniswap.org/protocol/V2/concepts/core-concepts/oracles](https://docs.uniswap.org/protocol/V2/concepts/core-concepts/oracles)
* [https://www.investopedia.com/terms/e/ema.asp](https://www.investopedia.com/terms/e/ema.asp)
