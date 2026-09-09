# Atomization Spec — 1 fact = 1 note

> Purpose: break compressed notes (10–25 facts per file) into **atom notes** so the graph exposes the structure of the knowledge.
> Atom = the smallest unit of knowledge an external Obsidian user sees, and the unit that carries contributor credit and sourcing.

## Absolute rules
1. **Don't invent.** Every sentence in an atom must come only from sentences, numbers, or quotes already present in the hub note (the existing facts/rails/maps file). No adding summaries, interpretations, or inferences. Don't change a single digit.
2. **Don't delete or move hub notes.** Existing links would break. Add a `## Atoms` section at the end of the hub file and only link out to the atoms from there.
3. **One atom = one verifiable claim** (+ its evidence/source). "A and B" is two atoms.
4. **A claim carrying `unverified` in the atom inherits `status: unverified`** unchanged.
5. No secrets (keys, balances, personal wallet addresses) — if it's not in the hub, it doesn't go in the atom either.

## Location and naming
```
<playbook>/atoms/<hub-slug>/NN-<english-slug>.md      NN = starting at 01, in order of appearance within the hub
```
Example: `hyperliquid/atoms/account-modes/03-unified-account-shares-margin.md`

## Atom file format
```markdown
---
id: <playbook>.atom.<hub-slug>.NN
title: <one-sentence claim — Korean, ~40 characters>
status: verified | unverified
as_of: <the hub's as_of, or the measurement date of this specific item>
hub: "[[../../facts/<hub-slug>]]"            # relative path. For rails/maps, use that path
source: "<one piece of evidence for this claim from the hub's sources, or the original quote>"
tags: [<1-3 relevant tags from the hub's tags>]
contributors: [house]
---

# <same as title>

<the claim, 1-3 sentences — verbatim from the hub or minimally edited. Preserve quotes as > blocks.>

**Evidence**: <measured value, quote, or table row — verbatim>

Related: [[<relative path to the gate file that uses this fact>]] · [[<source-material filename>]] · [[<memory filename>]]
```

## Linking rules (the key to graph density)
- **To gates**: a gate that cites this hub in its `source`, or a gate the hub body points to via `→ [[../gates/...]]` → link it from the atom's `Related:` as a relative path.
- **To source material**: link documents named in the hub's `sources`/`origin` **by filename only** (`[[HL_FACT_MAP]]`, `[[PATH_INTELLIGENCE]]`, `[[2026-09-07-multix-round-l]]`). In a playbooks-only vault these are unresolved links (hidden); in the wiki vault they resolve.
- **To memory**: if a memory name appears in the hub's sources, link it by filename (`[[project_transfer_intelligence]]`).
- **Between atoms**: the preceding/following atom in the same hub, or a directly related atom in another hub → `[[../<hub-slug>/NN-...]]`. Don't force a connection — only when the bodies actually reference each other.
- Don't touch gate files (one-directional: atom → gate). `gates/index.md` is left as-is.

## Hub note update (the only edit allowed)
Append to the **very end** of the hub file:
```markdown

## Atoms
- [[../atoms/<hub-slug>/01-...]] — <title>
- ...
```
(adjust path depth for `maps/`/`rails/` hubs)

## Size expectations
| Playbook | Hub count | Expected atoms |
|---|---|---|
| hyperliquid | facts 9 + rails 2 | 100–120 |
| rails | facts 5 + maps 1 | 80–100 |
| fund | core facts 3 + arb facts 3 + carry facts 1 + dated README body | 90–120 |

## Completion criteria
- Every hub has a `## Atoms` section; every atom has all 8 frontmatter fields
- Link integrity: all relative links within playbooks resolve (source-material and memory filename links are the exception)
- Zero numbers or claims in atom bodies that aren't in the hub (spot-check: cross-check 10 random atoms)
