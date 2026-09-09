---
id: hyperliquid.atom.usdc-deposit-rails.05
lang: en
title: The real structure behind unification — multiple chains flow through a bridge layer to Arbitrum, and we already have the LI.FI widget
status: verified
as_of: 2026-07-31
hub: "[[../../rails/usdc-deposit-rails]]"
source: "Synthesis of onboarding docs"
tags: [deposit, Bridge2]
contributors: [house]
---

# The real structure behind unification — multiple chains flow through a bridge layer to Arbitrum, and we already have the LI.FI widget

The actual structure is that Base/Polygon/Ethereum USDC flows through a bridge layer and converges into Arbitrum USDC, which enters HyperCore only via Bridge2 (Arbitrum USDC is the sole protocol entry point). We already have the means to unify the front end — the `/torii/fund` LI.FI widget is live (`FUND_RAIL_TIERS` T3), and our fee is 0.

**Basis**: "Base USDC/Polygon USDC/Ethereum → [bridge layer] → Arbitrum USDC → Bridge2 → HyperCore ↑ sole protocol entry point" / "What can be unified is the front end, and we already have it — the /torii/fund LI.FI widget is live (FUND_RAIL_TIERS T3), our fee is 0."

Related: (none)
