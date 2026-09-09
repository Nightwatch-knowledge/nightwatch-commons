---
id: rails.maps.route-map
title: 경로 맵 — 거래소·체인·회랑 (실측 기준)
status: verified (표기된 것만) / unobserved (나머지)
as_of: 2026-09-12
freshness_note: "수수료·문 상태는 주 단위로 낡는다. 최신값=nw_kg_facts(venue:%) / get_pair_gate. 이 맵은 구조와 검증된 회랑을 담는다"
sources: [QM_RAIL_LOG.md, project_transfer_intelligence, project_qm_rail_kg, feedback_fee_discipline_rails]
contributors: [house]
tier_candidate: commons
---

# 경로 맵

## 1. 전체 구조 (실선=실송금 실증, 점선=규정상 가능·미실증)

```mermaid
graph LR
  subgraph KR[한국 leg — 트래블룰]
    BITHUMB[bithumb<br/>단일지갑 · 주소록 사전등록 · 출금 1% 정률 가산]
    UPBIT[upbit<br/>단일지갑 · 화이트리스트 320쌍]
  end
  subgraph GLOBAL[글로벌 허브]
    BINANCE[binance<br/>10버킷 · 출금=spot · 절차 없음]
    BYBIT[bybit<br/>2버킷 · 출금=FUND · 주소등록]
    MEXC[mexc<br/>단일 · 절차 없음]
    GATE[gate<br/>단일 · 통화×체인×주소별 수동출금 1회+24h]
    KUCOIN[kucoin<br/>출금=main]
    OKX[okx<br/>출금=funding]
    BITGET[bitget]
  end
  HUB((허브 EOA<br/>자기 지갑))

  BINANCE ==>|KAIA 0.02 · 99s| BITHUMB
  BINANCE -.->|TRX 1.5 (75배)| BITHUMB
  BINANCE ==>|BSC 0.01 · 81s| BYBIT
  BINANCE ==>|SOL 0.30 · 141s| BYBIT
  MEXC ==>|BSC 0.01 · 80s| BINANCE
  MEXC ==>|ETH/ARB ~0 · 70s| HUB
  HUB ==>|가스 $0.0024| GATE
  GATE ==>|0.025 (직접출금 0.5의 1/20)| HUB
  BYBIT -.->|ERC20 $0.8 / KAIA $0.1 / PLASMA $0| BINANCE
  BYBIT -.->|TRX 1.0 · 주소등록 필요| BITHUMB
  KUCOIN ==>|BEP20 fee 30 차감 · 151s| GATE
  BITGET -.->|트래블룰 OK| BITHUMB
  OKX -.->|트래블룰 OK| BITHUMB
  GATE -.->|건당 <₩1M · 7영업일 등록| BITHUMB
  MEXC x--x|트래블룰 불가| BITHUMB
  KUCOIN x--x|트래블룰 불가| BITHUMB
```

## 2. 회랑 표 (실측만 — 날짜 붙음)

| 출발 → 도착 | 체인 | 공시비 | 실차감 | 지연 | 결과 | 실측일 |
|---|---|---|---|---|---|---|
| binance → bithumb | **KAIA** | 0.02 USDT | 0.02 | 99초 | ok | 2026-08-08 |
| binance → bithumb | TRX | 1.5 | — | — | 비추천 (KAIA의 75배) | 2026-08-08 |
| binance → bybit | **BSC** | 0.01 | 0.01 match | 1분21초 | ok, 2FA 없음 | 2026-08-02 |
| binance → bybit | SOL | 0.30 | 0.30 match | 2분21초 | ok (BSC보다 30배 비쌈) | 2026-08-02 |
| mexc → binance | BSC | 0.01 | 0.01 match | 80초 | ok (netWork 코드 필수) | 2026-08-03 |
| mexc → 허브 EOA | ETH/ARB | 0.00000084 | — | 70초 | ok | 2026-08-08 |
| 허브 EOA → gate | (온체인 가스) | $0.0024 | — | — | ok | 2026-08-08 |
| gate → 허브 EOA | — | 0.025 | — | — | ok (직접 CEX 출금 0.5의 1/20) | 2026-08-08 |
| kucoin → gate | BEP20 | 30 (차감) | 30 | 151초 | ok (EGL1 회수) | 2026-08-30 |
| bybit → bithumb | TRX | 1.0 (최소 2.6, 20블록) | — | — | **needs_address_registration** — 돈 안 움직임 | 2026-08-02 |
| bithumb → binance | — | 정률 1% **가산** | 요청량+1% | — | ok (SAPIEN 3,600 → 도착 3,565) | 2026-08-30 |

