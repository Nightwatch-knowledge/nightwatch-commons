---
id: hyperliquid.atom.usdc-deposit-rails.05
title: 통일성의 실제 구조 — 여러 체인이 브리지 레이어를 거쳐 Arbitrum으로, 우리는 이미 LI.FI 위젯 보유
status: verified
as_of: 2026-07-31
hub: "[[../../rails/usdc-deposit-rails]]"
source: "온보딩 문서 종합"
tags: [deposit, Bridge2]
contributors: [house]
---

# 통일성의 실제 구조 — 여러 체인이 브리지 레이어를 거쳐 Arbitrum으로, 우리는 이미 LI.FI 위젯 보유

실제 구조는 Base/Polygon/Ethereum USDC가 브리지 레이어를 거쳐 Arbitrum USDC로 모이고, Bridge2를 통해서만 HyperCore에 진입하는 형태다(Arbitrum USDC가 유일한 프로토콜 진입점). 앞단을 통일하는 수단은 우리가 이미 갖고 있다 — `/torii/fund` LI.FI 위젯이 라이브 상태이며(`FUND_RAIL_TIERS` T3), 우리 수수료는 0이다.

**근거**: "Base USDC/Polygon USDC/Ethereum → [브리지 레이어] → Arbitrum USDC → Bridge2 → HyperCore ↑ 유일한 프로토콜 진입점" / "통일 가능한 것은 앞단이고 우리는 이미 갖고 있다 — /torii/fund LI.FI 위젯 라이브(FUND_RAIL_TIERS T3, 우리 수수료 0)."

관련: (해당 없음)
