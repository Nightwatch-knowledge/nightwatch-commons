---
id: rails.facts.measured-costs
lang: en
title: Measured Cost Table — Fees, Latency, Chain Gaps
status: verified
as_of: 2026-09-06
sources: [QM_RAIL_LOG.md, project_transfer_intelligence, project_qm_rail_kg, feedback_fee_discipline_rails, ops_gpilot_egl1_stuck]
contributors: [house]
tags: [fee, transit, chain, cost]
tier_candidate: commons
---

# Measured Cost Table

## Chain gaps — the same route can differ by 8~75x
| Route | Fee by chain | Gap |
|---|---|---|
| binance → bithumb | KAIA 0.02 / TRX 1.5 | **75x** |
| binance → bybit | BSC 0.01 / SOL 0.30 | 30x (BSC is also faster) |
| bybit → binance | PLASMA $0 / KAIA $0.1 / ERC20 $0.8 | 8x (quoted; 0 is unknown_zero) |
| gate withdrawal | via hub EOA 0.025 / direct to CEX 0.5 | 20x |

Principle (Robin 2026-08-14): **"Fee reduction is the single most important job in arbitrage."** With a cycle margin of 0.25~2%, a 0.1%p transfer cost swings tens of percent of net profit. A cheap chain is not an "option" — it's the **default** → [[../gates/lowest-fee-chain-default]]

## Latency (submit → arrival confirmed)
| Route/chain | Latency |
|---|---|
| binance→bybit BSC | 81s |
| mexc→binance BSC | 80s |
| binance→bithumb KAIA | 99s |
| binance→bybit SOL | 141s |
| kucoin→gate BEP20 | 151s |
| mexc→EOA ETH/ARB | 70s |
| Base→HyperEVM CCTP v2 (Standard) | 13~19min (ref: Hyperliquid Playbook) |

**Slow chains (p90 > 15min) or 2+ hops = hedge required** (Robin 2026-09-02) → [[../gates/slow-chain-hedge-required]]. 42-cycle diagnosis: slow chains were the cause of losses.

## Quoted vs. actual deduction (`fee_match`)
- **binance's quoted withdrawal fee is honest** (2/2 match)
- **bithumb**: `withdraw_fee=0` but `withdraw_rate=1%` — trusting the 0 is wrong → `unknown_zero` principle
- **kucoin BEP20**: deducted from the 30 EGL1 request amount (measured 08-30)
- **STRK withdrawal fee $35.9** — a chain being viable ≠ economical. If the fee eats the cycle margin, that chain effectively doesn't exist

## Atoms
- [[../atoms/measured-costs/01-chain-gap-binance-bithumb]] — binance→bithumb chain gap — KAIA 0.02 vs TRX 1.5, 75x
- [[../atoms/measured-costs/02-chain-gap-binance-bybit]] — binance→bybit chain gap — BSC 0.01 vs SOL 0.30, 30x
- [[../atoms/measured-costs/03-chain-gap-bybit-binance]] — bybit→binance chain gap — PLASMA $0·KAIA $0.1·ERC20 $0.8, 8x
- [[../atoms/measured-costs/04-chain-gap-gate-withdraw]] — gate withdrawal — via hub 0.025 vs direct-to-CEX 0.5, 20x
- [[../atoms/measured-costs/05-principle-lowest-fee-default]] — principle — a cheap chain is not an option, it's the default
- [[../atoms/measured-costs/06-transit-binance-bybit-bsc]] — binance→bybit BSC latency 81s
- [[../atoms/measured-costs/07-transit-mexc-binance-bsc]] — mexc→binance BSC latency 80s
- [[../atoms/measured-costs/08-transit-binance-bithumb-kaia]] — binance→bithumb KAIA latency 99s
- [[../atoms/measured-costs/09-transit-binance-bybit-sol]] — binance→bybit SOL latency 141s
- [[../atoms/measured-costs/10-transit-kucoin-gate-bep20]] — kucoin→gate BEP20 latency 151s
- [[../atoms/measured-costs/11-transit-mexc-eoa-eth-arb]] — mexc→hub EOA ETH/ARB latency 70s
- [[../atoms/measured-costs/12-transit-base-hyperevm-cctp]] — Base→HyperEVM CCTP v2 latency 13~19min
- [[../atoms/measured-costs/13-principle-slow-chain-hedge]] — slow chains (p90>15min) or 2+ hops require a hedge
- [[../atoms/measured-costs/14-fee-disclosure-binance-honest]] — binance's quoted withdrawal fee is honest (2/2 match)
- [[../atoms/measured-costs/15-fee-disclosure-bithumb-unknown-zero]] — bithumb withdraw_fee=0 but actual rate is 1% — unknown_zero
- [[../atoms/measured-costs/16-fee-disclosure-kucoin-bep20]] — kucoin BEP20 — 30 EGL1 deducted from the request amount (measured 08-30)
- [[../atoms/measured-costs/17-fee-disclosure-strk]] — STRK withdrawal fee $35.9 — chain viability ≠ economics
