---
id: hyperliquid.atom.xyz-skhx-market.10
lang: en
title: execution cost comparison — 4 methods (single-shot taker / split taker / maker / internalization)
status: verified
as_of: 2026-07-31
hub: "[[../../facts/xyz-skhx-market]]"
source: "execution simulation + internalization review"
tags: [xyz, SKHX, execution]
contributors: [house]
---

# execution cost comparison — 4 methods (single-shot taker / split taker / maker / internalization)

The cost by execution method is as follows: 500 in one taker shot = −7.5bp (0.9 fee + 6.6 slippage, ≈600k KRW, risk 0); split into 1-hour taker slices = about −1bp (our volume is 0.9% of hourly volume, risk 0); maker order submission = +0.4bp to −0.16bp (maker 0.16bp, unfilled risk); customer-flow internalization (1h netting) = 0 cost, but 800M KRW unhedged + B-book status + custody risk.

**Basis**: table "500 in one taker shot | −7.5bp (0.9 fee + 6.6 slippage) ≈ 600k KRW | 0 / Split into 1-hour taker slices | about −1bp (our volume = 0.9% of hourly volume) | 0 / Maker order submission | +0.4bp to −0.16bp (maker 0.16bp) | unfilled risk / Customer-flow internalization (1h netting) | 0 | 800M KRW unhedged + B-book status + custody"

Related: [[../../gates/execution-size-split]]
