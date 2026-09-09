---
id: rails.atom.travel-rule-korea.12
title: 평가 단위 = (거래소×종목) 쌍 — A/B/C/X 등급
status: verified
as_of: 2026-08-05
hub: "[[../../facts/travel-rule-korea]]"
source: "BITHUMB_COUNTERPARTY_MAP.md"
tags: [travel-rule, korea]
contributors: [house]
---

# 평가 단위 = (거래소×종목) 쌍 — A/B/C/X 등급

평가 단위는 거래소 단위가 아니라 (거래소×종목) 쌍이다(Robin 정정, 2026-08-05). A=비교군+집행 / B=비교군·집행금지(가격 신호 전용) / C=관찰 / X=제외. 편입 절차는 데이터 인제스트이며, pair_gate가 unknown_support면 자동 차단하므로 데이터가 곧 심사다.

**근거**: "평가 단위 = (거래소 × 종목) 쌍 (Robin 정정, 2026-08-05) 거래소 단위 채택/탈락 폐기. A=비교군+집행 / B=비교군·집행금지(가격 신호 전용) / C=관찰 / X=제외. 편입 절차 = 데이터 인제스트 (pair_gate가 unknown_support→자동 차단이므로 데이터가 곧 심사)"

관련: [[../../facts/counterparty-grades]] · [[../../gates/travel-rule-check]]
