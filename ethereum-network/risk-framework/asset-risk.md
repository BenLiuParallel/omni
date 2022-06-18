# Asset Risk

Each asset in the Omni protocol has specific parameters that influences how they can be supplied and borrowed.

* **Collateral** - Can this asset be used to take borrow positions on?
* **Loan-to-Value (LTV)** - What is the maximum amount that can be borrowed? It is represented as a % with numerator equal to (amount borrowed) / (value of supplied asset)
* **Liquidation Threshold** - This represents the point when the asset would start to go through the liquidation process. It is represented as a % with numerator equal to (value of debt position) / (value of asset position). The difference between the LTV and Liquidation Threshold can be considered as the safety cushion for borrowers.
* **Liquidation Bonus** - The amount of additional collateral that liquidators receive / are discounted for purchasing assets on liquidation. Represented as percentage of the collateral purchased.

For each wallet the maximum LTV is calculate as the weighted average of the LTVs of the collateral assets and their value:

$$
Max LTV = \frac{ \sum{Collateral_i \: in \: USD \: \times \: LTV_i}}{Total \: Collateral \: in \: USD \:}
$$

For each wallet the Liquidation Threshold is calculate as the weighted average of the Liquidation Thresholds of the collateral assets and their value:

$$
Liquidation \: Threshold= \frac{ \sum{Collateral_i \: in \: USD \: \times \: Liquidation \: Threshold_i}}{Total \: Collateral \: in \:USD  \:}
$$

The table below shows a summary of the latest values:

|         Asset         | Symbol | Collateral | Loan to Value | Liquidation Threshold | Liquidation Bonus |
| :-------------------: | :----: | :--------: | :-----------: | :-------------------: | :---------------: |
|  Bored Ape Yacht Club |  BAYC  |     Yes    |      30%      |          70%          |         5%        |
|      CryptoPunks      |  Punk  |     Yes    |      30%      |          70%          |         5%        |
| Mutant Ape Yacht Club |  MAYC  |     Yes    |      30%      |          70%          |         5%        |
|        Doodles        | DOODLE |     Yes    |      30%      |          70%          |         5%        |
|          USDC         |  USDC  |     Yes    |      80%      |          85%          |         5%        |
|         Tether        |  USDT  |     Yes    |      75%      |          80%          |         5%        |
|          DAI          |   DAI  |     Yes    |      75%      |          80%          |         5%        |
|         Ether         |   ETH  |     Yes    |     82.5%     |          85%          |         5%        |
|   Lido Staked Ether   |  stETH |     Yes    |      69%      |          81%          |        7.5%       |
|    Wrapped Bitcoin    |  WBTC  |     Yes    |      70%      |          75%          |        6.5%       |
|        Apecoin        |   APE  |     Yes    |      20%      |          70%          |         5%        |

