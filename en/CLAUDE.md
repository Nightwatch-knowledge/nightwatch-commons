# playbooks/ — AI Operating Manual (CLAUDE.md)

> This repository is the NightWatch Knowledge Commons (public tier) — it contains only market-structure knowledge. Gates, deep lessons, and fund internals are pro / internal tier. Humans read it too, but the primary reader is AI.
> Structure: **raw (source material) → wiki (this folder) → INDEX (table of contents) → this file (how to use it)**.
> If this is your first time, read in this order: this file → [[INDEX]] → the relevant playbook's README → gates.

## 1. What this is

- **Playbook** = a complete bundle of knowledge an AI needs to act in one market (or one engine). One folder = one playbook.
- **File = node, `[[link]]` = edge.** This folder is text and a graph at the same time. Open it in Obsidian and you get the graph view.
- **The canonical source is not here — it's the DB and the ledger.** A playbook is a *curated summary of verified structural knowledge*; live values (prices, fees, gate status, balances) are read via each README's `live_endpoints`. Every figure must carry an `as_of` — judge freshness by the date.

## 2. Folder convention

```
<playbook>/
  README.md      frontmatter(name·slug·version·epoch·tier·curators·coverage_grade·settlement_reality·live_endpoints·origin) + read order
  facts/         Verified facts. Citations, measurements, sources. status: verified | unverified | curated
  rails/         (market playbooks) deposit/withdrawal and API access rails
  maps/          (rail playbooks) route maps — diagrams + corridor tables + machine-readable YAML
  atoms/<hub>/   Atom notes — 1 fact = 1 note (NN-slug.md). Linked from the hub node's trailing `## Atoms`. Convention=[[ATOMIZATION_SPEC]]
  gates/         Machine-readable rules. index.md + gate files
  lessons/       what-generalises.md — lessons that hold outside this market (numbered list)
  rooms/         open-questions.md — open questions = candidate Hive question nodes = contribution points
  changelog.md   Epoch-notation change history (no retroactive restatement)
```
The fund is a family: `fund/README` → `fund/core` (engine-agnostic) + `fund/<engine>/`. Engine playbooks **inherit** `rails`/`hyperliquid` gates rather than duplicating them.

## 3. Frontmatter schema

**Node (facts/rails/maps/lessons/rooms)**
```yaml
id: <playbook>.<kind>.<slug>     # e.g. hl.facts.account-modes
title: ...
status: verified | unverified | curated | open
as_of: YYYY-MM-DD                # date the fact was obtained. Don't trust it if missing
freshness_note: ...              # (optional) which values go stale quickly
sources: [...]                   # endpoints/docs/memory we actually hit. "Memory" is not a source
contributors: [house | <root sbt name>]
tags: [...]
tier_candidate: commons          # (optional) candidate for public release
```
**Gate (gates/*)** — rules loaded before acting. These five fields are machine-readable.
```yaml
gate_id: <playbook>.gate.<slug>
severity: blocking | advisory
when: "when to check"
check: "what to verify"
fail_action: "what to do on failure"
source: "[[supporting node]]"
as_of: YYYY-MM-DD
```

## 4. How an AI uses this folder

1. **Gates before action.** Load the relevant playbook's `gates/index.md`, including inherited gates (fund → rails/hyperliquid), and check everything whose `when` applies. If a `blocking` gate isn't passed, don't act.
2. **When citing a fact, state the node id and as_of together.** "According to hl.facts.account-modes (2026-07-31) …". Cite `unverified` items as hypotheses, not facts.
3. **Re-read numbers live.** Fees and prices in a playbook are snapshots. `get_pair_gate`, `get_quartermaster`, `get_token_intel`, and `nw_kg_facts` hold the current values.
4. **If you don't know, check rooms.** An unanswered question is likely already open in `rooms/open-questions.md` — if it isn't there, it's a candidate to add.
5. **Lessons carry across.** Whatever market you're working in, read `lessons/what-generalises.md` from every playbook. An incident in another market is a gate in this one.

## 5. How to contribute (writing)

- A new fact = a new node file (or a dated entry appended to an existing node). **Don't correct existing numbers** — append a new as_of entry below and record it in the changelog.
- Nodes go through a **submit → verify → load** pipeline. No exception, not even for house agents. Unverified nodes carry `status: unverified`.
- Adding a gate requires a supporting node (`source`) to exist first. Order: incident → fact node → gate.
- When you close an open question, don't delete it from rooms — move it to a "Resolved" section.
- Format: **vanilla Markdown + `[[wikilinks]]` + YAML frontmatter only.** No Dataview, Canvas, or plugin syntax (it breaks outside Obsidian).
- **Never include**: keys, tokens, passwords, wallet private keys, exchange API keys, real balances, personal wallet addresses (even public addresses — point to operational wallets only via the Credentials Index).

## 8. Don'ts (summary)

No retroactive restatement · fabricated figures ("reading absence as measurement") · sourceless facts · bypassing gates · secrets · plugin-only syntax · duplicating another playbook's gates (inherit via link instead).
