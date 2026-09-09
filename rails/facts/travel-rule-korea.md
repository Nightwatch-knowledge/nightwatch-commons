---
id: rails.facts.travel-rule-korea
title: 트래블룰과 한국 거래소 연결 지도
status: verified
as_of: 2026-09-06
sources: [BITHUMB_COUNTERPARTY_MAP.md, research/2026-08-05-bithumb-counterparty/, feedback_fee_discipline_rails]
contributors: [house]
tags: [travel-rule, bithumb, upbit, korea, whitelist]
tier_candidate: commons
---

# 트래블룰 — 한국 leg의 규칙

## 빗썸 연결 등급
| 등급 | 거래소 | 조건 |
|---|---|---|
| 자유송금 (트래블룰 연동) | bitget · bybit · okx · binance · **HTX · Toobit** (+atlas 8/1 명단) = **10곳** | 거래소 단위 1회 등록 |
| **중간 티어** | **Gate** | CODE 연동(2024-03)됐으나 빗썸 미활성 → 주소 사전등록 7영업일 후 **건당 <₩1M**. 반복출금 감시 조항 → **봇 상시 파이프 금지** |
| 불가 | mexc · kucoin | 우회 필요 (mexc→OKX→빗썸 대기) |
| **미신고 차단 41곳** | BingX(2026-01-12 추가) · BitMart · WEEX · Blofin · CoinW … | 등록 불가, **재조사 금지** |

업비트는 Gate 계정주확인 연동으로 더 명확.

## 빗썸 체인
- USDT 수용: **ETH · TRX · KAIA · APT** (2026-08-08). 출금은 TRX·ETH만 (08-02 관측)
- 한국행 최저 = **KAIA 0.02** (TRX 1.5)
- 출금비: 정률 1% 254종 / 정액 14종 / BTT-TRX·TT = 0. **⚠️ 1% 가정이 허브 스크리닝을 지배 — 39종 실측(Robin 액션)에서 낮은 종목이 나오면 DROP 판정이 뒤집힌다**

## 업비트 (2026-09-06)
- 화이트리스트 **320쌍**. ETH 체인 259쌍은 정책 `rule:chain_policy_mode=fee_known_and_hedged`(수수료 실측 확정 + 진입 문턱 포함 + 헷지 확실)로 열림. `rule:chain_fee_max_usd` 기본 3
- 하드코딩 `FORBIDDEN_CHAINS` 폐지 → KG 정책으로 대체
- 업비트→gate 등록쌍 14 (ARB·TRX 체인, usdt/trx 포함). 업비트 쪽 문제 없음 — **병목은 우리 매도처 목록(gateio 미허용)** → 개방 진행

## 평가 단위 = (거래소 × 종목) 쌍 (Robin 정정, 2026-08-05)
거래소 단위 채택/탈락 폐기. **A**=비교군+집행 / **B**=비교군·집행금지(가격 신호 전용) / **C**=관찰 / **X**=제외. 편입 절차 = 데이터 인제스트 (pair_gate가 `unknown_support`→자동 차단이므로 **데이터가 곧 심사**). 거래소 레일 티어는 쌍 등급의 한 필드. → [[counterparty-grades]]

## 사실 확인 함정
빗썸 공식 페이지는 봇 403 → jina.ai 프록시로 읽는다.

## Atoms
- [[../atoms/travel-rule-korea/01-bithumb-connection-free]] — 빗썸 자유송금 10곳 — 거래소 단위 1회 등록
- [[../atoms/travel-rule-korea/02-bithumb-connection-midtier]] — 빗썸 중간 티어 Gate — 사전등록 후 건당 <₩1M, 봇상시금지
- [[../atoms/travel-rule-korea/03-bithumb-connection-impossible]] — 빗썸 불가 — mexc·kucoin은 우회 필요
- [[../atoms/travel-rule-korea/04-bithumb-connection-blocked41]] — 미신고 차단 41곳 — 등록 불가, 재조사 금지
- [[../atoms/travel-rule-korea/05-upbit-gate-clearer]] — 업비트는 Gate 계정주확인 연동으로 더 명확
- [[../atoms/travel-rule-korea/06-bithumb-usdt-chains]] — 빗썸 USDT 수용체인 ETH·TRX·KAIA·APT, 출금은 TRX·ETH만
- [[../atoms/travel-rule-korea/07-bithumb-lowest-fee-chain]] — 한국행 최저 체인 = KAIA 0.02 (TRX 1.5)
- [[../atoms/travel-rule-korea/08-bithumb-withdraw-fee-structure]] — 빗썸 출금비 — 정률1% 254종·정액14종·0(BTT-TRX·TT), 39종 실측 대기
- [[../atoms/travel-rule-korea/09-upbit-whitelist]] — 업비트 화이트리스트 320쌍, ETH체인 259쌍은 정책으로 열림
- [[../atoms/travel-rule-korea/10-upbit-hardcode-deprecated]] — 하드코딩 FORBIDDEN_CHAINS 폐지 → KG 정책으로 대체
- [[../atoms/travel-rule-korea/11-upbit-gate-pairs]] — 업비트→gate 등록쌍 14, 병목은 매도처 목록
- [[../atoms/travel-rule-korea/12-pair-grade-unit]] — 평가 단위 = (거래소×종목) 쌍 — A/B/C/X 등급
- [[../atoms/travel-rule-korea/13-bithumb-fact-check-trap]] — 빗썸 공식 페이지는 봇 403 — jina.ai 프록시로 읽는다
