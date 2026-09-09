---
id: hyperliquid.atom.xyz-skhx-market.10
title: 집행 비용 비교 — 4방식(한방taker/분할taker/메이커/내재화)
status: verified
as_of: 2026-07-31
hub: "[[../../facts/xyz-skhx-market]]"
source: "체결 시뮬레이션 + 내재화 검토"
tags: [xyz, SKHX, execution]
contributors: [house]
---

# 집행 비용 비교 — 4방식(한방taker/분할taker/메이커/내재화)

집행 방식별 비용은 다음과 같다: 500 한 방에 taker = −7.5bp(0.9 수수료 + 6.6 슬리피지, ≈60만원, 리스크 0), 1시간 분할 taker = 약 −1bp(우리 물량이 시간당 거래량의 0.9%, 리스크 0), 메이커 호가 제출 = +0.4bp~−0.16bp(maker 0.16bp, 미체결 리스크), 고객흐름 내재화(1h 상계) = 0 비용이나 8억 무헤지+B-book 지위+커스터디 리스크.

**근거**: 표 "500 한 방에 taker | −7.5bp (0.9 수수료 + 6.6 슬리피지) ≈ 60만원 | 0 / 1시간 분할 taker | 약 −1bp (우리 물량 = 시간당 거래량의 0.9%) | 0 / 메이커 호가 제출 | +0.4bp ~ −0.16bp (maker 0.16bp) | 미체결 / 고객흐름 내재화(1h 상계) | 0 | 8억 무헤지 + B-book 지위 + 커스터디"

관련: [[../../gates/execution-size-split]]
