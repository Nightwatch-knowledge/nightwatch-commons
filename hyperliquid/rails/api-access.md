---
id: hl.rails.api-access
title: API·데이터 접근 레일 — 함정과 엔드포인트
status: verified
as_of: 2026-08-17
contributors: [house]
tags: [api, rate-limit, stats-data, leaderboard, eth_getLogs]
tier_candidate: commons
---

# API·데이터 접근

| 항목 | 사실 |
|---|---|
| **User-Agent** | `api.hyperliquid.xyz`는 **User-Agent 헤더가 없으면 429**. rate limit이 아니다 → [[../gates/api-user-agent]] |
| 공식 문서 덤프 | `https://hyperliquid.gitbook.io/hyperliquid-docs/llms-full.txt` (484KB, grep 가능). 페이지판이 덤프보다 최신일 수 있음 (07-17판 vs 07-31 덤프 사례) |
| 리더보드 | `GET https://stats-data.hyperliquid.xyz/Mainnet/leaderboard` — 41,031행, EOA 자동 등재. 공식 gitbook 미기재 (`unverified` 안정성) |
| 볼트 목록 | `.../Mainnet/vaults` — 9,466개. info API `vaultSummaries`는 `[]` 반환(비작동) |
| 빌더 체결 CSV | `stats-data.hyperliquid.xyz/Mainnet/builder_fills/{builder}/{YYYYMMDD}.csv.lz4` |
| 모드 조회 | info `{"type":"userAbstraction","user":…}` |
| 담보 토큰 조회 | info `{"type":"meta","dex":X}` → `collateralToken` |
| extraAgents | **마스터 주소로** 조회, named만 반환 |
| HyperEVM 로그 | `eth_getLogs` `0x3333…3333`, 최대 1000블록/쿼리, **~1req/s 페이싱 필수** |
| 테스트넷 | chainId 998 · `rpc.hyperliquid-testnet.xyz/evm` · `api.hyperliquid-testnet.xyz` |
| 자산 ID | perp `100000 + dex*10000 + i` (xyz=dex 1 → 110000+i) · spot `10000+i` · outcome `100_000_000+encoding` |

## Atoms
- [[../atoms/api-access/01-useragent-required-not-rate-limit]] — User-Agent 헤더 없으면 429 — rate limit이 아니다
- [[../atoms/api-access/02-official-docs-dump-location]] — 공식 문서 덤프 위치 — 페이지판이 덤프보다 최신일 수 있음
- [[../atoms/api-access/03-leaderboard-endpoint]] — 리더보드 엔드포인트 — 41,031행, EOA 자동 등재
- [[../atoms/api-access/04-vault-list-endpoint]] — 볼트 목록 엔드포인트 — 9,466개
- [[../atoms/api-access/05-builder-fills-csv-path]] — 빌더 체결 CSV 경로
- [[../atoms/api-access/06-mode-query-endpoint]] — 모드 조회 엔드포인트
- [[../atoms/api-access/07-collateral-token-query-endpoint]] — 담보 토큰 조회 엔드포인트
- [[../atoms/api-access/08-extraagents-query-rule]] — extraAgents 조회 규칙 — 마스터 주소로, named만 반환
- [[../atoms/api-access/09-hyperevm-log-query-pacing]] — HyperEVM 로그 조회 — eth_getLogs, 최대 1000블록/쿼리, ~1req/s 페이싱 필수
- [[../atoms/api-access/10-testnet-endpoints]] — 테스트넷 엔드포인트 — chainId 998
- [[../atoms/api-access/11-asset-id-scheme]] — 자산 ID 체계 — perp/spot/outcome 세 네임스페이스
