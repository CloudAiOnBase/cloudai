

# Dynamic Staking APR Model

## Overview
This staking model dynamically adjusts the Annual Percentage Rate (APR) based on the percentage of the circulating supply that is staked. The goal is to ensure a fair and sustainable reward system for stakers while maintaining the long-term viability of the staking pool.

## APR Calculation

When the staking pool has sufficient funds, the APR dynamically adjusts based on the total staked percentage of the circulating supply:

Formula: **APR (in %) = 10 - max(0, min(1, (Staked Percentage - 10) / 40)) × 6**

| Staked Percentage (% of Circulating Supply Staked) | Corresponding APR |
|-----------------------------------|--------------|
| ≤ 10% | 10% (maximum) |
| 10% < A < 50% | Scales between 10% and 4% dynamically |
| ≥ 50% | 4% (minimum) |

As staking participation increases, the APR gradually decreases from **10% to 4%**, ensuring sustainability. Intermediate values such as **5.5%** are possible based on the proportion of tokens staked.

### Example APR Values

Below is a table showing example APR values for different staked percentages:

| Staked Percentage (% of Circulating Supply) | Calculated APR |
|-----------------------------------|--------------|
| 5% | 10% |
| 10% | 10% |
| 20% | 8.5% |
| 30% | 7% |
| 40% | 5.5% |
| 50% | 4% |
| 60% | 4% (minimum) |

## Example Scenarios


### Scenario 1: Normal Staking Conditions
- **Total Staked**: 1,000 CLOUD
- **Circulating Supply**: 10,000 CLOUD
- **Staked Percentage**: 10%
- **APR Calculation**:
  - Using the formula: APR = 10% - max(0, min(1, (10 - 10) / 40)) × 6%
  - APR = 10% - max(0, min(1, 0)) × 6% = 10%
- **Reward for 100 CLOUD Stake**: 100 × 10% = 10 CLOUD per year

### Scenario 2: Higher Staked Percentage
- **Total Staked**: 4,000 CLOUD
- **Circulating Supply**: 10,000 CLOUD
- **Staked Percentage**: 40%
- **APR Calculation**:
  - Using the formula: APR = 10% - max(0, min(1, (40 - 10) / 40)) × 6%
  - APR = 10% - max(0, min(1, 30 / 40)) × 6%
  - APR = 10% - (0.75 × 6%) = 10% - 4.5% = 5.5%
- **Reward for 100 CLOUD Stake**:  100 × 5.5% = 5.5 CLOUD per year

## Fallback Mechanism (Only If Necessary)
If the pool funds ever become insufficient—meaning that not enough fees have been generated to fully cover staking rewards—the fallback mechanism is triggered. This occurs when the current pool funds are not enough to sustain rewards at the normal APR for a full year. Instead of stopping rewards entirely, the system dynamically adjusts the APR to reflect the available balance, ensuring that rewards are still distributed at a sustainable rate.

Formula: **Fallback APR (in %) = (Available Pool Funds / Total Staked Tokens) × 100**

This mechanism activates only when necessary, preventing the depletion of reserves while keeping the staking system functional.

### Scenario: Insufficient Pool Funds
- **Total Staked**: 3,000 CLOUD
- **Circulating Supply**: 10,000 CLOUD
- **Staked Percentage**: 30%
- **Normal APR Calculation**:
  - APR = 10% - max(0, min(1, (30 - 10) / 40)) × 6%
  - APR = 10% - (0.5 × 6%) = 10% - 3% = 7%
  - **Required Funds for 1 Year**: (3,000 × 7%) = **210 CLOUD**
- **Available Pool Funds**: 150 CLOUD (insufficient for full 7% APR)
- **Fallback Mechanism Activates**:
  - **Fallback APR = (150 / 3,000) × 100 = 5%**
  - New rewards distribution is adjusted to fit within available funds.
- **Result**: Stakers still receive rewards, but at a reduced 5% APR to prevent depletion of the pool.

## Key Benefits
- **Fair and adaptive APR** that scales based on staking participation.
- **Long-term sustainability** by reducing APR as more tokens are staked.
- **Failsafe fallback mechanism** to protect the staking pool in extreme cases.

