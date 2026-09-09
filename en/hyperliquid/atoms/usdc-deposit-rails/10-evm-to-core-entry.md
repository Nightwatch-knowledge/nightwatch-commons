---
id: hyperliquid.atom.usdc-deposit-rails.10
lang: en
title: EVM → Core entry — approve+deposit on CoreDepositWallet (common to contracts and wallets)
status: verified
as_of: 2026-08-17
hub: "[[../../rails/usdc-deposit-rails]]"
source: "corewriter-vaults EVM↔Core verification"
tags: [CCTP, HyperEVM, USDC]
contributors: [house]
---

# EVM → Core entry — approve+deposit on CoreDepositWallet (common to contracts and wallets)

To move USDC from EVM into Core, whether via contract or wallet, call `approve` + `deposit(amount_6dec, destinationDex)` on the Circle CoreDepositWallet `0x6b9e773128f453f5c2c60935ee2de2cbc5390a24`. ERC20 transfer is prohibited.

**Basis**: "EVM → Core entry (common to contracts and wallets) Circle CoreDepositWallet 0x6b9e773128f453f5c2c60935ee2de2cbc5390a24 approve + deposit(amount_6dec, destinationDex) — ERC20 transfer prohibited. Details → facts/corewriter-vaults"

Related: [[../corewriter-vaults/13-evm-to-core-usdc-deposit]]
