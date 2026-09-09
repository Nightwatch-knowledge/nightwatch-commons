---
id: hyperliquid.atom.api-access.09
title: HyperEVM 로그 조회 — eth_getLogs, 최대 1000블록/쿼리, ~1req/s 페이싱 필수
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "eth_getLogs 실측"
tags: [api, HyperEVM]
contributors: [house]
---

# HyperEVM 로그 조회 — eth_getLogs, 최대 1000블록/쿼리, ~1req/s 페이싱 필수

HyperEVM 로그는 `eth_getLogs`로 `0x3333…3333`을 조회하며, 최대 1000블록/쿼리 제한이 있고 ~1req/s 페이싱이 필수다.

**근거**: "HyperEVM 로그 | eth_getLogs 0x3333…3333, 최대 1000블록/쿼리, ~1req/s 페이싱 필수"

관련: [[../corewriter-vaults/12-sample-limits-and-observation-method]]
