---
id: hl.facts.hip4-outcome-markets
lang: en
title: HIP-4 Outcome markets (prediction markets) — live, belongs to the spot ledger
status: verified
as_of: 2026-07-31
sources: ["HIP-4 documentation", "spotClearinghouseState measured", "l2Book #9610 measured"]
contributors: [house]
tags: [HIP-4, outcome, prediction-market, portfolio-margin]
tier_candidate: commons
---

# HIP-4 Outcome markets

> "**HIP-4 is a general-purpose primitive that is useful for applications such as prediction markets** and bounded options-like instruments."
> "Outcomes bring non-linearity, dated contracts ... **does not involve leverage or liquidations**."

**Belongs to the spot ledger, not perp.** Asset ID `100_000_000 + encoding` (a separate namespace from perp's `100000+dex*10000+i` and spot's `10000+i`). Measured: a trader's `spotClearinghouseState` contains `{"coin":"+9610","total":"89391.0"}` inside the same balances array as USDC.

| outcome | description | quote |
|---|---|---|
| 961 | `priceBinary\|BTC\|expiry:20260731-0600\|targetPrice:64009\|period:1d` | USDC |
| 962 / 963 / 964 | ETH(1905.4) / SOL(73.672) / HYPE(53.777) | USDC |
| question 160 | `priceBucket\|BTC\|priceThresholds:62728,65289` | USDC |

Orderbook activity confirmed (`l2Book "#9610"` → bid 0.94203 / ask 0.956, 20 levels on each side), actual fills exist.
**Fees are currently zero** ("Fees are currently zero for outcome markets for initial testing").
> "composing with other primitives such as **portfolio margin** and the HyperEVM."
→ **Under portfolio margin, perp, spot, and prediction markets share a single collateral pool.**

CoreWriter action 17 = Outcome operation (Split/Merge/Negate) → [[corewriter-action-table]]

## Cross-playbook connections
Prediction markets are the textbook case of "settling reality." A structural comparison target against the Polymarket playbook (HIP-4's strength is collateral pool integration; its resolution source is the HL oracle).

## Atoms
- [[../atoms/hip4-outcome-markets/01-hip4-general-purpose-primitive]] — HIP-4 is a general-purpose primitive for prediction markets, with no leverage or liquidations
- [[../atoms/hip4-outcome-markets/02-belongs-to-spot-ledger]] — HIP-4 belongs to the spot ledger, not perp
- [[../atoms/hip4-outcome-markets/03-outcome-market-list]] — Measured list of outcome markets — BTC/ETH/SOL/HYPE binaries, BTC bucket
- [[../atoms/hip4-outcome-markets/04-orderbook-live-l2book-9610]] — Orderbook activity confirmed — l2Book #9610 bid/ask 20 levels
- [[../atoms/hip4-outcome-markets/05-fees-currently-zero]] — Outcome market fees are currently zero
- [[../atoms/hip4-outcome-markets/06-composes-with-portfolio-margin]] — Combined with portfolio margin, perp, spot, and prediction markets share a single collateral pool
- [[../atoms/hip4-outcome-markets/07-corewriter-action17]] — CoreWriter action 17 = Outcome operation
- [[../atoms/hip4-outcome-markets/08-cross-playbook-prediction-market-comparison]] — Prediction markets are the textbook case of "settling reality" — a structural comparison target against Polymarket