원칙: **온체인 구간 비용은 거래소 출금비의 1/200~1/400.** 허브 EOA 패턴(CEX → 자기 지갑 → 임의 CEX)이 목적지별 주소등록을 지갑 1개로 축소한다.

## 3. 한국 leg — 병목이 여기다

- **빗썸 USDT 수용 체인**: ETH · TRX · KAIA · APT (2026-08-08 확정. 08-02 시점엔 입금 TRX만 성공/BSC·SOL·MATIC·BASE 400 — 체인 개통이 늘어난 것이 아니라 관측이 늘어난 것. 최신 = KG)
- **KAIA가 한국행 최저**: 0.02 vs TRX 1.5
- **빗썸 출금 = 1% 정률(254종) / 정액(14종) / 0(BTT-TRX·TT)**, 그리고 **요청량에 가산** → 정산에서 유령 잔여로 보였던 것 = 수수료 ([[../lessons/what-generalises]] #2)
- **빗썸 주소록 = (주소+자산)별 사전등록**, API 조회 0건(화면과 불일치) — 등록 상태는 화면에서 확인
- **업비트 화이트리스트 320쌍**, ETH 체인 259쌍은 `chain_policy_mode=fee_known_and_hedged`로 열림(2026-09-06). 업비트→gate 등록쌍 14 (ARB·TRX). 병목은 업비트가 아니라 우리 매도처 목록(gateio 개방 진행)
- **빗썸 leg가 병목인 사례 다수** (XCN $5k 빗썸 8.29%p) — 해외 쪽만 보는 등급 금지

## 4. 트래블룰 연결 (빗썸 기준)
- 자유송금 **10곳**: bitget · bybit · okx · binance · HTX · Toobit + (rail_atlas 8/1 명단 4곳) — HTX·Toobit은 8/1 atlas에 누락, 코드 반영 대기
- 불가: mexc · gate(중간 티어) · kucoin
- **Gate = 중간 티어**: CODE 연동(2024-03)됐지만 빗썸 미활성 → "그 외 거래소" = 주소 사전등록(7영업일) 후 **건당 <₩1M**, 반복출금 감시 조항 → **봇 상시 파이프 금지, 간헐만**
- **미신고 차단 41곳 확정** (BingX 2026-01-12 추가, BitMart·WEEX·Blofin·CoinW 포함) — 등록 불가, 재조사 금지
- 우회로 대기: mexc → OKX → 빗썸 (OKX 어댑터 완성 후)

## 5. 기계용 회랑 정의 (검증된 것만)

```yaml
corridors:
  - {from: binance, to: bithumb, chain: KAIA, fee_usdt: 0.02, transit_s: 99, status: verified, as_of: 2026-08-08, default: true}
  - {from: binance, to: bithumb, chain: TRX,  fee_usdt: 1.5,  status: avoid, reason: "KAIA의 75배"}
  - {from: binance, to: bybit,   chain: BSC,  fee_usdt: 0.01, transit_s: 81,  status: verified, as_of: 2026-08-02, default: true}
  - {from: binance, to: bybit,   chain: SOL,  fee_usdt: 0.30, transit_s: 141, status: verified, as_of: 2026-08-02}
  - {from: mexc,    to: binance, chain: BSC,  fee_usdt: 0.01, transit_s: 80,  status: verified, as_of: 2026-08-03, note: "netWork 코드 필수(표시명 금지)"}
  - {from: kucoin,  to: gateio,  chain: BEP20, fee_token: 30, transit_s: 151, status: verified, as_of: 2026-08-30, fee_model: deduct}
  - {from: bybit,   to: bithumb, chain: TRX,  fee_usdt: 1.0, min: 2.6, status: blocked_until_address_registration, as_of: 2026-08-02}
  - {from: bithumb, to: binance, chain: "*",  fee_pct: 1.0, fee_model: add_on_top, status: verified, as_of: 2026-08-30}
  - {from: bybit,   to: binance, chain: PLASMA, fee_usd: 0,   status: quoted_unverified, note: "fee 0 = unknown_zero 취급"}
  - {from: bybit,   to: binance, chain: KAIA,   fee_usd: 0.1, status: quoted_unverified}
  - {from: bybit,   to: binance, chain: ERC20,  fee_usd: 0.8, status: quoted_unverified}
progress_unit: "경로(9×8=72) 기준. 체인은 경로 아래 축 — 같은 경로 다체인은 진행률을 올리지 않는다"
```

최신 회랑 상태는 `nw_kg_facts` `rail:<to>:<chain>:*`(일 1행)에서 읽는다. 이 YAML은 스냅샷이다.

## Atoms
- [[../atoms/route-map/01-corridor-binance-bithumb-kaia]] — 회랑 binance→bithumb KAIA — ok, 99초, 2026-08-08
- [[../atoms/route-map/02-corridor-binance-bithumb-trx]] — 회랑 binance→bithumb TRX — 비추천(KAIA의 75배)
- [[../atoms/route-map/03-corridor-binance-bybit-bsc]] — 회랑 binance→bybit BSC — ok, 2FA없음, 81초, 2026-08-02
- [[../atoms/route-map/04-corridor-binance-bybit-sol]] — 회랑 binance→bybit SOL — ok(BSC보다 30배 비쌈), 2026-08-02
- [[../atoms/route-map/05-corridor-mexc-binance-bsc]] — 회랑 mexc→binance BSC — ok(netWork코드 필수), 80초, 2026-08-03
- [[../atoms/route-map/06-corridor-mexc-eoa]] — 회랑 mexc→허브EOA ETH/ARB — ok, 70초, 2026-08-08
- [[../atoms/route-map/07-corridor-eoa-gate]] — 회랑 허브EOA→gate — 온체인가스 $0.0024, ok, 2026-08-08
- [[../atoms/route-map/08-corridor-gate-eoa]] — 회랑 gate→허브EOA — 0.025, 직접CEX출금 0.5의 1/20, ok
- [[../atoms/route-map/09-corridor-kucoin-gate-bep20]] — 회랑 kucoin→gate BEP20 — 30차감, 151초, ok(EGL1회수), 2026-08-30
- [[../atoms/route-map/10-corridor-bybit-bithumb-trx]] — 회랑 bybit→bithumb TRX — needs_address_registration, 돈 안움직임, 2026-08-02
- [[../atoms/route-map/11-corridor-bithumb-binance]] — 회랑 bithumb→binance — 정률1% 가산, ok(SAPIEN 3600→3565), 2026-08-30
- [[../atoms/route-map/12-onchain-cost-principle]] — 온체인 구간 비용 = 거래소 출금비의 1/200~1/400
- [[../atoms/route-map/13-bottleneck-bithumb-usdt-chains]] — 빗썸 USDT수용체인 확정(08-08) — 개통 아니라 관측 증가
- [[../atoms/route-map/14-bottleneck-kaia-lowest]] — KAIA가 한국행 최저 (0.02 vs TRX 1.5)
- [[../atoms/route-map/15-bottleneck-bithumb-fee-ghost]] — 빗썸 출금 가산 수수료가 정산 유령 잔여로 보였던 원인
- [[../atoms/route-map/16-bottleneck-bithumb-address-book]] — 빗썸 주소록 = (주소+자산)별 사전등록, 화면에서만 확인
- [[../atoms/route-map/17-bottleneck-upbit-whitelist]] — 업비트 화이트리스트 320쌍 — 병목은 우리 매도처 목록
- [[../atoms/route-map/18-bottleneck-bithumb-leg-cases]] — 빗썸 leg가 병목인 사례 다수 (XCN $5k 빗썸 8.29%p)
- [[../atoms/route-map/19-travel-rule-free-10]] — 트래블룰 자유송금 10곳 (HTX·Toobit 코드반영 대기)
- [[../atoms/route-map/20-travel-rule-impossible]] — 트래블룰 불가 — mexc·gate(중간티어)·kucoin
- [[../atoms/route-map/21-travel-rule-gate-midtier]] — Gate 중간티어 — 사전등록 후 건당<₩1M, 봇상시금지 간헐만
- [[../atoms/route-map/22-travel-rule-blocked41]] — 미신고 차단 41곳 확정 — 재조사 금지
- [[../atoms/route-map/23-travel-rule-workaround]] — 우회로 대기 — mexc→OKX→빗썸(OKX 어댑터 완성 후)
- [[../atoms/route-map/24-yaml-corridor-bybit-binance-plasma]] — 회랑(YAML) bybit→binance PLASMA fee $0 — quoted_unverified
- [[../atoms/route-map/25-yaml-corridor-bybit-binance-kaia]] — 회랑(YAML) bybit→binance KAIA fee $0.1 — quoted_unverified
- [[../atoms/route-map/26-yaml-corridor-bybit-binance-erc20]] — 회랑(YAML) bybit→binance ERC20 fee $0.8 — quoted_unverified
- [[../atoms/route-map/27-progress-unit]] — 진행률 단위 = 경로(9×8=72) 기준, 체인은 하위 축
