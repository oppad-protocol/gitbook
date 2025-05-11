# How to Launch a Farm in 3 Steps

_Deploy a fully operational reward farm in minutes._

Whether you’re bootstrapping liquidity for your token or rewarding LPs with $OPPAD, setting up a farm is fast and intuitive through the OPPAD Dashboard.

***

####

#### 🧩 Step 1: Enter Farm Parameters

Fill in the following:

* **Staking Token Address**: LP pair contract (e.g., OPPAD/ETH)
* **Reward Token Address**: Token you want to distribute
* **Emission Rate**: Tokens per block or per second
* **Start/End Blocks**: Define when farming begins and ends
* **Harvest Interval**: Time users must wait between claims

📥 Deposit the total reward token supply directly into the contract.

***

#### 🔗 Step 2: Deploy the Farm

Click `Deploy Contract` from the farming dashboard.

* The smart contract will initialize via `initializeFarm()`
* Contract is now live on-chain and visible in “Available Pools”
* Metrics like TVL, APR, and # of stakers start updating in real time

🔒 All core settings (rate, duration, reward token) are immutable post-deployment.

***

#### 🌾 Step 3: Share & Monitor

* Share your pool URL with the community
* Users can connect wallets, approve LPs, and start farming
* Monitor live analytics (TVL, rewards distributed) via dashboard
* Use Webhook alerts or backend feeds to stay notified

> \[!TIP]\
> Want to run multiple farms? Simply repeat the steps. OPPAD supports **multi-pool deployment** per project.
