---
id: rails.maps.route-map
lang: en
title: Route Map — Exchanges, Chains, Corridors (measured basis)
status: verified (only where marked) / unobserved (the rest)
as_of: 2026-09-12
freshness_note: "Fees and door status go stale weekly. Latest values = nw_kg_facts(venue:%) / get_pair_gate. This map holds the structure and verified corridors"
sources: [QM_RAIL_LOG.md, project_transfer_intelligence, project_qm_rail_kg, feedback_fee_discipline_rails]
contributors: [house]
tier_candidate: commons
---

# Route Map

## 1. Overall structure (solid line = actual transfer verified, dotted line = permitted by rule but unverified)

```mermaid
graph LR
  subgraph KR[Korea leg — Travel Rule]
    BITHUMB[bithumb<br/>single wallet · address-book pre-registration · 1% withdrawal fee added on top]
    UPBIT[upbit<br/>single wallet · whitelist, 320 pairs]
  end
  subgraph GLOBAL[Global hubs]
    BINANCE[binance<br/>10 buckets · withdraw=spot · no procedure]
    BYBIT[bybit<br/>2 buckets · withdraw=FUND · address registration]
    MEXC[mexc<br/>single · no procedure]
    GATE[gate<br/>single · manual withdrawal per currency×chain×address, 1x+24h]
    KUCOIN[kucoin<br/>withdraw=main]
    OKX[okx<br/>withdraw=funding]
    BITGET[bitget]
  end
  HUB((hub EOA<br/>own wallet))

  BINANCE ==>|KAIA 0.02 · 99s| BITHUMB
  BINANCE -.->|TRX 1.5 (75x)| BITHUMB
  BINANCE ==>|BSC 0.01 · 81s| BYBIT
  BINANCE ==>|SOL 0.30 · 141s| BYBIT
  MEXC ==>|BSC 0.01 · 80s| BINANCE
  MEXC ==>|ETH/ARB ~0 · 70s| HUB
  HUB ==>|gas $0.0024| GATE
  GATE ==>|0.025 (1/20 of direct withdrawal fee 0.5)| HUB
  BYBIT -.->|ERC20 $0.8 / KAIA $0.1 / PLASMA $0| BINANCE
  BYBIT -.->|TRX 1.0 · address registration required| BITHUMB
  KUCOIN ==>|BEP20 fee 30 deducted · 151s| GATE
  BITGET -.->|Travel Rule OK| BITHUMB
  OKX -.->|Travel Rule OK| BITHUMB
  GATE -.->|<₩1M per transaction · 7 business days to register| BITHUMB
  MEXC x--x|Travel Rule blocked| BITHUMB
  KUCOIN x--x|Travel Rule blocked| BITHUMB
```

## 2. Corridor table (measured only — dated)

| From → To | Chain | Quoted fee | Actual deduction | Delay | Result | Measured on |
|---|---|---|---|---|---|---|
| binance → bithumb | **KAIA** | 0.02 USDT | 0.02 | 99s | ok | 2026-08-08 |
| binance → bithumb | TRX | 1.5 | — | — | not recommended (75x KAIA) | 2026-08-08 |
| binance → bybit | **BSC** | 0.01 | 0.01 match | 1m21s | ok, no 2FA | 2026-08-02 |
| binance → bybit | SOL | 0.30 | 0.30 match | 2m21s | ok (30x more expensive than BSC) | 2026-08-02 |
| mexc → binance | BSC | 0.01 | 0.01 match | 80s | ok (netWork code required) | 2026-08-03 |
| mexc → hub EOA | ETH/ARB | 0.00000084 | — | 70s | ok | 2026-08-08 |
| hub EOA → gate | (on-chain gas) | $0.0024 | — | — | ok | 2026-08-08 |
| gate → hub EOA | — | 0.025 | — | — | ok (1/20 of direct CEX withdrawal fee 0.5) | 2026-08-08 |
| kucoin → gate | BEP20 | 30 (deducted) | 30 | 151s | ok (EGL1 recovery) | 2026-08-30 |
| bybit → bithumb | TRX | 1.0 (min 2.6, 20 blocks) | — | — | **needs_address_registration** — funds did not move | 2026-08-02 |
| bithumb → binance | — | flat 1% **added on top** | requested amount+1% | — | ok (SAPIEN 3,600 → arrived 3,565) | 2026-08-30 |

