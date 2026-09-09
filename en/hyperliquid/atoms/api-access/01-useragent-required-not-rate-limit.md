---
id: hyperliquid.atom.api-access.01
lang: en
title: 429 without a User-Agent header — not a rate limit
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "measured"
tags: [api, rate-limit]
contributors: [house]
---

# 429 without a User-Agent header — not a rate limit

`api.hyperliquid.xyz` returns 429 when the User-Agent header is missing. This is a missing-header issue, not a rate limit.

**Basis**: "User-Agent | api.hyperliquid.xyz returns 429 without a User-Agent header. Not a rate limit"

Related: [[../../gates/api-user-agent]]
