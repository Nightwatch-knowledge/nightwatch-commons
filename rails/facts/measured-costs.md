---
id: rails.facts.measured-costs
title: 실측 비용표 — 수수료·지연·체인 격차
status: verified
as_of: 2026-09-06
sources: [QM_RAIL_LOG.md, project_transfer_intelligence, project_qm_rail_kg, feedback_fee_discipline_rails, ops_gpilot_egl1_stuck]
contributors: [house]
tags: [fee, transit, chain, cost]
tier_candidate: commons
---

# 실측 비용표

## 체인 격차 — 같은 경로가 8~75배 다르다
| 경로 | 체인별 수수료 | 격차 |
|---|---|---|
| binance → bithumb | KAIA 0.02 / TRX 1.5 | **75배** |
| binance → bybit | BSC 0.01 / SOL 0.30 | 30배 (BSC가 더 빠르기도 함) |
| bybit → binance | PLASMA $0 / KAIA $0.1 / ERC20 $0.8 | 8배 (공시, 0은 unknown_zero) |
| gate 출금 | 허브 EOA 경유 0.025 / 직접 CEX 0.5 | 20배 |

원칙 (Robin 2026-08-14): **"수수료 절감 = 차익거래의 가장 중요한 일."** 사이클 마진 0.25~2%에서 이송 0.1%p = 순익의 수십 %. 싼 체인은 "선택지"가 아니라 **기본값** → [[../gates/lowest-fee-chain-default]]

## 지연 (접수 → 도착 확인)
| 경로·체인 | 지연 |
|---|---|
| binance→bybit BSC | 81초 |
| mexc→binance BSC | 80초 |
| binance→bithumb KAIA | 99초 |
| binance→bybit SOL | 141초 |
| kucoin→gate BEP20 | 151초 |
| mexc→EOA ETH/ARB | 70초 |
| Base→HyperEVM CCTP v2 (Standard) | 13~19분 (참고: Hyperliquid Playbook) |

**느린 체인(p90 > 15분) 또는 2홉 이상 = 헷지 필수** (Robin 2026-09-02) → [[../gates/slow-chain-hedge-required]]. 42사이클 진단: 느린 체인이 손실 원인.

## 공시 vs 실차감 (`fee_match`)
- **binance 공시 출금비는 정직** (2/2 match)
- **bithumb**: `withdraw_fee=0`인데 `withdraw_rate=1%` — 0을 믿으면 틀림 → `unknown_zero` 원칙
- **kucoin BEP20**: 30 EGL1 요청량에서 차감 (실측 08-30)
- **STRK 출금비 $35.9** — 체인 성립 ≠ 경제성. 수수료가 사이클 마진을 삼키면 그 체인은 없는 것

## Atoms
- [[../atoms/measured-costs/01-chain-gap-binance-bithumb]] — binance→bithumb 체인격차 — KAIA 0.02 vs TRX 1.5, 75배
- [[../atoms/measured-costs/02-chain-gap-binance-bybit]] — binance→bybit 체인격차 — BSC 0.01 vs SOL 0.30, 30배
- [[../atoms/measured-costs/03-chain-gap-bybit-binance]] — bybit→binance 체인격차 — PLASMA $0·KAIA $0.1·ERC20 $0.8, 8배
- [[../atoms/measured-costs/04-chain-gap-gate-withdraw]] — gate 출금 — 허브경유 0.025 vs 직접CEX 0.5, 20배
- [[../atoms/measured-costs/05-principle-lowest-fee-default]] — 원칙 — 싼 체인은 선택지가 아니라 기본값
- [[../atoms/measured-costs/06-transit-binance-bybit-bsc]] — binance→bybit BSC 지연 81초
- [[../atoms/measured-costs/07-transit-mexc-binance-bsc]] — mexc→binance BSC 지연 80초
- [[../atoms/measured-costs/08-transit-binance-bithumb-kaia]] — binance→bithumb KAIA 지연 99초
- [[../atoms/measured-costs/09-transit-binance-bybit-sol]] — binance→bybit SOL 지연 141초
- [[../atoms/measured-costs/10-transit-kucoin-gate-bep20]] — kucoin→gate BEP20 지연 151초
- [[../atoms/measured-costs/11-transit-mexc-eoa-eth-arb]] — mexc→허브EOA ETH/ARB 지연 70초
- [[../atoms/measured-costs/12-transit-base-hyperevm-cctp]] — Base→HyperEVM CCTP v2 지연 13~19분
- [[../atoms/measured-costs/13-principle-slow-chain-hedge]] — 느린 체인(p90>15분)·2홉 이상은 헷지 필수
- [[../atoms/measured-costs/14-fee-disclosure-binance-honest]] — binance 공시 출금비는 정직 (2/2 match)
- [[../atoms/measured-costs/15-fee-disclosure-bithumb-unknown-zero]] — bithumb withdraw_fee=0인데 실제 rate 1% — unknown_zero
- [[../atoms/measured-costs/16-fee-disclosure-kucoin-bep20]] — kucoin BEP20 — 30 EGL1이 요청량에서 차감(실측 08-30)
- [[../atoms/measured-costs/17-fee-disclosure-strk]] — STRK 출금비 $35.9 — 체인 성립 ≠ 경제성
