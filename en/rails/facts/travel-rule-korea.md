---
id: rails.facts.travel-rule-korea
lang: en
title: Travel Rule and Korea Exchange Connection Map
status: verified
as_of: 2026-09-06
sources: [BITHUMB_COUNTERPARTY_MAP.md, research/2026-08-05-bithumb-counterparty/, feedback_fee_discipline_rails]
contributors: [house]
tags: [travel-rule, bithumb, upbit, korea, whitelist]
tier_candidate: commons
---

# Travel Rule — Rules of the Korea Leg

## Bithumb connection grades
| Grade | Exchange | Condition |
|---|---|---|
| Free transfer (Travel Rule-linked) | bitget · bybit · okx · binance · **HTX · Toobit** (+atlas 8/1 list) = **10 venues** | One-time registration per exchange |
| **Mid tier** | **Gate** | CODE-linked (2024-03) but inactive on bithumb → after 7 business days of address pre-registration, **<₩1M per transaction**. Repeated-withdrawal monitoring clause → **no always-on bot pipe** |
| Not possible | mexc · kucoin | Workaround needed (mexc→OKX→bithumb pending) |
| **Unregistered (blocked), 41 venues** | BingX (added 2026-01-12) · BitMart · WEEX · Blofin · CoinW … | Registration not possible, **no re-investigation** |

Upbit is clearer, thanks to Gate's account-holder verification link.

## Bithumb chains
- USDT accepted via: **ETH · TRX · KAIA · APT** (2026-08-08). Withdrawal only via TRX·ETH (observed 08-02)
- Lowest fee to Korea = **KAIA 0.02** (TRX 1.5)
- Withdrawal fee: flat-rate 1% for 254 tickers / fixed fee for 14 tickers / BTT-TRX·TT = 0. **⚠️ The 1% assumption dominates hub screening — if measured values for 39 tickers (Robin action) come back lower, the DROP verdict flips**

## Upbit (2026-09-06)
- Whitelist: **320 pairs**. 259 ETH-chain pairs are opened by policy `rule:chain_policy_mode=fee_known_and_hedged` (fee confirmed by measurement + entry threshold included + hedge certain). `rule:chain_fee_max_usd` default 3
- Hardcoded `FORBIDDEN_CHAINS` retired → replaced by KG policy
- Upbit→gate registered pairs: 14 (ARB·TRX chains, incl. usdt/trx). No issue on Upbit's side — **the bottleneck is our sell-venue list (gateio not allowed)** → opening in progress

## Evaluation unit = (exchange × ticker) pair (Robin correction, 2026-08-05)
Exchange-level adopt/reject is retired. **A**=comparison group + execution / **B**=comparison group only, execution banned (price signal only) / **C**=observe / **X**=excluded. Inclusion procedure = data ingestion (since pair_gate auto-blocks on `unknown_support`, **the data itself is the review**). The exchange rail tier is one field of the pair grade. → [[counterparty-grades]]

## Fact-check trap
Bithumb's official page returns bot 403 → read it via the jina.ai proxy.

## Atoms
- [[../atoms/travel-rule-korea/01-bithumb-connection-free]] — Bithumb free transfer, 10 venues — one-time registration per exchange
- [[../atoms/travel-rule-korea/02-bithumb-connection-midtier]] — Bithumb mid tier Gate — after pre-registration, <₩1M per transaction, no always-on bot
- [[../atoms/travel-rule-korea/03-bithumb-connection-impossible]] — Bithumb not possible — mexc·kucoin need a workaround
- [[../atoms/travel-rule-korea/04-bithumb-connection-blocked41]] — Unregistered (blocked), 41 venues — registration not possible, no re-investigation
- [[../atoms/travel-rule-korea/05-upbit-gate-clearer]] — Upbit is clearer, thanks to Gate's account-holder verification link
- [[../atoms/travel-rule-korea/06-bithumb-usdt-chains]] — Bithumb USDT-accepted chains: ETH·TRX·KAIA·APT; withdrawal only via TRX·ETH
- [[../atoms/travel-rule-korea/07-bithumb-lowest-fee-chain]] — Lowest fee to Korea = KAIA 0.02 (TRX 1.5)
- [[../atoms/travel-rule-korea/08-bithumb-withdraw-fee-structure]] — Bithumb withdrawal fees — flat-rate 1% for 254 tickers · fixed for 14 · 0 (BTT-TRX·TT), 39 tickers pending measurement
- [[../atoms/travel-rule-korea/09-upbit-whitelist]] — Upbit whitelist, 320 pairs; 259 ETH-chain pairs opened by policy
- [[../atoms/travel-rule-korea/10-upbit-hardcode-deprecated]] — Hardcoded FORBIDDEN_CHAINS retired → replaced by KG policy
- [[../atoms/travel-rule-korea/11-upbit-gate-pairs]] — Upbit→gate registered pairs: 14; bottleneck is the sell-venue list
- [[../atoms/travel-rule-korea/12-pair-grade-unit]] — Evaluation unit = (exchange × ticker) pair — A/B/C/X grades
- [[../atoms/travel-rule-korea/13-bithumb-fact-check-trap]] — Bithumb's official page returns bot 403 — read via jina.ai proxy
