# MadeOnShroom Whitepaper

**Version 1.1 — June 2026**

*A non-custodial, fair-launch token launchpad on Solana and Base, with unruggable guarantees and creator rewards.*

---

## Contents

1. [Abstract](#abstract)
2. [The Problem](#1-the-problem)
3. [The MadeOnShroom Solution](#2-the-madeonshroom-solution)
4. [Bonding Curve Mechanics](#3-bonding-curve-mechanics)
5. [Token Standard & Supply](#4-token-standard--supply)
6. [Fees, Taxes & Creator Rewards](#5-fees-taxes--creator-rewards)
7. [Bridge to Base & the Official $SHROOM Token](#6-bridge-to-base--the-official-shroom-token)
8. [Bounties (Escrow Challenges)](#7-bounties-escrow-challenges)
9. [Security & Unruggable Guarantees](#8-security--unruggable-guarantees)
10. [Technical Architecture](#9-technical-architecture)
11. [Roadmap](#10-roadmap)
12. [Risk & Disclaimer](#11-risk--disclaimer)

---

## Abstract

MadeOnShroom is a **non-custodial, fair-launch token launchpad** on **Solana and Base**. It lets
anyone create a fully on-chain token in seconds and trade it on an automated **bonding curve** — with
no coding, no order book, and no intermediary holding user funds.

On Solana, MadeOnShroom is built on the **Meteora Dynamic Bonding Curve (DBC)** program; on Base,
tokens trade on an on-chain bonding curve priced in ETH. Across both chains the platform enforces
unruggable guarantees and a **creator rewards model** in which token creators set their token's
trading tax and earn a share of every trade. This paper describes the protocol design, economic
model, security properties, and roadmap.

---

## 1. The Problem

Launching a token has traditionally been technical, expensive, and dangerous for buyers. Most
launches suffer from one or more of these issues:

- **Rug pulls** — creators retain mint authority or pull liquidity, destroying holder value.
- **Custodial risk** — platforms that hold user funds or keys can be hacked, freeze accounts, or disappear.
- **Unaligned incentives** — creators are not rewarded for sustained trading activity, encouraging short-term behavior.
- **Opaque pricing** — hidden fees and unclear mechanics.
- **Chain silos** — most launchpads live on a single chain, splitting communities and liquidity.

---

## 2. The MadeOnShroom Solution

MadeOnShroom addresses these problems with five design principles:

- **Multi-chain by default** — the same launchpad runs natively on **Solana and Base**, so creators
  reach both communities from one platform.
- **Non-custodial by default** — every action is a transaction you sign in your own wallet. The
  platform never holds your funds, tokens, or keys, and never signs on your behalf.
- **Unruggable at launch** — on Solana, mint and freeze authority are revoked, metadata is immutable,
  and graduated liquidity is permanently locked — enforced on-chain for every token.
- **Aligned creator rewards** — the creator chooses each token's trading tax (1.5%–6%); the platform
  keeps a flat 1% and the creator earns the remainder on every trade, rewarding them for building
  real, lasting volume.
- **Transparent economics** — a small creation fee and a clearly disclosed, creator-chosen trading tax.

---

## 3. Bonding Curve Mechanics

Every token trades on an **on-chain bonding curve** — a fully on-chain pricing program. Price rises
automatically as people buy and falls as people sell. There is no order book and no market maker.

> **Buy → price up · Sell → price down** — priced continuously by the on-chain curve.

On **Solana**, tokens run on the **Meteora Dynamic Bonding Curve**. When a token's reserve reaches
**~110 SOL**, it *graduates* automatically: a **Meteora DAMM v2** liquidity pool is created from the
accumulated SOL and remaining tokens, and the liquidity is **100% permanently locked**. The token
then continues trading on the DAMM v2 pool — unruggable, with liquidity no one can withdraw.

On **Base**, tokens trade on an on-chain bonding curve priced in ETH. When a token reaches its
graduation target (~$50k fully-diluted value) it *graduates* automatically to a **Uniswap V2** pair,
where the creator-chosen tax keeps applying as a transfer tax — the same non-custodial,
creator-rewards model.

---

## 4. Token Standard & Supply

Every token launched on MadeOnShroom shares the same fixed, verifiable parameters:

| Parameter           | Value                                      |
| ------------------- | ------------------------------------------ |
| Total supply        | 1,000,000,000 per launched token (fixed)   |
| Standard            | SPL token (Solana) · ERC-20 (Base)         |
| Mint authority      | Revoked at launch (Solana)                 |
| Freeze authority    | Revoked at launch (Solana)                 |
| Metadata            | Immutable (Solana)                         |
| Starting market cap | Identical for all launches                 |

The entire supply is held in the bonding curve at launch, ensuring a fair, identical starting point
with no pre-mine or team allocation.

---

## 5. Fees, Taxes & Creator Rewards

Creating a token on **Solana** costs a flat **0.025 SOL platform fee** at launch plus a **~0.025 SOL**
Solana network fee (account rent + validator gas), for roughly **0.05 SOL** in total. Creating on
**Base** costs a small ETH creation fee plus network gas.

Each token carries a **trading tax chosen by its creator at launch — from 1.5% to 6%** on every buy
and sell, fixed on-chain. On each trade the **platform always keeps a flat 1%** and the **creator
earns the remainder**. The same rate applies before and after a Solana token graduates to its Meteora
DAMM v2 pool — so the creator earns their share on every trade, for the life of the token.

| Action                                | Platform  | Creator |
| ------------------------------------- | --------- | ------- |
| Token creation (Solana)               | 0.025 SOL | —       |
| Buy / sell — tax set to 1.5%          | 1%        | 0.5%    |
| Buy / sell — tax set to 6%            | 1%        | 5%      |
| Graduation                            | Free      | —       |

The platform's flat 1% is fixed on-chain; the creator's share is whatever remains of the tax they
chose. Fees accrue on-chain and are claimed by the share owner — creators from their Profile →
Rewards, the platform from the Admin panel.

---

## 6. Bridge to Base & the Official $SHROOM Token

To make it easy to get onto Base, MadeOnShroom includes a **Bridge**. Users can move **SOL, ETH, BNB,
and other assets** from their native chain to **ETH on Base** in a few clicks (powered by deBridge,
fully non-custodial), then swap that ETH for tokens on Base.

The platform's **official $SHROOM token** is live on **Base** and featured on the home page:

| Parameter       | Value                                        |
| --------------- | -------------------------------------------- |
| Chain           | Base                                         |
| Total supply    | 1,000,000                                    |
| Transfer tax    | 5% (3% ETH rewards · 1% burn · 1% marketing) |
| Max wallet / tx | None                                         |

$SHROOM trades on Uniswap (Base) and is fully verifiable on Basescan.

---

## 7. Bounties (Escrow Challenges)

Bounties extend MadeOnShroom beyond trading: they let anyone post a **challenge backed by a real SOL
reward** and pay it out to whoever proves they completed it. They are designed to drive community
participation — content, tasks, milestones — with a transparent, on-chain reward.

**Lifecycle**

1. **Post.** A creator describes the challenge, chooses the SOL reward freely, and sets a deadline.
   They sign a single transaction that transfers the **reward plus a flat 0.1 SOL platform fee** to
   the platform escrow wallet. The backend verifies this deposit on-chain before activating the
   bounty.
2. **Submit.** Participants submit photo or video proof of completion.
3. **Approve & pay.** A winning submission requires approval from **both the creator and the platform
   team**. Once both approve, the reward is paid to the winner and the payout transaction is recorded
   on-chain.
4. **Refund.** If the deadline passes without an approved winner, the reward is **refunded to the
   creator**. The flat 0.1 SOL fee is non-refundable.

| Item         | Value                                                 |
| ------------ | ----------------------------------------------------- |
| Reward       | Chosen freely by the creator                          |
| Platform fee | Flat **0.1 SOL** per bounty (non-refundable)          |
| Approval     | Creator **and** platform must both approve the winner |
| On expiry    | Reward refunded to the creator                        |

**Custody model.** Unlike token creation and trading — which are fully non-custodial — a bounty
reward is **held in escrow by the platform wallet** between posting and settlement. This is the one
deliberately custodial part of the protocol, required so the reward is guaranteed to exist when a
winner is approved. The backend never holds private keys: every escrow deposit, payout, and refund is
an ordinary on-chain transfer that is verified server-side and independently checkable on an explorer.

---

## 8. Security & Unruggable Guarantees

On **Solana**, every token enforces the following properties on-chain at launch:

- **Mint authority revoked** — supply is permanently fixed at 1,000,000,000; no one can ever mint more.
- **Freeze authority revoked** — no account can be frozen; tokens cannot be locked or seized.
- **Immutable metadata** — name, symbol, and image cannot be changed after creation.
- **LP locked at graduation** — 100% of migrated liquidity is permanently locked and can never be withdrawn.

On **Base**, tokens are standard ERC-20s trading on an on-chain bonding curve that graduates to a
Uniswap V2 pair at ~$50k fully-diluted value; all activity is public and verifiable on Basescan.

---

## 9. Technical Architecture

MadeOnShroom is **non-custodial by design**. All pricing, trading, and graduation logic runs on
public on-chain programs and contracts: the Meteora DBC program on Solana (graduated tokens trade on
Meteora DAMM v2), and on-chain bonding-curve contracts on Base that graduate to a Uniswap V2 pair at
~$50k fully-diluted value (the creator tax continues as a transfer tax). The backend is a **read-only indexer**
that reads public on-chain data (token lists, charts, holders, trade history). It cannot move funds
and is never part of a transaction's signing path.

Meteora DBC program id (Solana): `dbcij3LWUppWqq96dh6gJWwBifmcGfLSB5D4DuSMaqN`. Every token, trade,
and pool is independently verifiable on a public explorer (Solscan on Solana, Basescan on Base). A
native mobile app (iOS & Android) provides the same non-custodial experience.

---

## 10. Roadmap

| Milestone                  | Description                                                                                  | Status            |
| -------------------------- | -------------------------------------------------------------------------------------------- | ----------------- |
| Live on Solana             | Non-custodial launchpad, bonding-curve trading, graduation, and creator rewards — shipped.    | Done              |
| Live on Base               | Multi-chain launchpad with on-chain bonding-curve trading on Base — shipped.                   | Done              |
| Bridge to Base             | In-app, non-custodial bridge from Solana, Ethereum, BNB and more onto Base — shipped.          | Done              |
| Mobile apps                | Native iOS & Android apps submitted to the app stores.                                         | In progress       |
| Ecosystem & integrations   | Deeper analytics, partner integrations, and growth of the token ecosystem across both chains.  | Planned           |

The roadmap is indicative and may evolve. It is not a commitment or a guarantee of future features.

---

## 11. Risk & Disclaimer

**Not financial advice.** Nothing in this document is financial, investment, legal, or tax advice.
Crypto tokens are highly speculative and frequently lose all value. You can lose 100% of the funds you
commit. Only use funds you can afford to lose entirely.

MadeOnShroom provides non-custodial tooling to interact with public on-chain programs. It does not
endorse any token created on the platform and is not responsible for the actions of token creators or
third parties. Always do your own research. See the
[Terms of Service](https://madeonshroom.com/terms) and
[Privacy Policy](https://madeonshroom.com/privacy) for full details.
