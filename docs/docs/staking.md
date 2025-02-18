
## **CloudAI Staking Specifications**

### **1. Staking**

- **Minimum Stake Amount:**  
  - `minStakeAmount` – **100 CLOUD** (initial value, DAO adjustable).  
  - Users must stake **at least** this amount to participate in staking.  

- **Staking Function Behavior:**  
  - Users cannot stake **less than `minStakeAmount`**.
  - If a user attempts to stake below this threshold, the transaction **reverts**.
  
- **Rationale:**  
  - Prevents spam transactions with **tiny stake amounts**.
  - Ensures **staking rewards are distributed efficiently**.
  - Avoids **blockchain storage overhead** caused by many inactive, low-value stakes.

- **Canceling Unstaking:**  
  - If a user **stakes** or **cancels their unstaking**, the unstaking process is **automatically revoked**.
  - The tokens in **unstaking cooldown are returned to active stake**.

----------

### **2. Staking Rewards**

- **Rewards are instantly claimable** (users can claim at any time).
- No **auto-compounding** (users must manually stake rewards).

----------

### **3. Unstaking**

- **Unstaking Cooldown:** **10 days** before funds can be withdrawn.
- **Users must manually claim** their tokens after the cooldown ends.

----------

### **4. Inactivity Handling**

- **After 1 year of inactivity** (no staking, unstaking, reward claims, or vote):
  - The staker is **ignored in governance quorum** (still staked and earning rewards).

- **After 3 years of inactivity**:
  - The staker is **automatically unstaked**.
  - Staked tokens + **unclaimed rewards** are sent back to the user’s wallet.

- **Effect:**
  - Optimize rewards distribution and governance :
  - Ensures governance remains **active and fair**.
  - Prevents **forever-locked inactive funds** while maintaining user flexibility.
  

----------

### **5. Emergency Withdraw**

- **Function:** Unstakes **all tokens** from the staking contract and returns them to users' wallets.
- **Effect:**
  - **All staked tokens + unpaid rewards (optional)** are refunded.
  - Staking contract becomes **inactive** after execution.

----------

### **6. Empty Rewards Pool Back to Community Funds**

- Return unallocated rewards back to the community fund.
- Requires DAO approval and a specified recipient wallet.

----------

### **7. Parameters**

| **Parameter** | **Initial value** |
|--------------|----------|
| **Minimum Stake Amount** | 100 CLOUD |
| **APR range** | 4% → 10% |
| **Staked Circ. Supply range** | 10% → 50% |
| **Cooldown** | 10 days |
| **Governance Inactivity Threshold** | 1 years |
| **Auto-unstake** | 3 years |

Governance Inactivity Threshold
- Params are fetched from **CloudUtils contract** where they can be adjusted.

- **CloudUtils params control transition:**
  - **Phase 1:** Controlled by the dev.
  - **Phase 2:** Dev team takes over (multisig-controlled, minimum 5 members, majority required).
  - **Phase 3:** Control is transferred to the **CloudAI DAO**. CloudUtils can still be used by the dev team in case of emergencies.
  
- **Caching Period:** **24 hours** (reduces gas fees and contract dependency issues)
- **Manual caching**: Function to manually recache.
- **Time-Lock:** **48h delay on governance changes** for security (will be implemented in **CloudUtils** later)

----------

### **8. Views and Events**
  
- **Smart contract view functions** will allow DAO governance to fetch staking data:
  - `getStakerInfo(address staker) → (uint256 stakedAmount, uint256 unstakingAmount, uint256 unclaimedRewards, uint256 unstakingStartTime, uint256 claimableTimestamp, uint256 totalEarnedRewards)` – Fetches individual staker's data.
  - `getTotalStakers() → uint256` – Returns the total number of stakers.
  - `getTotalStakedTokens() → uint256` – Returns the total amount of tokens staked in the contract.
  - `getTotalStakedTokensForTally() → uint256` – Returns the total amount of staked tokens excluding inactive stakers for governance tallying.
  - `getAllStakers(uint256 start, uint256 count) → (address[] memory stakers, uint256[] memory stakedAmounts)` – Enables paginated retrieval for large-scale governance queries.
  - `getStakersData(address[] memory stakers) → (uint256[] memory stakedAmounts)` – Fetches staking data for a specific group of stakers for governance tally purposes.
  - `getStakingParams() → (uint256 minStakeAmount, uint256 cooldown, uint256 autoUnstakePeriod, uint256 governanceInactivityThreshold, uint256 aprMin, uint256 aprMax, uint256 stakedCircSupplyMin, uint256 stakedCircSupplyMax)` – Returns all staking-related parameters.

- **Event Logging for Off-Chain Processing:**
  - `event StakerData(address indexed staker, uint256 stakedAmount);`
  - Emits an event whenever a staker **stakes/unstakes**, enabling **efficient off-chain tracking**.

----------

### **9. Sustainability Plan (goal)**

| **Phase**  | **Rewards Source**                      | **Sustainability Plan** |
|------------|---------------------------------|----------------|
| **Years 1-5**  | Community Allocation (**400M CLOUD**) | Rewards come from pre-allocated community tokens. |
| **Years 5-10** | **50% Fees** + **50% Community Fund**  | Transition phase: staking rewards are partially funded by protocol fees. |
| **Years 10+**  | **100% Fee-Based Staking**  | Fully sustainable: staking rewards come entirely from protocol-generated fees (no new token emissions). |

----------

### **10. Non-Upgradable**

- The contract is immutable after deployment for security.
- Staked tokens cannot be accessed by the dev team or anyone.
- Ensures stakers that there is no possibility of loss or theft.

----------
