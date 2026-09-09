---
id: fund.core.lessons.what-generalises
lang: en
title: What generalises — 10 lessons that carry across engines
status: curated
as_of: 2026-09-12
contributors: [house]
tier_candidate: commons
---

# What generalises (engine-agnostic)

1. **The wallet is the truth, the ledger is the explanation.** When the three numbers (index, ledger, NAV) disagree, the wallet wins. The rest is an explanation attributing that change, and any unexplained residual is stated in one line rather than hidden.
2. **Annualize only a run-rate.** Annualizing a one-time entry fee produces illusions like −112%. State fees in terms of the breakeven *date*, not an annualized rate. (Torii Carry Book)
3. **Positions belong in the ledger, not in memory.** A restart wipes memory. Whether you can resume depends on whether the facts were persisted.
4. **A single ledger writer, and accrual based on settlement boundaries.** Run without these two, even on paper, and you get phantom funding (3 accruals in 19 seconds) and double-counting.
5. **"A gate that can never trigger is indistinguishable from a gate that always passes."** Before you trust a verdict, verify live that each gate has actually both rejected *and* allowed at least once. Case: 8 duplicate mark-price ticks drove stdev to 0, leaving the volatility gate fail-open.
6. **Retirement is an accounting decision, not a filing action.** "Retire the epoch" and "invalidate all records" were a single flag, and the second meaning was never made explicit — so open positions and fees silently vanished. When you discard something, the record must say what was discarded. (MultiX Round L → Fix B)
7. **Don't invent a price that doesn't exist.** The quote at the time of retirement was gone — a fabricated closing price is the defect of "reading absence as measurement." Record the entry fact and the last measured value, then stop.
8. **A test that locks in a false statement keeps that false statement alive.** If a test asserts a narrative, the narrative can't be corrected when it's wrong. A single `replay()` run disproved a statement that four rounds of review had missed — return the book the record actually supports, not the book the prose describes.
9. **A hedge is an attached layer, not a trigger.** Make the hedge a separate engine and the trigger gets duplicated — and the duplicate misses gates. One gap = one trade; "hedged" is an attribute.
10. **One loss is allowed; the same cause twice is not.** Cause → KG fact → T0 gate. For failure to become a curriculum, the plumbing has to exist.
