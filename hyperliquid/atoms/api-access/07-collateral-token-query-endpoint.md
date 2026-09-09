---
id: hyperliquid.atom.api-access.07
title: 담보 토큰 조회 엔드포인트
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "info API"
tags: [api, account-mode]
contributors: [house]
---

# 담보 토큰 조회 엔드포인트

dex별 담보 토큰은 info `{"type":"meta","dex":X}` → `collateralToken`으로 조회한다.

**근거**: "담보 토큰 조회 | info {"type":"meta","dex":X} → collateralToken"

관련: [[../account-modes/06-collateral-token-per-dex-mapping]]
