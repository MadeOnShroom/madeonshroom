<div align="center">

# 🍄 MadeOnShroom

### A non-custodial, fair-launch token launchpad on Solana and Base

Create, trade, and grow tokens through a fully on-chain bonding curve — on **Solana** and on **Base** — with unruggable guarantees and creator rewards. No coding, no order book, no intermediary ever holding your funds.

[![Solana](https://img.shields.io/badge/Live%20on-Solana-9945FF?logo=solana&logoColor=white)](https://solana.com)
[![Base](https://img.shields.io/badge/Live%20on-Base-0052FF?logo=coinbase&logoColor=white)](https://base.org)
[![Non-custodial](https://img.shields.io/badge/Custody-Non--custodial-FF1A1A)](#-security--unruggable-guarantees)
[![Website](https://img.shields.io/badge/Website-madeonshroom.com-FF1A1A)](https://madeonshroom.com)

[**Website**](https://madeonshroom.com) · [**Whitepaper**](./WHITEPAPER.md) · [**Architecture**](./docs/ARCHITECTURE.md) · [**X / Twitter**](https://x.com/madeonshroom) · [**Telegram**](https://t.me/madeonshroom)

</div>

---

## Overview

**MadeOnShroom** is a **multi-chain token launchpad on Solana and Base**. Anyone can launch a fully
on-chain token in seconds and trade it on an automated **bonding curve** — with no coding, no order
book, and no intermediary holding user funds. On Solana it is built on the **Meteora Dynamic Bonding
Curve (DBC)** program; on Base, tokens trade on an on-chain bonding curve priced in ETH.

The platform is **non-custodial by design**: every action is a transaction you sign in your own
wallet. MadeOnShroom never holds your funds, your tokens, or your keys, and never signs on your behalf.

> ⚠️ This repository is a **public information repository** (overview, whitepaper, and high-level
> architecture). It does **not** contain the application source code, infrastructure, or any secrets.

---

## ✨ Key features

- **Multi-chain — Solana and Base** — launch and trade on either chain from one platform.
- **Non-custodial** — you sign every transaction in your own wallet; the platform never custodies funds or keys.
- **Unruggable at launch** — on Solana, mint & freeze authority are revoked and metadata is immutable; graduated liquidity is permanently locked.
- **Bonding-curve pricing** — price rises as people buy and falls as they sell, fully on-chain, no order book.
- **Creator-set tax (1.5%–6%)** — the creator picks each token's trading tax at launch; the platform keeps a flat 1% and the creator earns the rest on every buy and sell, for the life of the token.
- **Automatic graduation (Solana)** — at ~110 SOL of reserve, liquidity migrates to a Meteora DAMM v2 pool and is permanently locked.
- **Bridge to Base** — bring SOL, ETH, BNB, and other assets onto Base in a few clicks, then grab the official $SHROOM token.
- **Official $SHROOM token** — the platform's own token, live on Base, featured on the home page.
- **Bounties** — post a challenge backed by a real SOL reward held in escrow; the winner is paid only after both the creator and the platform approve.
- **Web + native mobile** — the same experience on the web and on iOS & Android.

---

## ⚙️ How it works

1. **Create** — define your token (name, symbol, image, socials) and pick the chain (**Solana** or
   **Base**) and a trading tax between **1.5% and 6%**. One signed transaction launches it on an
   on-chain bonding curve.
2. **Trade** — buyers and sellers trade against the bonding curve. Price is determined continuously by
   the on-chain curve — `buy → price up`, `sell → price down`.
3. **Graduate (Solana)** — when a Solana token's reserve reaches **~110 SOL**, it automatically
   migrates to a **Meteora DAMM v2** liquidity pool, and 100% of that liquidity is **permanently locked**.

### Token standard

| Parameter           | Value                                          |
| ------------------- | ---------------------------------------------- |
| Total supply        | 1,000,000,000 per launched token (fixed)       |
| Standard            | SPL token (Solana) · ERC-20 (Base)             |
| Mint authority      | Revoked at launch (Solana)                     |
| Freeze authority    | Revoked at launch (Solana)                     |
| Metadata            | Immutable (Solana)                             |
| Starting market cap | Identical for every launch                     |

No pre-mine, no team allocation — the entire supply sits in the bonding curve at launch.

---

## 💰 Fees & taxes

Creating a token on **Solana** costs a flat **0.025 SOL platform fee** plus a **~0.025 SOL** Solana
network fee (account rent + validator gas) — roughly **0.05 SOL** in total. Creating on **Base** costs
a small ETH creation fee plus network gas.

Each token carries a **trading tax chosen by its creator at launch — anywhere from 1.5% to 6%** on
every buy and sell, fixed on-chain. On every trade the **platform always keeps a flat 1%** and the
**creator earns the remainder**. The same rate applies before and after a Solana token graduates to
its Meteora DAMM v2 pool — so a higher tax means a bigger creator share on every trade, for the life
of the token.

| Action                                | Platform  | Creator |
| ------------------------------------- | --------- | ------- |
| Token creation (Solana)               | 0.025 SOL | —       |
| Buy / sell — tax set to 1.5%          | 1%        | 0.5%    |
| Buy / sell — tax set to 6%            | 1%        | 5%      |
| Graduation                            | Free      | —       |

Trading fees accrue on-chain and are claimed by their respective owner — creators from their
**Profile → Rewards**, the platform from the **Admin panel**.

---

## 🌉 Bridge to Base

The **Bridge** lets anyone move funds onto Base in a few clicks, then buy the official $SHROOM token:

1. **Bridge** — bring **SOL, ETH, BNB, and other assets** from their native chain to **ETH on Base**,
   powered by [deBridge](https://debridge.finance) (non-custodial — you connect your own wallet).
2. **Buy** — swap your Base ETH for **$SHROOM** on Uniswap (set slippage above the token's transfer
   tax).

---

## ⭐ Official $SHROOM token

The platform's official token, **$SHROOM**, is live on **Base** and featured on the home page.

| Parameter      | Value                                          |
| -------------- | ---------------------------------------------- |
| Chain          | Base                                           |
| Total supply   | 1,000,000                                      |
| Transfer tax   | 5% (3% ETH rewards · 1% burn · 1% marketing)   |
| Max wallet / tx| None                                           |

Buy on [Uniswap (Base)](https://app.uniswap.org/swap?chain=base) and verify the contract on
[Basescan](https://basescan.org).

---

## 🎯 Bounties

Bounties turn community actions into on-chain challenges with a real reward. Anyone can post a task,
back it with a SOL reward, and pay it out to whoever proves they completed it.

1. **Post** — a creator describes the challenge, sets the SOL reward and a deadline, and signs one
   transaction that sends the **reward + a flat 0.1 SOL platform fee** to the platform escrow wallet.
   The deposit is verified on-chain before the bounty goes live.
2. **Submit** — participants submit photo/video proof of completion.
3. **Approve & pay** — a winning submission must be approved by **both** the creator **and** the
   platform team. The reward is then paid to the winner, and the payout transaction is recorded
   on-chain for transparency.
4. **Refund** — if the deadline passes with no approved winner, the **reward is refunded to the
   creator**. The flat 0.1 SOL fee is non-refundable.

> ⚠️ **Custody note.** Unlike token creation and trading — which are fully non-custodial — a bounty
> **reward is held in escrow by the platform wallet** between posting and payout. Every escrow
> deposit, payout, and refund is an on-chain transfer you can verify on a block explorer.

---

## 🛡️ Security & unruggable guarantees

On **Solana**, every token enforces the following **on-chain at launch**:

- **Mint authority revoked** — supply is permanently fixed; no one can ever mint more.
- **Freeze authority revoked** — no account can be frozen; tokens cannot be locked or seized.
- **Immutable metadata** — name, symbol, and image cannot be changed after creation.
- **LP locked at graduation** — 100% of migrated liquidity is permanently locked and can never be withdrawn.

On **Base**, tokens are standard ERC-20s that trade on an on-chain bonding curve. Every token, trade,
and pool is independently verifiable on a public explorer such as [Solscan](https://solscan.io)
(Solana) or [Basescan](https://basescan.org) (Base). To report a vulnerability, see
[SECURITY.md](./SECURITY.md).

---

## 🏗️ Architecture (high level)

MadeOnShroom is non-custodial: all pricing, trading, and graduation logic runs on **public on-chain
programs and contracts** (Meteora DBC, then DAMM v2 after graduation, on Solana; on-chain bonding-curve
contracts on Base). A **read-only indexer** serves public on-chain data (token lists, charts, holders,
trade history) — it cannot move funds and is never part of a transaction's signing path.

See [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md) for the full overview.

---

## 📚 Documentation

- [Whitepaper](./WHITEPAPER.md) — protocol design, economics, security, and roadmap
- [Architecture](./docs/ARCHITECTURE.md) — how the system fits together
- [Security policy](./SECURITY.md) — responsible disclosure
- [Terms of Service](https://madeonshroom.com/terms) · [Privacy Policy](https://madeonshroom.com/privacy)

---

## ⚠️ Disclaimer

Nothing in this repository is financial, investment, legal, or tax advice. Crypto tokens are highly
speculative and frequently lose all value — you can lose 100% of the funds you commit. MadeOnShroom
provides non-custodial tooling to interact with public on-chain programs; it does not endorse any
token created on the platform and is not responsible for the actions of token creators or third
parties. Always do your own research.

---

<div align="center">

© 2026 MadeOnShroom. All rights reserved. See [LICENSE](./LICENSE).

</div>
