---
id: hyperliquid.atom.api-access.11
lang: en
title: Asset ID scheme — three namespaces for perp/spot/outcome
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "measured (asset ID mapping)"
tags: [api]
contributors: [house]
---

# Asset ID scheme — three namespaces for perp/spot/outcome

Asset IDs are divided into three namespaces: perp `100000 + dex*10000 + i` (xyz=dex 1 → 110000+i), spot `10000+i`, outcome `100_000_000+encoding`.

**Basis**: "Asset ID | perp 100000 + dex*10000 + i (xyz=dex 1 → 110000+i) · spot 10000+i · outcome 100_000_000+encoding"

Related: [[../corewriter-vaults/04-asset-id-mapping-rule]] · [[../hip4-outcome-markets/02-belongs-to-spot-ledger]]
