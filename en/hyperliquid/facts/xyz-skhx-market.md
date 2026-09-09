---
id: hl.facts.xyz-skhx-market
lang: en
title: xyz:SKHX Market Measurements — 1:1 with the underlying share, 0.87bp spread, execution cost comparison
status: verified
as_of: 2026-07-31
freshness_note: "Price/volume data staled on a daily basis. Structure (1:1 with the underlying share, leverage, asset ID) is stable. For the latest price, MCP get_kg_facts('sk-hynix').live"
sources: ["l2Book xyz:SKHX measured", "meta dex:xyz", "execution simulation"]
contributors: [house]
tags: [xyz, SKHX, market-structure, execution, slippage]
tier_candidate: commons
---

# xyz:SKHX Market Measurements (2026-07-31)

| | Value |
|---|---|
| mark | **$1,153.1** (matches SK Hynix's 1.6M KRW @ ~1,385 KRW/$ → **confirms 1:1 with the underlying share**) |
| spread | best bid 1,154.50 / ask 1,154.60 = **$0.10 = 0.87bp** (half-spread 0.43bp) |
| orderbook depth | top-of-book $43,119 · 4 ticks $120k · 8 ticks $299k |
| 24h volume | **$1.535B** (= $64M/hour) |
| OI | 391,131 SKHX ≈ $451M |
| funding | +0.0000002/h (effectively zero) |
| maxLeverage | 10 |
| asset ID | 110022 (`110000 + i`, xyz = perpDexs index 1) |

**500 SKHX market-order execution simulation** (= $576,550 ≈ 800M KRW)
```
BUY  500 → VWAP 1,155.32  = 6.63bp slippage
SELL 500 → VWAP 1,153.75  = 6.94bp slippage
```

⚠️ **`xyz:SKHY` ($156.04, 24h $419M, OI 1,027,858) is a separate instrument, 7.39x different from SKHX.** Identity unverified — do not lump it together as "SK Hynix" in code. → [[../gates/symbol-identity-skhx-vs-skhy]]

## Execution cost comparison (internalization review conclusion)

| Method | Cost | Risk |
|---|---|---|
| 500 in one taker shot | **−7.5bp** (0.9 fee + 6.6 slippage) ≈ 600k KRW | 0 |
| Split into 1-hour taker slices | about **−1bp** (our volume = 0.9% of hourly volume) | 0 |
| **Maker order submission** | **+0.4bp to −0.16bp** (maker 0.16bp) | unfilled risk |
| Customer-flow internalization (1h netting) | 0 | **800M KRW unhedged + B-book status + custody** |

**Conclusion**: The 6.6bp slippage arises not from "customers not matching each other" but from **"dumping it all at once."** Most of the cost disappears through **execution method**, not internalization. With the spread already tight at 0.87bp, the internalization prize is small anyway. → [[../gates/execution-size-split]]

## Netting is two kinds, and only one of them is ours
| | What | Verdict |
|---|---|---|
| **Account level** (cross/unified/portfolio margin) | Our account's positions share collateral | ✅ Real, free, riskless → [[account-modes]] |
| **Customer-flow level** (internalization) | We become the counterparty by matching customer A's buy against customer B's sell | ❌ B-book. Gains 0.9bp but takes on broker status |

## Related measurements (other documents)
- xyz is **4x cheaper** than the main venue (based on execution records, not the fee schedule, `TORII_TERMINAL.md`)
- Builder code HIP-3 confirmed operating across 952 fills, competitive rates 1.2–5.0bp
- Korean-underlying instruments total $1.42B/day = 25.9% of xyz's volume (2026-07-28)

## Atoms
- [[../atoms/xyz-skhx-market/01-mark-price-1153-confirms-1to1]] — mark price $1,153.1 — confirms 1:1 with the SK Hynix underlying share
- [[../atoms/xyz-skhx-market/02-spread-0-87bp]] — spread $0.10 = 0.87bp
- [[../atoms/xyz-skhx-market/03-orderbook-depth]] — orderbook depth — top-of-book $43,119 · 4 ticks $120k · 8 ticks $299k
- [[../atoms/xyz-skhx-market/04-24h-volume-1-535b]] — 24h volume $1.535B ($64M/hour)
- [[../atoms/xyz-skhx-market/05-oi-391131-skhx]] — OI 391,131 SKHX ≈ $451M
- [[../atoms/xyz-skhx-market/06-funding-near-zero]] — funding +0.0000002/h — effectively zero
- [[../atoms/xyz-skhx-market/07-max-leverage-10-asset-id-110022]] — maxLeverage 10, asset ID 110022
- [[../atoms/xyz-skhx-market/08-500skhx-simulation-slippage]] — 500 SKHX market-order execution simulation — 6.63bp slippage on buy / 6.94bp on sell
- [[../atoms/xyz-skhx-market/09-skhy-different-asset-warning]] — warning — xyz:SKHY is a separate instrument 7.39x different from SKHX, identity unverified
- [[../atoms/xyz-skhx-market/10-execution-cost-comparison-table]] — execution cost comparison — 4 methods (single-shot taker / split taker / maker / internalization)
- [[../atoms/xyz-skhx-market/11-conclusion-execution-method-not-internalization]] — conclusion — the cause of the 6.6bp slippage is "dumping it all at once," not the absence of internalization
- [[../atoms/xyz-skhx-market/12-netting-two-kinds-only-one-is-ours]] — netting is two kinds, and only the account level is ours
- [[../atoms/xyz-skhx-market/13-related-observations-torii-terminal]] — related measurements — xyz is 4x cheaper than the main venue, builder code HIP-3 952 fills · competitive rates 1.2–5.0bp, Korean-underlying instruments 25.9%
