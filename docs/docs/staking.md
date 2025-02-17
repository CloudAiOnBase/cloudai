
## **CloudAI Staking Specifications**

### **1. Staking Rewards Distribution**

- **Rewards are instantly claimable** (users can claim at any time).
- No **auto-compounding** (users must manually stake rewards).

----------

### **2. Unstaking Conditions**

- **Unstaking Cooldown:** **10 days** before funds can be withdrawn.
- **Users must manually claim** their tokens after the cooldown ends.

----------

### **3. Staking Rewards & Sustainability Plan (goal)**

| **Phase**  | **Rewards Source**                     | **Annual APR** | **Sustainability Plan** |
|------------|---------------------------------|----------------|----------------------|
| **Years 1-5**  | Community Allocation (**400M CLOUD**) | Dynamic (Based on staked %)| Rewards come from pre-allocated community tokens. |
| **Years 5-10** | **50% Fees** + **50% Community Fund** | Dynamic | Transition phase: staking rewards are partially funded by protocol fees. |
| **Years 10+**  | **100% Fee-Based Staking** | Dynamic | Fully sustainable: staking rewards come entirely from protocol-generated fees (no new token emissions). |

----------

### **4. Inactivity Auto-Unstaking**

- **Any staker who does not perform any action (stake, unstake, or claim rewards) for 2 years is automatically unstaked.**
- **Effect:**
  - Staked tokens + **unclaimed rewards** are automatically unstaked and sent back to the user’s wallet.
  - Optimize rewards distribution and governance.

----------

### **5. Pause Rewards Distribution**

- DAO can pause reward distribution while still allowing staking and unstaking.
- Staked funds remain unaffected, but no rewards are accrued during the pause.

----------

### **6. Empty Rewards Pool to Community Funds**

- Return unallocated rewards back to the community fund.
- Ensures efficient fund management and sustainability.
- Requires DAO approval and a specified recipient wallet.

----------

### **7. Emergency Withdraw**

- **Function:** Unstakes **all tokens** from the staking contract and returns them to users' wallets.
- **Effect:**
  - **All staked tokens + unpaid rewards** are refunded.
  - Staking contract becomes **inactive** after execution.

----------

### **8. Modifiable Parameters**

- Will be fetched from CloudUtils (controlled by dev team). When DAO is ready, CloudUtils will fetch from the DAO contract. CloudUtils will remain with a security control mechanism to be useful in case of emergencies.

| **Parameter** | **Initial value** |
|--------------|----------|
| **APR** | 4% → 10% |
| **Staked CC** | 10% → 50% |
| **Cooldown** | 10 days |
| **Auto-unstake** | 2 years |

----------

### **9. Staking Contract Params**

- Relies on **CloudUtils contract** for **circulating supply** and the **other params**.
- **Caching Period:** **24 hours** (reduces gas fees and contract dependency issues)
- Function to manually recache.
- **CloudUtils params Transition:**
  - **Phase 1:** Controlled by the dev.
  - **Phase 2:** Dev team takes over (multisig-controlled, minimum 5 members).
  - **Phase 3:** Ownership is transferred to the **CloudAI DAO**.
- **Time-Lock:** **48h delay on governance changes** for security.
- **Final DAO Control:** Once the DAO is established, CloudUtils will fetch all parameters directly from a **DAO-owned contract** to ensure full decentralization.

----------

### **10. Views and Events**

- **Event Logging for Off-Chain Processing:**
  - `event StakerData(address indexed staker, uint256 stakedAmount, uint256 votingPower);`
  - Emits an event whenever a staker **stakes/unstakes**, enabling **efficient off-chain tracking**.
- **Smart contract view functions** will allow DAO governance to fetch staking data:
  - `getStakerInfo(address staker) → (uint256 stakedAmount, uint256 votingPower)` – Fetches individual staker's data.
  - `getTotalStakers() → uint256` – Returns the total number of stakers.
  - `getAllStakers(uint256 start, uint256 count) → (address[] memory stakers, uint256[] memory stakedAmounts, uint256[] memory votingPowers)` – Enables paginated retrieval for large-scale governance queries.
  - `getVotingPowerAtBlock(address staker, uint256 blockNumber) → uint256` – Retrieves a staker’s voting power at a specific block for governance integrity.
- **Off-chain indexing (The Graph) and event logs** can be used to enhance governance tracking:
  - `event StakerData(address indexed staker, uint256 stakedAmount, uint256 votingPower);` – Enables DAO to track historical & real-time staker data efficiently.
- **Security:** All governance queries will be public to ensure full transparency.
- **Future Expansion:** `getStakersData()` for batch retrieval will be implemented in **CloudUtils** later.

----------

### **11. Non-Upgradable**

- The contract is immutable after deployment for security.
- Staked tokens cannot be accessed by the dev team or anyone.
- Ensures stakers that there is no possibility of loss or theft.

----------

