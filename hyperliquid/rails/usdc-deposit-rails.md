---
id: hl.rails.usdc-deposit
title: 입금·출금 레일 — 프로토콜(Arbitrum 전용) vs 앱, 그리고 차세대 정본 CCTP v2→HyperEVM
status: verified
as_of: 2026-08-17
sources: ["Bridge 문서 (2회 반복 인용)", "온보딩 문서", "Circle CCTP v2 domain 목록", "HL 공식 발표 (Arbitrum bridge deprecated 예정)"]
contributors: [house]
tags: [deposit, withdraw, Bridge2, CCTP, HyperEVM, USDC]
tier_candidate: commons
---

# USDC 입출금 레일

## 프로토콜 (Bridge2) = Arbitrum USDC 전용
> "Hyperliquid's native bridge is between Hyperliquid and **Arbitrum**."
> "the Hyperliquid **bridge contract only accepts Arbitrum USDC sent over Arbitrum**." (문서 내 2회 반복)

## 앱 기능 = Base/Polygon/Ethereum도 받음 (이메일 로그인 온보딩 항목에만 기술)
> "You can send USDC on **Arbitrum/Ethereum/Base/Polygon** to **the deposit address shown** ... Your deposit arrives as USDC on HyperCore."
→ HL 앱 프론트엔드가 붙인 입금 라우팅 서비스. 운영 주체·API 유무 `unverified`.
→ **우리는 쓸 수 없다**: 유저를 app.hyperliquid.xyz로 안 보내고, 컨트랙트는 더더욱 못 쓴다.

## 비USDC 입금 (spot으로 받아줌 → 팔아서 USDC)
BTC(Bitcoin) · ETH/ENA(Ethereum) · SOL/2Z/ANSEM/BONK/FARTCOIN/PUMP/SPX(Solana) · MON(Monad) · XPL(Plasma) · AVAX(Avalanche) · ZEC(Zcash)

## 출금
> "click 'Withdraw to Arbitrum.' This transaction does not cost gas. There is a **$1 withdrawal fee** instead."

## 통일성의 진짜 구조 (2026-07-31 시점)
```
Base USDC   ┐
Polygon USDC├→ [브리지 레이어] → Arbitrum USDC → Bridge2 → HyperCore
Ethereum    ┘                      ↑ 유일한 프로토콜 진입점
```
통일 가능한 것은 앞단이고 우리는 이미 갖고 있다 — `/torii/fund` LI.FI 위젯 라이브(`FUND_RAIL_TIERS` T3, 우리 수수료 0).

## ★ 차세대 정본: CCTP v2 → HyperEVM (2026-08-16 Phase 0)
- **CCTP v2 domain 19 = HyperEVM** [Circle 공식]. **Standard만, Fast 불가** → Base발 입금 ~13-19분 지연 (UX 반영 필수)
- **HyperEVM 네이티브 USDC = `0xb88339CB7199b77E23DB6E890353E22632Ba630f`** (테스트넷 `0x2B3370eE501B4a559b57D449569354196457D8Ab`). CCTP v2 컨트랙트 주소는 타 체인과 균일 (TokenMessengerV2 `0x28b5…cf5d`)
- **2025-12 USDC가 HyperCore↔HyperEVM 공식 linked** + HL 공식: "In the final state, **the Arbitrum bridge will be deprecated** and all USDC will be natively minted." → **우리 CCTP 경로가 우회로가 아니라 차세대 정본.** T1(CCTP) vs T3(LI.FI) 논쟁은 이것으로 판가름 (설계 반영 = `SMART_VAULT_DESIGN.md` §4)
- 코드 액션: `depositAssets.js` NATIVE_USDC[999] 추가, :252-259 TODO 해소

## EVM → Core 진입 (컨트랙트·지갑 공통)
Circle CoreDepositWallet `0x6b9e773128f453f5c2c60935ee2de2cbc5390a24`에 `approve` + `deposit(amount_6dec, destinationDex)` — ERC20 transfer 금지. 상세 → [[../facts/corewriter-vaults]]

## Atoms
- [[../atoms/usdc-deposit-rails/01-protocol-bridge2-arbitrum-only]] — 프로토콜(Bridge2)은 Arbitrum USDC 전용이다
- [[../atoms/usdc-deposit-rails/02-app-feature-multichain-but-unusable-for-us]] — 앱 기능은 Base/Polygon/Ethereum도 받지만 우리는 쓸 수 없다
- [[../atoms/usdc-deposit-rails/03-non-usdc-deposit-list]] — 비USDC 입금 지원 목록 — spot으로 받아 팔아서 USDC화
- [[../atoms/usdc-deposit-rails/04-withdrawal-1usd-fee-no-gas]] — 출금 — Withdraw to Arbitrum, 가스 없음, $1 수수료
- [[../atoms/usdc-deposit-rails/05-unified-structure-and-existing-lifi-widget]] — 통일성의 실제 구조 — 여러 체인이 브리지 레이어를 거쳐 Arbitrum으로, 우리는 이미 LI.FI 위젯 보유
- [[../atoms/usdc-deposit-rails/06-cctp-v2-domain19-standard-only]] — CCTP v2 domain 19 = HyperEVM — Standard만, Fast 불가, 13~19분 지연
- [[../atoms/usdc-deposit-rails/07-native-usdc-address-mainnet-testnet]] — HyperEVM 네이티브 USDC 주소(메인넷·테스트넷) + TokenMessengerV2 균일 주소
- [[../atoms/usdc-deposit-rails/08-arbitrum-bridge-deprecated-cctp-is-canonical]] — 결론 — CCTP 경로가 우회로가 아니라 차세대 정본이다
- [[../atoms/usdc-deposit-rails/09-code-action-depositassets-todo]] — 코드 액션 — depositAssets.js NATIVE_USDC[999] 추가로 TODO 해소
- [[../atoms/usdc-deposit-rails/10-evm-to-core-entry]] — EVM → Core 진입 — CoreDepositWallet에 approve+deposit(컨트랙트·지갑 공통)
