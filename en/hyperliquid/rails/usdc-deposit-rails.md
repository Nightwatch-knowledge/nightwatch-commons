---
id: hl.rails.usdc-deposit
lang: en
title: Deposit/Withdrawal Rails — Protocol (Arbitrum-only) vs. App, and the Next-Gen Canonical CCTP v2→HyperEVM
status: verified
as_of: 2026-08-17
sources: ["Bridge doc (quoted twice)", "Onboarding doc", "Circle CCTP v2 domain list", "HL official announcement (Arbitrum bridge to be deprecated)"]
contributors: [house]
tags: [deposit, withdraw, Bridge2, CCTP, HyperEVM, USDC]
tier_candidate: commons
---

# USDC Deposit/Withdrawal Rails

## Protocol (Bridge2) = Arbitrum USDC Only
> "Hyperliquid's native bridge is between Hyperliquid and **Arbitrum**."
> "the Hyperliquid **bridge contract only accepts Arbitrum USDC sent over Arbitrum**." (quoted twice in the doc)

## App Feature = Also Accepts Base/Polygon/Ethereum (described only in the email-login onboarding section)
> "You can send USDC on **Arbitrum/Ethereum/Base/Polygon** to **the deposit address shown** ... Your deposit arrives as USDC on HyperCore."
→ This is a deposit-routing service attached by the HL app frontend. Who operates it and whether an API exists is `unverified`.
→ **We cannot use this**: we don't send users to app.hyperliquid.xyz, and we can use a contract even less.

## Non-USDC Deposits (accepted as spot → sold for USDC)
BTC(Bitcoin) · ETH/ENA(Ethereum) · SOL/2Z/ANSEM/BONK/FARTCOIN/PUMP/SPX(Solana) · MON(Monad) · XPL(Plasma) · AVAX(Avalanche) · ZEC(Zcash)

## Withdrawal
> "click 'Withdraw to Arbitrum.' This transaction does not cost gas. There is a **$1 withdrawal fee** instead."

## The Real Structure Behind "Unification" (as of 2026-07-31)
```
Base USDC   ┐
Polygon USDC├→ [bridge layer] → Arbitrum USDC → Bridge2 → HyperCore
Ethereum    ┘                      ↑ sole protocol entry point
```
What can be unified is the front end, and we already have it — the `/torii/fund` LI.FI widget is live (`FUND_RAIL_TIERS` T3, our fee is 0).

## ★ Next-Gen Canonical: CCTP v2 → HyperEVM (2026-08-16 Phase 0)
- **CCTP v2 domain 19 = HyperEVM** [Circle official]. **Standard only, Fast not available** → deposits from Base are delayed ~13-19 minutes (must be reflected in UX)
- **HyperEVM native USDC = `0xb88339CB7199b77E23DB6E890353E22632Ba630f`** (testnet `0x2B3370eE501B4a559b57D449569354196457D8Ab`). CCTP v2 contract addresses are uniform across chains (TokenMessengerV2 `0x28b5…cf5d`)
- **In 2025-12, USDC became officially linked HyperCore↔HyperEVM** + HL officially: "In the final state, **the Arbitrum bridge will be deprecated** and all USDC will be natively minted." → **Our CCTP path is not a workaround — it's the next-gen canonical.** This settles the T1 (CCTP) vs. T3 (LI.FI) debate (reflected in design = `SMART_VAULT_DESIGN.md` §4)
- Code action: add `NATIVE_USDC[999]` to `depositAssets.js`, resolving the TODO at :252-259

## EVM → Core Entry (common to contracts and wallets)
Call `approve` + `deposit(amount_6dec, destinationDex)` on the Circle CoreDepositWallet `0x6b9e773128f453f5c2c60935ee2de2cbc5390a24` — ERC20 transfer is prohibited. Details → [[../facts/corewriter-vaults]]

## Atoms
- [[../atoms/usdc-deposit-rails/01-protocol-bridge2-arbitrum-only]] — The protocol (Bridge2) is Arbitrum USDC only
- [[../atoms/usdc-deposit-rails/02-app-feature-multichain-but-unusable-for-us]] — The app feature also accepts Base/Polygon/Ethereum, but we cannot use it
- [[../atoms/usdc-deposit-rails/03-non-usdc-deposit-list]] — List of supported non-USDC deposits — accepted as spot, sold for USDC
- [[../atoms/usdc-deposit-rails/04-withdrawal-1usd-fee-no-gas]] — Withdrawal — Withdraw to Arbitrum, no gas, $1 fee
- [[../atoms/usdc-deposit-rails/05-unified-structure-and-existing-lifi-widget]] — The real structure behind unification — multiple chains flow through a bridge layer to Arbitrum, and we already have the LI.FI widget
- [[../atoms/usdc-deposit-rails/06-cctp-v2-domain19-standard-only]] — CCTP v2 domain 19 = HyperEVM — Standard only, Fast not available, 13-19 minute delay
- [[../atoms/usdc-deposit-rails/07-native-usdc-address-mainnet-testnet]] — HyperEVM native USDC address (mainnet and testnet) + uniform TokenMessengerV2 address
- [[../atoms/usdc-deposit-rails/08-arbitrum-bridge-deprecated-cctp-is-canonical]] — Conclusion — the CCTP path is not a workaround, it's the next-gen canonical
- [[../atoms/usdc-deposit-rails/09-code-action-depositassets-todo]] — Code action — resolve the TODO by adding NATIVE_USDC[999] to depositAssets.js
- [[../atoms/usdc-deposit-rails/10-evm-to-core-entry]] — EVM → Core entry — approve+deposit on CoreDepositWallet (common to contracts and wallets)
