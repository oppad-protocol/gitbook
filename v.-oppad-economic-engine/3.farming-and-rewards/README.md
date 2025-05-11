# 3.Farming & Rewards

_Earn protocol rewards. Bootstrap liquidity. Power the ecosystem._

The **OPPAD Farming Module** enables DeFi projects to launch sustainable yield farms where users stake LP tokens in return for token incentives. With fully on-chain emission logic, off-chain scheduling, and live analytics, this module delivers gas-efficient, secure farming without compromising flexibility.

***

#### 🧱 1. Introduction

Yield farming is essential to early liquidity generation. OPPAD makes it simple. Projects can deploy farms via a no-code dashboard or API, reward LP providers, and monitor real-time data—all in one system.

***

#### ⚙️ 2. Key Features

* **Custom Farm Deployment**: Launch new farms for any LP pair and reward token
* **Automated Reward Scheduler**: Cron-based reward emission
* **Flexible Emission**: Configure per-block or per-second reward rates
* **Multi-Farm Support**: Run multiple farms concurrently
* **Live Metrics Dashboard**: Track TVL, APR, and earnings
* **Emergency Controls**: Pause, migrate, or stop farms via multisig

***

#### 🧠 3. Architecture Overview

```mermaid
mermaidCopyEditflowchart TB
  subgraph User Layer
    U[Liquidity Provider]
    P[Project Admin]
  end
  subgraph Interface
    UI[Dashboard] --- API[REST API]
  end
  subgraph Service Layer
    FS[Farming Service]
    RS[Reward Scheduler]
    MQ[Message Queue]
    DB[(PostgreSQL)]
  end
  subgraph Blockchain
    FC[Farm Contract]
    RT[Reward Token]
    LP[LP Token]
  end

  P -->|Deploy Farm| UI --> API --> FS
  FS -->|initFarm()| FC
  U -->|Stake LP| FC
  FC -->|emit stake/withdraw events| MQ --> RS -->|distributeRewards()| FC
  FC -->|record state| DB
  API -->|fetch metrics| DB
  UI -->|display metrics| API
```

***

#### 🚀 4. Farm Deployment & Configuration

**4.1 Deployment Flow**

1. **Select LP Pair** (e.g., OPPAD/ETH, USDT/USDC)
2. **Set Reward Token** (e.g., $OPPAD)
3. **Emission Rate** (per block or per second)
4. **Start & End Blocks**
5. **Deposit Reward Tokens**
6. **Deploy via initializeFarm()**

**4.2 Configuration Parameters**

| Parameter         | Description                        |
| ----------------- | ---------------------------------- |
| LP Token Address  | Contract of the LP pair            |
| Reward Token Addr | Token to distribute                |
| Reward Rate       | Emission per block/second          |
| Start/End Block   | Active duration for the farm       |
| Deposit Amount    | Tokens allocated for emission      |
| Harvest Interval  | Minimum wait between reward claims |

***

#### 🧑‍🌾 5. User Participation

**5.1 Staking LP Tokens**

* Connect via MetaMask/WalletConnect
* Approve LP contract
* Call `deposit(amount)`
* Monitor staking & rewards via dashboard

**5.2 Claiming Rewards**

* Wait for harvest interval
* Call `harvest()`
* Optionally re-stake in a new farm

**5.3 Unstaking**

* Use `withdraw(amount)` for standard exit
* Use `emergencyWithdraw()` to exit instantly (forfeiting pending rewards)

***

#### ⏱️ 6. Reward Scheduler

* **Off-Chain Triggers**: Uses cron or AWS EventBridge
* **On-Chain Distribution**: Calls `updatePool()` and `distribute()`
* **Emits Events**: `RewardPaid`, `PoolUpdated` used for analytics

***

#### 📊 7. Analytics & Monitoring

| Metric       | Description                                         |
| ------------ | --------------------------------------------------- |
| TVL          | Total value of staked LPs (USD equivalent)          |
| APR          | Annualized yield based on current TVL and emissions |
| Live Charts  | Real-time updates via frontend and API              |
| Admin Alerts | Notify if TVL drops or rewards deplete              |

***

#### 🔐 8. Security & Audit

* ✅ Contracts scanned via **OPPAD Shield AI**
* ✅ Manual audit review for public pools
* ✅ `nonReentrant` guards on staking/harvesting
* ✅ Immutable core params (rate, duration)
* ✅ Multisig admin control for pause/migrate

***

#### 🔌 9. Integration & API

**REST Endpoints**

* `GET /farms`: List all active farms
* `GET /farms/{id}/metrics`: Pull TVL/APR/reward stats
* `POST /farms`: Admin-only farm deployment
* `POST /farms/{id}/deposit`: Stake LP
* `POST /farms/{id}/withdraw`: Unstake or harvest

**WebSocket Feeds**

* Subscribe to `Stake`, `Withdraw`, and `RewardPaid` events in real-time

***

> \[!INFO]\
> Farming complements OPPAD staking and NFTs — enabling liquidity providers to **earn yield**, **boost governance access**, and **support early-stage projects** all at once.
