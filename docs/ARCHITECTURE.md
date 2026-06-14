# Architecture Overview

> High-level, public overview only. This document intentionally omits source code, internal
> file structure, infrastructure details, and any secrets or credentials.

MadeOnShroom is a **multi-chain launchpad on Solana and Base** and is **non-custodial by design**. The
platform never holds user funds or keys and is never part of a transaction's signing path. All
value-bearing logic lives in **public on-chain programs and contracts**; the off-chain components are
read-only.

## Components

### 1. On-chain programs & contracts (source of truth)

**Solana**

- **Meteora Dynamic Bonding Curve (DBC)** — handles token creation, bonding-curve pricing, buys,
  sells, and graduation. Program id: `dbcij3LWUppWqq96dh6gJWwBifmcGfLSB5D4DuSMaqN`.
- **Meteora DAMM v2** — after a token graduates (~110 SOL reserve), liquidity migrates here and is
  permanently locked. The token continues trading on this pool.

**Base**

- **On-chain bonding-curve contracts** — token creation and bonding-curve pricing (buys/sells) in ETH.
  Tokens are standard ERC-20s.
- **Uniswap V2** — after a token graduates (~$50k fully-diluted value), it trades on a Uniswap V2 pair;
  the creator-chosen tax keeps applying as a transfer tax.

Each token carries a creator-chosen trading tax of **1.5%–6%**: the platform keeps a flat 1% and the
creator earns the remainder, fixed on-chain. All token, trade, and pool state is public and
independently verifiable on a block explorer (Solscan on Solana, Basescan on Base).

### 2. Client applications (transaction builders)

The web app and the native mobile app build unsigned transactions and hand them to the user's wallet
to sign. The wallet — not the platform — holds the keys and authorizes every action.

- **Web** — the user signs with a connected wallet: a Solana wallet (e.g. Phantom) for Solana, or an
  EVM wallet (WalletConnect / browser wallets) for Base.
- **Mobile (iOS & Android)** — the same non-custodial flow.

### 3. Read-only indexer (data only)

A backend service indexes **public on-chain data** to power fast, convenient reads:

- Token lists and discovery (trending, new, top volume, graduated) across both chains
- Price charts and historical snapshots
- Holder distributions
- Trade history

The indexer **cannot move funds**, never holds private keys, and is never on a transaction's
signing path. If it were unavailable, on-chain trading would still function directly against the
programs.

### 4. Bridge to Base (third-party, non-custodial)

The Bridge lets users move **SOL, ETH, BNB, and other assets** onto **ETH on Base**, then swap into
tokens on Base. It is powered by a third-party bridge (deBridge) embedded as an isolated widget — the
user connects their own wallet and the platform never takes custody of bridged funds.

### 5. Bounty escrow (the one custodial component)

Bounties let a creator post a SOL-backed challenge. Unlike token creation and trading, a bounty
reward is **held in escrow by the platform wallet** between posting and settlement — this is the only
deliberately custodial part of the platform.

- **Deposit.** The creator signs a transfer of the **reward + a flat 0.1 SOL fee** to the platform
  escrow wallet. The backend verifies the transfer on-chain (correct destination, sender, and amount)
  before activating the bounty.
- **Approval.** A winning submission must be approved by **both the creator and the platform team**.
- **Settlement.** The platform pays the approved winner (or, after the deadline with no winner,
  refunds the creator) and records the on-chain transaction. The flat fee is non-refundable.

The backend still **never holds private keys** and never signs a deposit on a user's behalf — it only
verifies that the expected on-chain transfers happened. Every deposit, payout, and refund is a public
transfer verifiable on an explorer.

## Non-custodial flow (create / trade)

```
User wallet  ──signs──▶  On-chain program (Meteora DBC / DAMM v2 on Solana · bonding curve / Uniswap V2 on Base)
     ▲                              │
     │ unsigned tx                  │ public state
     │                              ▼
 Client app  ◀──reads──────  Read-only indexer
```

1. The client builds an unsigned transaction (create, buy, or sell) for the selected chain.
2. The user reviews and signs it in their own wallet.
3. The signed transaction is submitted to Solana or Base and executed by the on-chain program.
4. The indexer observes the resulting public on-chain state and serves it back to clients.

## Trust model

- **No custody** — the platform cannot access, freeze, or move user funds.
- **Unruggable tokens (Solana)** — mint/freeze authority revoked, metadata immutable, graduated LP locked.
- **Verifiable** — every action settles on-chain and can be checked on a public explorer.

## Out of scope for this repository

Application source code, deployment and infrastructure configuration, environment variables, RPC
provider endpoints, wallet addresses, and any other operational secrets are **not** published here.
