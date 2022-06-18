# ERC-20 Price Discovery

For ETH and ERC-20 assets, we use Chainlink's decentralized oracles for the price feeds, with prices updated every time the deviation crosses a certain threshold. See table below for details:

| Asset | Price updated every | Address                                    |
| ----- | :-----------------: | ------------------------------------------ |
| ETH   |          1%         | 0x5f4ec3df9cbd43714fe2740f5e3616155c5b8419 |
| USDC  |          1%         | 0x8fffffd4afb6115b954bd326cbe7b4ba576818f6 |
| USDT  |          1%         | 0x3e7d1eab13ad0104d2750b8863b489d65364e32d |
| DAI   |          1%         | 0xaed0c38402a5d19df6e4c03f4e2dced6e29c1ee9 |
| APE   |          2%         | 0x2bA49Aaa16E6afD2a993473cfB70Fa8559B523cF |
| stETH |          1%         | 0xcfe54b5cd566ab89272946f602d76ea879cab4a8 |
