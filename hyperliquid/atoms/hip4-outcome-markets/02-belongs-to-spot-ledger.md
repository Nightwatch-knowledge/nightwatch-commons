---
id: hyperliquid.atom.hip4-outcome-markets.02
title: HIP-4의 소속은 perp이 아니라 spot 원장이다
status: verified
as_of: 2026-07-31
hub: "[[../../facts/hip4-outcome-markets]]"
source: "spotClearinghouseState 실측"
tags: [HIP-4, outcome]
contributors: [house]
---

# HIP-4의 소속은 perp이 아니라 spot 원장이다

Outcome 시장은 perp이 아니라 spot 원장 소속이다. 자산 ID는 `100_000_000 + encoding`으로, perp의 `100000+dex*10000+i`, spot의 `10000+i`와 별도 네임스페이스를 쓴다. 실측으로 거래자의 `spotClearinghouseState`에 `{"coin":"+9610","total":"89391.0"}`가 USDC와 같은 balances 배열 안에 존재함을 확인했다.

**근거**: "소속 = perp이 아니라 spot 원장. 자산 ID 100_000_000 + encoding (perp 100000+dex*10000+i, spot 10000+i와 별도 네임스페이스). 실측: 거래자의 spotClearinghouseState에 {"coin":"+9610","total":"89391.0"}가 USDC와 같은 balances 배열 안에 존재."

관련: (해당 없음)
