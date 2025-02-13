## CloudAI Staking Specifications

---

### **1. Dynamic Staking APR Model**
| % of Circulating Supply Staked | Staking APR |
|--------------------------------|-------------|
| ≤ 10%                         | 10% APR (max cap) |
| 20%                            | 8% APR |
| 30%                            | 6% APR |
| ≥ 40%                          | 4% APR (minimum cap) |

- **APR is dynamically adjusted** based on the percentage of circulating supply staked.  
- **Circulating supply is fetched from an external contract.**  

---

### **2. Staking Contract Dependency**  
- **Relies on an external contract** to fetch the real-time **circulating supply** via `getCirculatingSupply()`.  

---

### **3. Unstaking Conditions**  
- **Unstaking Period:** 7 days.  
- **Users must manually claim** their tokens after the cooldown.  

---

### **4. Ownership & Governance**  
- **Initial Owner:** Deployer of the contract.  
- **DAO Transition:** Ownership will be **transferred to the CloudAI DAO** once it is established.  
- **Governance Control:** DAO will have full control over staking parameters and features.  

---

### **5. Contract Controls & Features**  

#### ✅ **Pause Rewards Distribution**  
- DAO can **pause** reward distribution while still allowing staking and unstaking.  
- Staked funds remain unaffected, but no rewards are accrued during the pause.  

#### ✅ **Modifiable Parameters (DAO-Controlled)**  
- **APR Rates.**  
- **Adjust phase transitions (e.g., 5-year, 10-year shifts).**  
- **Redemption mechanism (e.g., 7-day cooldown).**  

#### ✅ **Emergency Withdraw**  
- **Function:** Unstakes **all tokens** from the staking contract and returns them to users' wallets.  
- **Trigger:** Can only be activated by the DAO.  
- **Effect:**  
  - All staked tokens are **automatically withdrawn** for every staker.  
  - Staking contract becomes **inactive** after execution.  

#### ✅ **Empty Rewards Pool to Community Funds**  
- DAO can **return unallocated rewards** back to the community fund.  
- Ensures efficient fund management and sustainability.  
- **Requires DAO approval** and **a specified recipient wallet.**  

#### ✅ **Non-Upgradable**  
- The contract is **immutable** after deployment for security and stability.  

---

### **6. Staking Rewards & Sustainability Plan**  

| **Phase**  | **Rewards Source**                     | **Annual APR** | **Sustainability Plan** |
|------------|---------------------------------|----------------|----------------------|
| **Years 1-5**  | Community Allocation (**400M CLOUD**) | Dynamic (Based on staked %)| Rewards come from pre-allocated community tokens. |
| **Years 5-10** | **50% Fees** + **50% Community Fund** | Dynamic | Transition phase: staking rewards are partially funded by protocol fees. |
| **Years 10+**  | **100% Fee-Based Staking** | Dynamic | Fully sustainable: staking rewards come entirely from protocol-generated fees (no new token emissions). |

---

### **Final Summary**  
This **staking contract** follows a **dynamic APR model**, adjusting rewards based on the circulating supply staked. Governance and key parameters are **controlled by the DAO** once established. Users can stake with a **7-day unstaking cooldown**, while DAO-controlled mechanisms allow for **pausing rewards, modifying APR settings, emergency withdrawals, and returning unused rewards to the community fund**. The contract is **non-upgradable** and transitions to a **fully fee-based reward system** over time for sustainability.  

