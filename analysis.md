# **Wallet Risk Analysis**



### **Methodology Overview**



**1.Data Collection Method**

We collected transaction data for a given list of Ethereum wallet addresses using the Etherscan API. For each wallet, the full transaction history was retrieved, including fields such as sender and receiver addresses, gas used, transaction value, and timestamps. To ensure scalability and avoid hitting API rate limits, a delay of 0.3 seconds per request was maintained . The data was compiled and stored in a CSV for reproducibility.

Additionally, a curated list of known Compound Protocol smart contract addresses was used to filter only those transactions that represent direct interactions with the Compound DeFi system.



**2. Feature Selection Rationale**

The selected features aim to capture transactional behavior, resource usage, and interaction diversity, all of which can serve as proxies for wallet risk or suspicious activity:



a) num\_compound\_txs: Counts how many times the wallet interacted with the Compound protocol. Higher interaction frequency may signal deeper DeFi engagement or automation.



b) avg\_gas\_used: Average gas per Compound transaction. Bots or arbitrage tools may have consistent or high gas usage patterns.



c) total\_gas\_cost\_eth: Total ETH spent on gas. High expenditure can indicate aggressive strategies or high-frequency operations.



d) unique\_contracts\_interacted: Measures the breadth of smart contract engagement. A higher number may suggest experimental, spammy, or arbitrage behaviors.



e) tx\_time\_entropy: Captures the entropy (randomness) of transaction timestamps. Low entropy implies regularity or bot-like execution, while high entropy suggests randomness or human behavior.



These features were chosen based on domain knowledge in DeFi behavioral analytics and are generalizable to other protocols.



**3. Scoring Method**

A composite risk score was assigned to each wallet using a weighted linear combination of the engineered features:

risk\_score = 

&nbsp;   num\_compound\_txs \* 1.5 + 

&nbsp;   tx\_time\_entropy \* 2 +

&nbsp;   total\_gas\_cost\_eth \* 1.2 +

&nbsp;   unique\_contracts\_interacted \* 1.0



This formula balances frequency, variability, and resource intensity to approximate wallet riskiness. The weights were assigned based on intuitive importance, with entropy and Compound engagement given more influence due to their stronger link to bot-like or high-risk behavior.



**4. Justification of the Risk Indicators**



Each risk indicator was selected with the goal of identifying potential non-organic or high-risk behavior:

a) Compound Transaction Count: High frequency may indicate automated farming or flash loan behavior.

b) Entropy of Timestamps: Regular spacing suggests scripting; randomness suggests human input.

c) Gas Metrics: Large or unusually consistent gas usage can signify programmatic execution.

d) Contract Diversity: Interacting with a wide range of contracts increases exposure to vulnerabilities or speculative behaviors.



These indicators are modular and scalable—they can be extended to other DeFi protocols, used for clustering, anomaly detection, or fed into a supervised learning model once labeled data is available.



