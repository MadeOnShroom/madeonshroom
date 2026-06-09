<div align="center">

# 🍄 MadeOnShroom

### A non-custodial, fair-launch token launchpad on Solana

Create, trade, and grow tokens through a fully on-chain bonding curve — with unruggable guarantees and creator rewards. No coding, no order book, no intermediary ever holding your funds.

[![Solana](https://img.shields.io/badge/Built%20on-Solana-9945FF?logo=solana&logoColor=white)](https://solana.com)
[![Network](https://img.shields.io/badge/Network-Mainnet-14F195)](https://madeonshroom.com)
[![Non-custodial](https://img.shields.io/badge/Custody-Non--custodial-FF1A1A)](#-security--unruggable-guarantees)
[![Website](https://img.shields.io/badge/Website-madeonshroom.com-FF1A1A)](https://madeonshroom.com)

[**Website**](https://madeonshroom.com) · [**Whitepaper**](./WHITEPAPER.md) · [**Architecture**](./docs/ARCHITECTURE.md) · [**X / Twitter**](https://x.com/madeonshroom) · [**Telegram**](https://t.me/madeonshroom)

</div>

---

## Overview

**MadeOnShroom** lets anyone launch a fully on-chain SPL token in seconds and trade it on an
automated bonding curve. It is built on the **Meteora Dynamic Bonding Curve (DBC)** program and
enforces unruggable guarantees at launch, while rewarding creators with a share of every trade.

The platform is **non-custodial by design**: every action is a transaction you sign in your own
wallet. MadeOnShroom never holds your SOL, your tokens, or your keys, and never signs on your behalf.

> ⚠️ This repository is a **public information repository** (overview, whitepaper, and high-level
> architecture). It does **not** contain the application source code, infrastructure, or any secrets.

---

## ✨ Key features

- **Non-custodial** — you sign every transaction in your own wallet; the platform never custodies funds or keys.
- **Unruggable at launch** — mint & freeze authority revoked, metadata immutable, graduated liquidity permanently locked.
- **Bonding-curve pricing** — price rises as people buy and falls as they sell, fully on-chain, no order book.
- **Creator rewards** — creators earn 50% of trading fees on the bonding curve, then the larger 70% share after graduation, continuously.
- **Automatic graduation** — at ~110 SOL of reserve, liquidity migrates to a Meteora DAMM v2 pool and is locked.
- **Transparent economics** — a flat creation fee and a flat trading fee, identical for every launch.
- **Web + native mobile** — the same non-custodial experience on the web and on iOS & Android.

---

## ⚙️ How it works

1. **Create** — define your token (name, symbol, image, socials). The transaction mints a fixed supply
   of **1,000,000,000** tokens and revokes mint & freeze authority on-chain.
2. **Trade** — buyers and sellers trade against the bonding curve. Price is determined continuously by
   the on-chain curve — `buy → price up`, `sell → price down`.
3. **Graduate** — when the curve's reserve reaches **~110 SOL**, the token automatically migrates to a
   **Meteora DAMM v2** liquidity pool, and 100% of that liquidity is **permanently locked**.

### Token standard

| Parameter           | Value                          |
| ------------------- | ------------------------------ |
| Total supply        | 1,000,000,000 (fixed)          |
| Standard            | SPL token (Solana)             |
| Mint authority      | Revoked at launch              |
| Freeze authority    | Revoked at launch              |
| Metadata            | Immutable                      |
| Starting market cap | Identical for every launch     |

No pre-mine, no team allocation — the entire supply sits in the bonding curve at launch.

---

## 💰 Fees

Creating a token costs a flat **0.025 SOL platform fee** plus a **~0.025 SOL** Solana network fee
(account rent + validator gas) — roughly **0.05 SOL** in total. During the bonding-curve phase, every
trade carries a flat **1% fee** split evenly (**50% platform / 50% creator**). After graduation to a
Meteora DAMM v2 pool, the fee is **0.25%**, split **30% platform / 70% creator**.

| Action                                   | Platform  | Creator |
| ---------------------------------------- | --------- | ------- |
| Token creation                           | 0.025 SOL | —       |
| Buy / sell — bonding curve (1%)          | 0.5%      | 0.5%    |
| Buy / sell — after graduation (0.25%)    | 0.075%    | 0.175%  |
| Graduation                               | Free      | —       |

The splits are fixed on-chain and identical for every token — 50% / 50% on the 1% bonding-curve fee,
then 30% platform / 70% creator on the 0.25% fee after graduation. Fees accrue on-chain in SOL and
are claimed by their respective owner.

---

## 🛡️ Security & unruggable guarantees

Every token enforces the following **on-chain at launch**:

- **Mint authority revoked** — supply is permanently fixed; no one can ever mint more.
- **Freeze authority revoked** — no account can be frozen; tokens cannot be locked or seized.
- **Immutable metadata** — name, symbol, and image cannot be changed after creation.
- **LP locked at graduation** — 100% of migrated liquidity is permanently locked and can never be withdrawn.

Every token, trade, and pool is independently verifiable on a Solana explorer such as
[Solscan](https://solscan.io). To report a vulnerability, see [SECURITY.md](./SECURITY.md).

---

## 🏗️ Architecture (high level)

MadeOnShroom is non-custodial: all pricing, trading, and graduation logic runs on **public Solana
programs** (Meteora DBC, then DAMM v2 after graduation). A **read-only indexer** serves public
on-chain data (token lists, charts, holders, trade history) — it cannot move funds and is never part
of a transaction's signing path.

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
