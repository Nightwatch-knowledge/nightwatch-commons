---
id: hyperliquid.atom.api-access.09
lang: en
title: HyperEVM log query — eth_getLogs, max 1000 blocks/query, ~1req/s pacing required
status: verified
as_of: 2026-08-17
hub: "[[../../rails/api-access]]"
source: "eth_getLogs measured"
tags: [api, HyperEVM]
contributors: [house]
---

# HyperEVM log query — eth_getLogs, max 1000 blocks/query, ~1req/s pacing required

HyperEVM logs are queried via `eth_getLogs` on `0x3333…3333`, with a limit of max 1000 blocks per query, and ~1req/s pacing is required.

**Basis**: "HyperEVM logs | eth_getLogs 0x3333…3333, max 1000 blocks/query, ~1req/s pacing required"

Related: [[../corewriter-vaults/12-sample-limits-and-observation-method]]
