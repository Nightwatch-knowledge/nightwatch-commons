---
id: hyperliquid.atom.api-access.11
title: 자산 ID 체계 — perp/spot/outcome 세 네임스페이스
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "실측 (자산 ID 매핑)"
tags: [api]
contributors: [house]
---

# 자산 ID 체계 — perp/spot/outcome 세 네임스페이스

자산 ID는 세 네임스페이스로 나뉜다: perp `100000 + dex*10000 + i`(xyz=dex 1 → 110000+i), spot `10000+i`, outcome `100_000_000+encoding`.

**근거**: "자산 ID | perp 100000 + dex*10000 + i (xyz=dex 1 → 110000+i) · spot 10000+i · outcome 100_000_000+encoding"

관련: [[../corewriter-vaults/04-asset-id-mapping-rule]] · [[../hip4-outcome-markets/02-belongs-to-spot-ledger]]