Principle: **on-chain leg cost is 1/200–1/400 of exchange withdrawal fees.** The hub EOA pattern (CEX → own wallet → any CEX) collapses per-destination address registration down to a single wallet.

## 3. Korea leg — the bottleneck is here

- **Bithumb USDT-accepting chains**: ETH · TRX · KAIA · APT (confirmed 2026-08-08. As of 08-02 only TRX deposits succeeded / BSC·SOL·MATIC·BASE returned 400 — this is not more chains opening up, it's more observation. Latest = KG)
- **KAIA is the lowest-cost route to Korea**: 0.02 vs TRX 1.5
- **Bithumb withdrawal = flat 1% (254 tickers) / fixed amount (14 tickers) / 0 (BTT-TRX·TT)**, and **added on top of the requested amount** → what looked like a phantom remainder in settlement was this fee ([[../lessons/what-generalises]] #2)
- **Bithumb address book = pre-registration per (address+asset)**, 0 hits via API lookup (mismatch with the UI) — check registration status in the UI
- **Upbit whitelist, 320 pairs**, 259 ETH-chain pairs opened under `chain_policy_mode=fee_known_and_hedged` (2026-09-06). Upbit→gate registered pairs: 14 (ARB·TRX). The bottleneck isn't Upbit, it's our list of sell destinations (gateio opening in progress)
- **Bithumb leg is the bottleneck in many cases** (XCN $5k, bithumb 8.29pp) — grading only the overseas side is forbidden

## 4. Travel Rule connectivity (bithumb basis)
- Free transfer (Travel Rule-linked), **10 venues**: bitget · bybit · okx · binance · HTX · Toobit + (4 more from the rail_atlas 8/1 list) — HTX·Toobit are missing from the 8/1 atlas, code update pending
- Not possible: mexc · gate (mid tier) · kucoin
- **Gate = mid tier**: CODE-linked (2024-03) but not activated on bithumb's side → treated as "other exchange" = address pre-registration (7 business days) then **<₩1M per transaction**, repeated-withdrawal monitoring clause → **no standing bot pipeline, occasional only**
- **Unregistered (blocked), confirmed 41 venues** (BingX added 2026-01-12, includes BitMart·WEEX·Blofin·CoinW) — cannot register, no re-investigation
- Workaround pending: mexc → OKX → bithumb (once the OKX adapter is complete)

## 5. Machine-readable corridor definitions (verified only)

```yaml
corridors:
  - {from: binance, to: bithumb, chain: KAIA, fee_usdt: 0.02, transit_s: 99, status: verified, as_of: 2026-08-08, default: true}
  - {from: binance, to: bithumb, chain: TRX,  fee_usdt: 1.5,  status: avoid, reason: "75x KAIA"}
  - {from: binance, to: bybit,   chain: BSC,  fee_usdt: 0.01, transit_s: 81,  status: verified, as_of: 2026-08-02, default: true}
  - {from: binance, to: bybit,   chain: SOL,  fee_usdt: 0.30, transit_s: 141, status: verified, as_of: 2026-08-02}
  - {from: mexc,    to: binance, chain: BSC,  fee_usdt: 0.01, transit_s: 80,  status: verified, as_of: 2026-08-03, note: "netWork code required (display name forbidden)"}
  - {from: kucoin,  to: gateio,  chain: BEP20, fee_token: 30, transit_s: 151, status: verified, as_of: 2026-08-30, fee_model: deduct}
  - {from: bybit,   to: bithumb, chain: TRX,  fee_usdt: 1.0, min: 2.6, status: blocked_until_address_registration, as_of: 2026-08-02}
  - {from: bithumb, to: binance, chain: "*",  fee_pct: 1.0, fee_model: add_on_top, status: verified, as_of: 2026-08-30}
  - {from: bybit,   to: binance, chain: PLASMA, fee_usd: 0,   status: quoted_unverified, note: "fee 0 = treated as unknown_zero"}
  - {from: bybit,   to: binance, chain: KAIA,   fee_usd: 0.1, status: quoted_unverified}
  - {from: bybit,   to: binance, chain: ERC20,  fee_usd: 0.8, status: quoted_unverified}
progress_unit: "Basis: routes (9×8=72). Chain is a sub-axis under route — multiple chains on the same route do not increase progress"
```

Latest corridor status is read from `nw_kg_facts` `rail:<to>:<chain>:*` (one row per day). This YAML is a snapshot.

## Atoms
- [[../atoms/route-map/01-corridor-binance-bithumb-kaia]] — Corridor binance→bithumb KAIA — ok, 99s, 2026-08-08
- [[../atoms/route-map/02-corridor-binance-bithumb-trx]] — Corridor binance→bithumb TRX — not recommended (75x KAIA)
- [[../atoms/route-map/03-corridor-binance-bybit-bsc]] — Corridor binance→bybit BSC — ok, no 2FA, 81s, 2026-08-02
- [[../atoms/route-map/04-corridor-binance-bybit-sol]] — Corridor binance→bybit SOL — ok (30x more expensive than BSC), 2026-08-02
- [[../atoms/route-map/05-corridor-mexc-binance-bsc]] — Corridor mexc→binance BSC — ok (netWork code required), 80s, 2026-08-03
- [[../atoms/route-map/06-corridor-mexc-eoa]] — Corridor mexc→hub EOA ETH/ARB — ok, 70s, 2026-08-08
- [[../atoms/route-map/07-corridor-eoa-gate]] — Corridor hub EOA→gate — on-chain gas $0.0024, ok, 2026-08-08
- [[../atoms/route-map/08-corridor-gate-eoa]] — Corridor gate→hub EOA — 0.025, 1/20 of direct CEX withdrawal fee 0.5, ok
- [[../atoms/route-map/09-corridor-kucoin-gate-bep20]] — Corridor kucoin→gate BEP20 — 30 deducted, 151s, ok (EGL1 recovery), 2026-08-30
- [[../atoms/route-map/10-corridor-bybit-bithumb-trx]] — Corridor bybit→bithumb TRX — needs_address_registration, funds did not move, 2026-08-02
- [[../atoms/route-map/11-corridor-bithumb-binance]] — Corridor bithumb→binance — flat 1% added on top, ok (SAPIEN 3600→3565), 2026-08-30
- [[../atoms/route-map/12-onchain-cost-principle]] — On-chain leg cost = 1/200–1/400 of exchange withdrawal fees
- [[../atoms/route-map/13-bottleneck-bithumb-usdt-chains]] — Bithumb USDT-accepting chains confirmed (08-08) — more observation, not more chains opening
- [[../atoms/route-map/14-bottleneck-kaia-lowest]] — KAIA is the lowest cost route to Korea (0.02 vs TRX 1.5)
- [[../atoms/route-map/15-bottleneck-bithumb-fee-ghost]] — Bithumb's added-on-top withdrawal fee is why settlement showed a phantom remainder
- [[../atoms/route-map/16-bottleneck-bithumb-address-book]] — Bithumb address book = pre-registration per (address+asset), verifiable only in the UI
- [[../atoms/route-map/17-bottleneck-upbit-whitelist]] — Upbit whitelist, 320 pairs — the bottleneck is our list of sell destinations
- [[../atoms/route-map/18-bottleneck-bithumb-leg-cases]] — Bithumb leg is the bottleneck in many cases (XCN $5k, bithumb 8.29pp)
- [[../atoms/route-map/19-travel-rule-free-10]] — Travel Rule free transfer, 10 venues (HTX·Toobit code update pending)
- [[../atoms/route-map/20-travel-rule-impossible]] — Travel Rule blocked — mexc·gate (mid tier)·kucoin
- [[../atoms/route-map/21-travel-rule-gate-midtier]] — Gate mid tier — after pre-registration, <₩1M per transaction, occasional only, no standing bot
- [[../atoms/route-map/22-travel-rule-blocked41]] — Unregistered (blocked), confirmed 41 venues — no re-investigation
- [[../atoms/route-map/23-travel-rule-workaround]] — Workaround pending — mexc→OKX→bithumb (once OKX adapter is complete)
- [[../atoms/route-map/24-yaml-corridor-bybit-binance-plasma]] — Corridor (YAML) bybit→binance PLASMA fee $0 — quoted_unverified
- [[../atoms/route-map/25-yaml-corridor-bybit-binance-kaia]] — Corridor (YAML) bybit→binance KAIA fee $0.1 — quoted_unverified
- [[../atoms/route-map/26-yaml-corridor-bybit-binance-erc20]] — Corridor (YAML) bybit→binance ERC20 fee $0.8 — quoted_unverified
- [[../atoms/route-map/27-progress-unit]] — Progress unit = basis of routes (9×8=72), chain is a sub-axis
</content>
