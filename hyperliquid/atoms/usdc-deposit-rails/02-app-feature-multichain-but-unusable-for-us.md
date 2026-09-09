---
id: hyperliquid.atom.usdc-deposit-rails.02
title: 앱 기능은 Base/Polygon/Ethereum도 받지만 우리는 쓸 수 없다
status: verified
as_of: 2026-08-17
hub: "[[../../rails/usdc-deposit-rails]]"
source: "온보딩 문서"
tags: [deposit]
contributors: [house]
---

# 앱 기능은 Base/Polygon/Ethereum도 받지만 우리는 쓸 수 없다

이메일 로그인 온보딩 항목에만 기술된 앱 기능은 Arbitrum/Ethereum/Base/Polygon의 USDC를 표시된 입금 주소로 보내면 HyperCore에 USDC로 도착한다고 안내한다. 이는 HL 앱 프론트엔드가 붙인 입금 라우팅 서비스로, 운영 주체·API 유무는 `unverified`다. 유저를 app.hyperliquid.xyz로 보내지 않고 컨트랙트는 더더욱 쓸 수 없으므로 우리는 이 경로를 쓸 수 없다.

**근거**: "You can send USDC on Arbitrum/Ethereum/Base/Polygon to the deposit address shown ... Your deposit arrives as USDC on HyperCore." → "우리는 쓸 수 없다: 유저를 app.hyperliquid.xyz로 안 보내고, 컨트랙트는 더더욱 못 쓴다."

관련: (해당 없음)
