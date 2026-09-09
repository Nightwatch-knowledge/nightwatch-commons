---
id: hyperliquid.atom.usdc-deposit-rails.02
lang: en
title: The app feature also accepts Base/Polygon/Ethereum, but we cannot use it
status: verified
as_of: 2026-08-17
hub: "[[../../rails/usdc-deposit-rails]]"
source: "Onboarding doc"
tags: [deposit]
contributors: [house]
---

# The app feature also accepts Base/Polygon/Ethereum, but we cannot use it

An app feature, described only in the email-login onboarding section, states that sending USDC on Arbitrum/Ethereum/Base/Polygon to the displayed deposit address will arrive as USDC on HyperCore. This is a deposit-routing service attached by the HL app frontend; who operates it and whether an API exists is `unverified`. Since we don't send users to app.hyperliquid.xyz, and we can use a contract even less, we cannot use this path.

**Basis**: "You can send USDC on Arbitrum/Ethereum/Base/Polygon to the deposit address shown ... Your deposit arrives as USDC on HyperCore." → "We cannot use this: we don't send users to app.hyperliquid.xyz, and we can use a contract even less."

Related: (none)
