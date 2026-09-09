---
id: hyperliquid.atom.api-access.01
title: User-Agent 헤더 없으면 429 — rate limit이 아니다
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "실측"
tags: [api, rate-limit]
contributors: [house]
---

# User-Agent 헤더 없으면 429 — rate limit이 아니다

`api.hyperliquid.xyz`는 User-Agent 헤더가 없으면 429를 반환한다. 이는 rate limit이 아니라 헤더 누락 문제다.

**근거**: "User-Agent | api.hyperliquid.xyz는 User-Agent 헤더가 없으면 429. rate limit이 아니다"

관련: [[../../gates/api-user-agent]]
