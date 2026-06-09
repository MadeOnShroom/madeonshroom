# Architecture Overview

> High-level, public overview only. This document intentionally omits source code, internal
> file structure, infrastructure details, and any secrets or credentials.

MadeOnShroom is **non-custodial by design**. The platform never holds user funds or keys and is never
part of a transaction's signing path. All value-bearing logic lives in **public on-chain programs**;
the off-chain components are read-only.

## Components

### 1. On-chain programs (source of truth)

- **Meteora Dynamic Bonding Curve (DBC)** — handles token creation, bonding-curve pricing, buys,
  sells, and graduation. Program id: `dbcij3LWUppWqq96dh6gJWwBifmcGfLSB5D4DuSMaqN`.
- **Meteora DAMM v2** — after a token graduates (~110 SOL reserve), liquidity migrates here and is
  permanently locked. The token continues trading on this pool at a 0.25% fee, split 30% platform /
  70% creator (vs. 1% split 50/50 on the bonding curve).

All token, trade, and pool state is public and independently verifiable on a Solana explorer.

### 2. Client applications (transaction builders)

The web app and the native mobile app build unsigned transactions and hand them to the user's wallet
to sign. The wallet — not the platform — holds the keys and authorizes every action.

- **Web** — the user signs with a connected Solana wallet.
- **Mobile (iOS & Android)** — the same non-custodial flow via Phantom.

### 3. Read-only indexer (data only)

A backend service indexes **public on-chain data** to power fast, convenient reads:

- Token lists and discovery (trending, new, top volume, graduated)
- Price charts and historical snapshots
- Holder distributions
- Trade history

The indexer **cannot move funds**, never holds SOL or private keys, and is never on a transaction's
signing path. If it were unavailable, on-chain trading would still function directly against the
programs.

## Non-custodial flow (create / trade)

```
User wallet  ──signs──▶  On-chain program (Meteora DBC / DAMM v2)
     ▲                              │
     │ unsigned tx                  │ public state
     │                              ▼
 Client app  ◀──reads──────  Read-only indexer
```

1. The client builds an unsigned transaction (create, buy, or sell).
2. The user reviews and signs it in their own wallet.
3. The signed transaction is submitted to Solana and executed by the on-chain program.
4. The indexer observes the resulting public on-chain state and serves it back to clients.

## Trust model

- **No custody** — the platform cannot access, freeze, or move user funds.
- **Unruggable tokens** — mint/freeze authority revoked, metadata immutable, graduated LP locked.
- **Verifiable** — every action settles on-chain and can be checked on a public explorer.

## Out of scope for this repository

Application source code, deployment and infrastructure configuration, environment variables, RPC
provider endpoints, wallet addresses, and any other operational secrets are **not** published here.
