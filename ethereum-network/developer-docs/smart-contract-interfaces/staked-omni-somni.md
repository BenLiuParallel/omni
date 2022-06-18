---
description: >-
  Users get rewards for supplying assets to the pool inform of sOMNI. Users also
  get sOMNI when they purchase OMNI through PCV. sOMNI is 1-to-1 pegged token
  for OMNI and can be converted to OMNI.
---

# Staked OMNI (sOMNI)

### stake

**`function stake(address onBehalfOf, uint256 amount)`**

Stakes a certain amount of OMNI tokens, with the option of sending the sOMNI tokens to another address (i.e. the `onBehalfOf` address).

Note: the `msg.sender` must already have a balance of OMNI token.

{% hint style="danger" %}
The user must `approve()` the `amount` for the sOMNI contract to stake, before execution.
{% endhint %}

| Name       | Type    | Description                                                                                                                |
| ---------- | ------- | -------------------------------------------------------------------------------------------------------------------------- |
| onBehalfOf | address | The address which will receive the sOMNI tokens. Use `msg.sender` if the sOMNI should be sent to the same calling address. |
| amount     | uint256 | The amount of OMNI to be staked                                                                                            |

### claimRewards

**`function claimRewards(address to, uint256 amount)`**

Claims an `amount` of **`OMNI`** rewards that the `msg.sender` has accrued, with the option of sending the rewards to a different account.\


| Name   | Type    | Description                                                                                                                                                    |
| ------ | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| to     | address | <p>The address which will receive the OMNI tokens rewards. Use <code>msg.sender</code> if the OMNI rewards should be sent to the same calling address.<br></p> |
| amount | uint256 | <p>The amount of OMNI to be claimed. Use <code>uint(-1)</code> to claim all outstanding rewards for the user.<br></p>                                          |

### redeem

**`function redeem(address to, uint256 amount)`**

Redeems the staked tokens - receiving **`OMNI`** tokens and burning sOMNI tokens.

{% hint style="warning" %}
A user can only redeem the underlying **`OMNI`** tokens if the following has been satisfied:

1. Activated their `cooldown()` period, and
2. The sum of `stakersCooldowns()` + `COOLDOWN_SECONDS()` for their address must be greater than the current unix block timestamp, and
3. They must call `redeem()` before the sum of `stakersCooldowns()` + `COOLDOWN_SECONDS()` +`UNSTAKE_WINDOW()` has passed.
{% endhint %}



| Name   | Type    | Description                                                                                                                                                 |
| ------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| to     | address | <p>The address which will receive the redeemed OMNI tokens. Use <code>msg.sender</code> if the OMNI should be sent to the same calling address.<br><br></p> |
| amount | uint256 | The amount of OMNI to be redeemed. Use `uint(-1)` to redeem the entire balance of the user.                                                                 |

### cooldown

**`function cooldown()`**

Activates the cool down timer to be able to unstake.

### stakersCooldowns

**`function stakersCooldowns(address staker) view returns uint`**

Returns the unix timestamp in seconds for when the `staker` activated the cool down by calling `cooldown()`.

A staker is able to successfully unstake when this value + `COOLDOWN_SECONDS` in unix time has passed.

### COOLDOWN\_SECONDS

**`function COOLDOWN_SECONDS() view returns uint`**

Returns the current minimum cool down time needed to elapse before a staker is able to unstake their tokens.

As of October 2020, the current `COOLDOWN_SECONDS` value is 864000 seconds (i.e. 10 days). This value should always be checked directly from the contracts.

### UNSTAKE\_WINDOW

**`function UNSTAKE_WINDOW() view returns uint`**

Returns the maximum window of time in seconds that a staker can `redeem()` their stake once a `cooldown()` period has been completed.

As of October 2020, the current `UNSTAKE_WINDOW` value is 172800 seconds (i.e. 2 days). This value should always be checked directly from the contracts.

### getNextCooldownTimestamp

**`function getNextCooldownTimestamp(uint256 fromCooldownTimestamp, uint256 amountToReceive, address toAddress, uint256 toBalance) public returns (uint256)`**&#x20;

Calculates the cool down timestamp based on the sender / receiver timestamps.

#### Cool down examples:

* A user stakes OMNI for the first time. Their cool down time is set to the current block timestamp.
* A user already has sOMNI and decides to stake more OMNI (i.e. call `stake()`), while they already have a cool down period active:
  * If the cool down is expired (e.g. beyond the `UNSTAKE_WINDOW`), then the cool down period will remain expired.
  * If the cool down period is still valid, using the amount staked and and the current block timestamp, a weighted average is calculated with the current cool down timestamp of the user.
* A user calls `redeem()`. This will reset the cool down timestamp.
* A user calls `claimRewards()`. The cool down timestamp is not affected.
* A user transfers (i.e. sends) sOMNI to another address:
  * The cool down timestamp of the `msg.sender` remains the same.
  * For the receiver of the sOMNI:
    * If they have a valid cool down period finishing before the cool down period of the `msg.sender`, a weighted average is calculated with the current cool down timestamp of the user.
    * If the receiver has an expired cool down timestamp, the cool down timestamp is reset.
    * If both the receiver and `msg.sender` have valid cool down periods, and the `msg.sender` cool down period ends before the receiver, then the receiver's cool down period remains the same.

| Name                       | Type    | Description                                      |
| -------------------------- | ------- | ------------------------------------------------ |
| fromCooldownTimestamp      | uint256 | <p>The cool down timestamp of the sender<br></p> |
| <p>amountToReceive<br></p> | uint256 | The amount of sOMNI tokens to be sent            |
| toAddress                  | address | The receiver's address                           |
| toBalance                  | uint256 | The current sOMNI balance of the receiver        |

### getTotalRewardsBalance

**`function getTotalRewardsBalance(address staker) external view returns (uint256)`**

Returns the total rewards that are pending to be claimed by a staker.



| Name       | Type    | Description          |
| ---------- | ------- | -------------------- |
| **staker** | address | The staker's address |
