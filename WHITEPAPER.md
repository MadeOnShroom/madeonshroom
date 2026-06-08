# MadeOnShroom Whitepaper

**Version 1.0 — June 2026**

*A non-custodial, fair-launch token launchpad on Solana with unruggable guarantees and creator rewards.*

---

## Contents

1. [Abstract](#abstract)
2. [The Problem](#1-the-problem)
3. [The MadeOnShroom Solution](#2-the-madeonshroom-solution)
4. [Bonding Curve Mechanics](#3-bonding-curve-mechanics)
5. [Token Standard & Supply](#4-token-standard--supply)
6. [Fees & Creator Rewards](#5-fees--creator-rewards)
7. [Security & Unruggable Guarantees](#6-security--unruggable-guarantees)
8. [Technical Architecture](#7-technical-architecture)
9. [Roadmap](#8-roadmap)
10. [Risk & Disclaimer](#9-risk--disclaimer)

---

## Abstract

MadeOnShroom is a **non-custodial, fair-launch token launchpad** on the Solana blockchain. It lets
anyone create a fully on-chain SPL token in seconds and trade it on an automated **bonding curve** —
with no coding, no order book, and no intermediary holding user funds.

Built on the **Meteora Dynamic Bonding Curve (DBC)** program, MadeOnShroom enforces unruggable
guarantees at launch and introduces a **creator rewards model** in which token creators earn a share
of every trade. This paper describes the protocol design, economic model, security properties, and
roadmap.

---

## 1. The Problem

Launching a token has traditionally been technical, expensive, and dangerous for buyers. Most
launches suffer from one or more of these issues:

- **Rug pulls** — creators retain mint authority or pull liquidity, destroying holder value.
- **Custodial risk** — platforms that hold user funds or keys can be hacked, freeze accounts, or disappear.
- **Unaligned incentives** — creators are not rewarded for sustained trading activity, encouraging short-term behavior.
- **Opaque pricing** — hidden fees and unclear mechanics.

---

## 2. The MadeOnShroom Solution

MadeOnShroom addresses these problems with four design principles:

- **Non-custodial by default** — every action is a transaction you sign in your own wallet. The
  platform never holds your SOL, tokens, or keys, and never signs on your behalf.
- **Unruggable at launch** — mint and freeze authority are revoked, metadata is immutable, and
  graduated liquidity is permanently locked — enforced on-chain for every token.
- **Aligned creator rewards** — creators earn 50% of all trading fees on their token, continuously,
  rewarding them for building real, lasting volume.
- **Transparent economics** — a flat creation fee and a flat trading fee, both clearly disclosed and
  identical for every launch.

---

## 3. Bonding Curve Mechanics

Every token trades on a **Meteora Dynamic Bonding Curve** — a fully on-chain pricing program. Price
rises automatically as people buy and falls as people sell. There is no order book and no market
maker.

> **Buy → price up · Sell → price down** — priced continuously by the on-chain curve.

When a token's bonding-curve reserve reaches **~110 SOL**, it *graduates* automatically: a **Meteora
DAMM v2** liquidity pool is created from the accumulated SOL and remaining tokens, and the liquidity
is **100% permanently locked**. The token then continues trading on the DAMM v2 pool — unruggable,
with liquidity no one can withdraw.

---

## 4. Token Standard & Supply

Every token launched on MadeOnShroom shares the same fixed, verifiable parameters:

| Parameter           | Value                       |
| ------------------- | --------------------------- |
| Total supply        | 1,000,000,000 (fixed)       |
| Standard            | SPL token (Solana)          |
| Mint authority      | Revoked at launch           |
| Freeze authority    | Revoked at launch           |
| Metadata            | Immutable                   |
| Starting market cap | Identical for all launches  |

The entire supply is held in the bonding curve at launch, ensuring a fair, identical starting point
with no pre-mine or team allocation.

---

## 5. Fees & Creator Rewards

Creating a token costs a flat **0.025 SOL platform fee** at launch plus a **~0.025 SOL** Solana
network fee (account rent + validator gas), for roughly **0.05 SOL** in total. Every trade carries a
flat **1% fee** on each buy and sell, split evenly between the platform and the token's creator.

| Action         | Platform  | Creator |
| -------------- | --------- | ------- |
| Token creation | 0.025 SOL | —       |
| Buy trade      | 0.5%      | 0.5%    |
| Sell trade     | 0.5%      | 0.5%    |
| Graduation     | Free      | —       |

The 50% / 50% split is fixed on-chain by the bonding-curve config and is identical for every token.
Fees accrue on-chain in SOL and are claimed by the share owner — creators from their Profile →
Rewards, the platform from the Admin panel.

---

## 6. Security & Unruggable Guarantees

Every token enforces the following properties on-chain at launch:

- **Mint authority revoked** — supply is permanently fixed at 1,000,000,000; no one can ever mint more.
- **Freeze authority revoked** — no account can be frozen; tokens cannot be locked or seized.
- **Immutable metadata** — name, symbol, and image cannot be changed after creation.
- **LP locked at graduation** — 100% of migrated liquidity is permanently locked and can never be withdrawn.

---

## 7. Technical Architecture

MadeOnShroom is **non-custodial by design**. All pricing, trading, and graduation logic runs on the
public Meteora DBC program; graduated tokens trade on Meteora DAMM v2. The backend is a **read-only
indexer** that reads public on-chain data (token lists, charts, holders, trade history). It cannot
move funds and is never part of a transaction's signing path.

Meteora DBC program id: `dbcij3LWUppWqq96dh6gJWwBifmcGfLSB5D4DuSMaqN`. Every token, trade, and pool
is independently verifiable on a Solana explorer such as Solscan. A native mobile app (iOS & Android)
provides the same non-custodial experience via Phantom.

---

## 8. Roadmap

| Milestone                  | Description                                                                                  | Status            |
| -------------------------- | -------------------------------------------------------------------------------------------- | ----------------- |
| Live on mainnet            | Non-custodial launchpad, bonding-curve trading, graduation, and creator rewards — shipped.    | Done              |
| Mobile apps                | Native iOS & Android apps submitted to the app stores.                                         | In progress       |
| SHROOM Points & referrals  | On-platform loyalty and referral program with future utility (governance, fee discounts).     | Live / expanding  |
| Ecosystem & integrations   | Deeper analytics, partner integrations, and growth of the token ecosystem.                     | Planned           |

The roadmap is indicative and may evolve. It is not a commitment or a guarantee of future features.

---

## 9. Risk & Disclaimer

**Not financial advice.** Nothing in this document is financial, investment, legal, or tax advice.
Crypto tokens are highly speculative and frequently lose all value. You can lose 100% of the funds you
commit. Only use funds you can afford to lose entirely.

MadeOnShroom provides non-custodial tooling to interact with public on-chain programs. It does not
endorse any token created on the platform and is not responsible for the actions of token creators or
third parties. Always do your own research. See the
[Terms of Service](https://madeonshroom.com/terms) and
[Privacy Policy](https://madeonshroom.com/privacy) for full details.
