---
id: hl.rails.api-access
lang: en
title: API / Data Access Rails — Pitfalls and Endpoints
status: verified
as_of: 2026-08-17
contributors: [house]
tags: [api, rate-limit, stats-data, leaderboard, eth_getLogs]
tier_candidate: commons
---

# API / Data Access

| Item | Fact |
|---|---|
| **User-Agent** | `api.hyperliquid.xyz` returns **429 without a User-Agent header**. It is not a rate limit → [[../gates/api-user-agent]] |
| Official docs dump | `https://hyperliquid.gitbook.io/hyperliquid-docs/llms-full.txt` (484KB, greppable). The page version can be newer than the dump (case: 07-17 page vs. 07-31 dump) |
| Leaderboard | `GET https://stats-data.hyperliquid.xyz/Mainnet/leaderboard` — 41,031 rows, EOAs are auto-listed. Not documented in the official gitbook (`unverified` stability) |
| Vault list | `.../Mainnet/vaults` — 9,466 entries. The info API's `vaultSummaries` returns `[]` (non-functional) |
| Builder fills CSV | `stats-data.hyperliquid.xyz/Mainnet/builder_fills/{builder}/{YYYYMMDD}.csv.lz4` |
| Mode query | info `{"type":"userAbstraction","user":…}` |
| Collateral token query | info `{"type":"meta","dex":X}` → `collateralToken` |
| extraAgents | Query **by master address**; only named agents are returned |
| HyperEVM logs | `eth_getLogs` on `0x3333…3333`, max 1000 blocks/query, **~1req/s pacing required** |
| Testnet | chainId 998 · `rpc.hyperliquid-testnet.xyz/evm` · `api.hyperliquid-testnet.xyz` |
| Asset ID | perp `100000 + dex*10000 + i` (xyz=dex 1 → 110000+i) · spot `10000+i` · outcome `100_000_000+encoding` |

## Atoms
- [[../atoms/api-access/01-useragent-required-not-rate-limit]] — 429 without a User-Agent header — not a rate limit
- [[../atoms/api-access/02-official-docs-dump-location]] — Official docs dump location — the page version can be newer than the dump
- [[../atoms/api-access/03-leaderboard-endpoint]] — Leaderboard endpoint — 41,031 rows, EOAs auto-listed
- [[../atoms/api-access/04-vault-list-endpoint]] — Vault list endpoint — 9,466 entries
- [[../atoms/api-access/05-builder-fills-csv-path]] — Builder fills CSV path
- [[../atoms/api-access/06-mode-query-endpoint]] — Mode query endpoint
- [[../atoms/api-access/07-collateral-token-query-endpoint]] — Collateral token query endpoint
- [[../atoms/api-access/08-extraagents-query-rule]] — extraAgents query rule — by master address, only named agents returned
- [[../atoms/api-access/09-hyperevm-log-query-pacing]] — HyperEVM log query — eth_getLogs, max 1000 blocks/query, ~1req/s pacing required
- [[../atoms/api-access/10-testnet-endpoints]] — Testnet endpoints — chainId 998
- [[../atoms/api-access/11-asset-id-scheme]] — Asset ID scheme — three namespaces: perp/spot/outcome
