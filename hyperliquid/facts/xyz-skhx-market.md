---
id: hl.facts.xyz-skhx-market
title: xyz:SKHX 시장 실측 — 원주 1:1, 스프레드 0.87bp, 집행 비용 비교
status: verified
as_of: 2026-07-31
freshness_note: "시세·거래량은 일 단위로 낡음. 구조(원주 1:1, 레버리지, 자산ID)는 안정. 최신 시세는 MCP get_kg_facts('sk-hynix').live"
sources: ["l2Book xyz:SKHX 실측", "meta dex:xyz", "체결 시뮬레이션"]
contributors: [house]
tags: [xyz, SKHX, market-structure, execution, slippage]
tier_candidate: commons
---

# xyz:SKHX 시장 실측 (2026-07-31)

| | 값 |
|---|---|
| mark | **$1,153.1** (= SK하이닉스 160만원 @ ~1,385원/$ 과 일치 → **원주 1:1 확정**) |
| 스프레드 | best bid 1,154.50 / ask 1,154.60 = **$0.10 = 0.87bp** (반값 0.43bp) |
| 호가 깊이 | 최우선 $43,119 · 4틱 $120k · 8틱 $299k |
| 24h 거래량 | **$1.535B** (= 시간당 $64M) |
| OI | 391,131 SKHX ≈ $451M |
| 펀딩 | +0.0000002/h (사실상 0) |
| maxLeverage | 10 |
| 자산 ID | 110022 (`110000 + i`, xyz = perpDexs 인덱스 1) |

**500 SKHX 시장가 체결 시뮬레이션** (= $576,550 ≈ 8억원)
```
BUY  500 → VWAP 1,155.32  = 6.63bp 슬리피지
SELL 500 → VWAP 1,153.75  = 6.94bp 슬리피지
```

⚠️ **`xyz:SKHY`($156.04, 24h $419M, OI 1,027,858)는 SKHX와 7.39배 차이나는 별개 물건.** 정체 미확인 — 코드에서 "SK하이닉스"로 뭉뚱그리지 말 것. → [[../gates/symbol-identity-skhx-vs-skhy]]

## 집행 비용 비교 (내재화 검토 결론)

| 방식 | 비용 | 리스크 |
|---|---|---|
| 500 한 방에 taker | **−7.5bp** (0.9 수수료 + 6.6 슬리피지) ≈ 60만원 | 0 |
| 1시간 분할 taker | 약 **−1bp** (우리 물량 = 시간당 거래량의 0.9%) | 0 |
| **메이커 호가 제출** | **+0.4bp ~ −0.16bp** (maker 0.16bp) | 미체결 |
| 고객흐름 내재화(1h 상계) | 0 | **8억 무헤지 + B-book 지위 + 커스터디** |

**결론**: 슬리피지 6.6bp는 "고객끼리 안 맞물려서"가 아니라 **"한 번에 던져서"** 생긴다. 비용의 대부분은 내재화가 아니라 **집행 방식**으로 사라진다. 스프레드가 0.87bp로 이미 타이트해 내재화 상금도 작다. → [[../gates/execution-size-split]]

## netting은 두 가지이며 하나만 우리 것이다
| | 무엇 | 판정 |
|---|---|---|
| **계정 레벨** (cross/unified/portfolio margin) | 우리 계정의 포지션들이 담보 공유 | ✅ 실재·공짜·무위험 → [[account-modes]] |
| **고객흐름 레벨** (내재화) | 고객 A매수 ↔ B매도를 우리가 맞물려 상대방이 됨 | ❌ B-book. 0.9bp 얻고 브로커 지위 |

## 관련 실측 (다른 문서)
- xyz는 메인보다 **4배 싸다** (요금표 아닌 체결기록 기준, `TORII_TERMINAL.md`)
- 빌더코드 HIP-3 작동 확인 952건, 경쟁요율 1.2~5.0bp
- 한국물 합계 $1.42B/일 = xyz 거래량의 25.9% (2026-07-28)

## Atoms
- [[../atoms/xyz-skhx-market/01-mark-price-1153-confirms-1to1]] — mark 가격 $1,153.1 — SK하이닉스 원주 1:1 확정
- [[../atoms/xyz-skhx-market/02-spread-0-87bp]] — 스프레드 $0.10 = 0.87bp
- [[../atoms/xyz-skhx-market/03-orderbook-depth]] — 호가 깊이 — 최우선 $43,119·4틱 $120k·8틱 $299k
- [[../atoms/xyz-skhx-market/04-24h-volume-1-535b]] — 24h 거래량 $1.535B (시간당 $64M)
- [[../atoms/xyz-skhx-market/05-oi-391131-skhx]] — OI 391,131 SKHX ≈ $451M
- [[../atoms/xyz-skhx-market/06-funding-near-zero]] — 펀딩 +0.0000002/h — 사실상 0
- [[../atoms/xyz-skhx-market/07-max-leverage-10-asset-id-110022]] — maxLeverage 10, 자산 ID 110022
- [[../atoms/xyz-skhx-market/08-500skhx-simulation-slippage]] — 500 SKHX 시장가 체결 시뮬레이션 — 매수 6.63bp/매도 6.94bp 슬리피지
- [[../atoms/xyz-skhx-market/09-skhy-different-asset-warning]] — 경고 — xyz:SKHY는 SKHX와 7.39배 차이나는 별개 물건, 정체 미확인
- [[../atoms/xyz-skhx-market/10-execution-cost-comparison-table]] — 집행 비용 비교 — 4방식(한방taker/분할taker/메이커/내재화)
- [[../atoms/xyz-skhx-market/11-conclusion-execution-method-not-internalization]] — 결론 — 슬리피지 6.6bp의 원인은 "한 번에 던져서"이지 내재화 부재가 아니다
- [[../atoms/xyz-skhx-market/12-netting-two-kinds-only-one-is-ours]] — netting은 두 가지이며 계정 레벨만 우리 것이다
- [[../atoms/xyz-skhx-market/13-related-observations-torii-terminal]] — 관련 실측 — xyz는 메인보다 4배 싸고, 빌더코드 HIP-3 952건·경쟁요율 1.2~5.0bp, 한국물 25.9%
