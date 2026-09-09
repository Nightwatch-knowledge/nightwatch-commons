---
id: hyperliquid.atom.usdc-deposit-rails.10
title: EVM → Core 진입 — CoreDepositWallet에 approve+deposit(컨트랙트·지갑 공통)
status: verified
as_of: 2026-08-17
hub: "[[../../rails/usdc-deposit-rails]]"
source: "corewriter-vaults EVM↔Core 실증"
tags: [CCTP, HyperEVM, USDC]
contributors: [house]
---

# EVM → Core 진입 — CoreDepositWallet에 approve+deposit(컨트랙트·지갑 공통)

EVM에서 Core로 USDC를 진입시킬 때는 컨트랙트든 지갑이든 공통으로 Circle CoreDepositWallet `0x6b9e773128f453f5c2c60935ee2de2cbc5390a24`에 `approve` + `deposit(amount_6dec, destinationDex)`를 호출한다. ERC20 transfer는 금지된다.

**근거**: "EVM → Core 진입 (컨트랙트·지갑 공통) Circle CoreDepositWallet 0x6b9e773128f453f5c2c60935ee2de2cbc5390a24에 approve + deposit(amount_6dec, destinationDex) — ERC20 transfer 금지. 상세 → facts/corewriter-vaults"

관련: [[../corewriter-vaults/13-evm-to-core-usdc-deposit]]
