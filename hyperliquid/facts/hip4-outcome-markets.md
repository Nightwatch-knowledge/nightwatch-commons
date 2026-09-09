---
id: hl.facts.hip4-outcome-markets
title: HIP-4 Outcome markets (예측시장) — 라이브, spot 원장 소속
status: verified
as_of: 2026-07-31
sources: ["HIP-4 문서", "spotClearinghouseState 실측", "l2Book #9610 실측"]
contributors: [house]
tags: [HIP-4, outcome, prediction-market, portfolio-margin]
tier_candidate: commons
---

# HIP-4 Outcome markets

> "**HIP-4 is a general-purpose primitive that is useful for applications such as prediction markets** and bounded options-like instruments."
> "Outcomes bring non-linearity, dated contracts ... **does not involve leverage or liquidations**."

**소속 = perp이 아니라 spot 원장.** 자산 ID `100_000_000 + encoding` (perp `100000+dex*10000+i`, spot `10000+i`와 별도 네임스페이스). 실측: 거래자의 `spotClearinghouseState`에 `{"coin":"+9610","total":"89391.0"}`가 USDC와 같은 balances 배열 안에 존재.

| outcome | description | quote |
|---|---|---|
| 961 | `priceBinary\|BTC\|expiry:20260731-0600\|targetPrice:64009\|period:1d` | USDC |
| 962 / 963 / 964 | ETH(1905.4) / SOL(73.672) / HYPE(53.777) | USDC |
| question 160 | `priceBucket\|BTC\|priceThresholds:62728,65289` | USDC |

호가창 가동 확인(`l2Book "#9610"` → bid 0.94203 / ask 0.956, 양쪽 20레벨), 실체결 존재.
**수수료 현재 0** ("Fees are currently zero for outcome markets for initial testing").
> "composing with other primitives such as **portfolio margin** and the HyperEVM."
→ **portfolio margin 아래서 perp·spot·예측이 한 담보 풀에 들어온다.**

CoreWriter action 17 = Outcome operation (Split/Merge/Negate) → [[corewriter-action-table]]

## 플레이북 간 연결
예측시장 = "정산되는 현실"의 교과서 사례. Polymarket 플레이북과 구조 비교 대상 (HIP-4는 담보 풀 통합이 강점, 해결 소스는 HL 오라클).

## Atoms
- [[../atoms/hip4-outcome-markets/01-hip4-general-purpose-primitive]] — HIP-4는 예측시장용 범용 프리미티브이며 레버리지·청산이 없다
- [[../atoms/hip4-outcome-markets/02-belongs-to-spot-ledger]] — HIP-4의 소속은 perp이 아니라 spot 원장이다
- [[../atoms/hip4-outcome-markets/03-outcome-market-list]] — 실측된 outcome 시장 목록 — BTC/ETH/SOL/HYPE 바이너리, BTC 버킷
- [[../atoms/hip4-outcome-markets/04-orderbook-live-l2book-9610]] — 호가창 가동 확인 — l2Book #9610 bid/ask 20레벨
- [[../atoms/hip4-outcome-markets/05-fees-currently-zero]] — outcome 시장 수수료는 현재 0
- [[../atoms/hip4-outcome-markets/06-composes-with-portfolio-margin]] — portfolio margin과 결합하면 perp·spot·예측이 한 담보 풀에 들어온다
- [[../atoms/hip4-outcome-markets/07-corewriter-action17]] — CoreWriter action 17 = Outcome operation
- [[../atoms/hip4-outcome-markets/08-cross-playbook-prediction-market-comparison]] — 예측시장은 "정산되는 현실"의 교과서 사례 — Polymarket과 구조 비교 대상
