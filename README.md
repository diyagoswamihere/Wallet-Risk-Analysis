# Wallet-Risk-Analysis

This project analyzes Ethereum wallet transactions using Etherscan’s API to detect interactions with the Compound DeFi protocol

Objective: <br>
To identify Ethereum wallets interacting with the Compound protocol, extract insightful features from their transaction history, and assign risk scores based on transaction behavior for further analytics or downstream ML modeling.

Datasets <br>
Wallet IDs: Provided in Wallet id - Sheet1.csv <br>
Transaction Data: Collected via Etherscan API <br>
Compound Contracts: A manually curated and extensible list of known Compound-related smart contract addresses

Steps:<br>

1. Data Collection<br>

     Fetched full transaction histories of 103 Ethereum wallets using the Etherscan API
     Limited to 3 API calls/sec using time.sleep() for compliance
     Extracted and stored all transactions in all_wallets_transactions.csv

3. Compound Interaction Filtering<br>

     Filtered transactions by checking to address against known Compound smart contract addresses
     Generated a subset: compound_wallets_transactions.csv
     Result: 520 Compound-related transactions detected

4. Feature Engineering<br>

     Created features for each wallet:
        num_compound_txs: Number of Compound transactions
        avg_gas_used: Average gas used
        total_gas_cost_eth: Total gas cost in ETH
        unique_contracts_interacted: Number of unique contracts interacted with 
        tx_time_entropy: Entropy of transaction timestamps
        risk_score: Composite score based on weighted features

6. Visualization<br>

     Visualized the top 10 riskiest wallets using matplotlib and seaborn

Files Included <br>
1. Wallet id - Sheet1.csv – Source wallet IDs<br>
2. all_wallets_transactions.csv – Full transaction history for all wallets<br>
3. compound_wallets_transactions.csv – Filtered Compound-related txs<br>
4. wallet_risk_features.csv – Final feature set with risk scores<br>
5. compound_filter_and_features.py – Feature engineering pipeline<br>
6. wallet_risk_scores.csv- The final file with the wallets and their risk scores
Refer to the analysis.md for any detailed explanation. 

👤 Author
Diya Goswami
