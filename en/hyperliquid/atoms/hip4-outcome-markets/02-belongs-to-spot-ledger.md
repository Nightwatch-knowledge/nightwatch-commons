---
id: hyperliquid.atom.hip4-outcome-markets.02
lang: en
title: HIP-4 belongs to the spot ledger, not perp
status: verified
as_of: 2026-07-31
hub: "[[../../facts/hip4-outcome-markets]]"
source: "spotClearinghouseState measured"
tags: [HIP-4, outcome]
contributors: [house]
---

# HIP-4 belongs to the spot ledger, not perp

Outcome markets belong to the spot ledger, not perp. The asset ID is `100_000_000 + encoding`, a separate namespace from perp's `100000+dex*10000+i` and spot's `10000+i`. Measurement confirmed that a trader's `spotClearinghouseState` contains `{"coin":"+9610","total":"89391.0"}` inside the same balances array as USDC.

**Basis**: "Belongs to the spot ledger, not perp. Asset ID 100_000_000 + encoding (a separate namespace from perp's 100000+dex*10000+i and spot's 10000+i). Measured: a trader's spotClearinghouseState contains {"coin":"+9610","total":"89391.0"} inside the same balances array as USDC."

Related: (none)
