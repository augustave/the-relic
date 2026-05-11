# Vocabulary Governance

**Phase II spec. Speculative pre-work. Mitigates R-001 (vocabulary drift).**

The concept vocabulary is the load-bearing structure of every relic. If concepts can rename, merge, or disappear without controls, every prior bridge silently breaks. This document is the contract that prevents that.

---

## Principles

1. **Keys are immutable, labels are mutable.** A concept's internal `key` (e.g., `OOD`) never changes. Its `label` (e.g., "OODA Loop") can evolve via aliases.
2. **The registry is append-only.** Concepts and their aliases are never deleted, only deprecated.
3. **Listener relics see era-appropriate labels.** A listener whose `heard_n` is 12 sees the label that was effective at episode 12, not today's label.
4. **Deprecation is a graph operation, not a delete.** A deprecated concept points to its successor; old bonds still resolve through the deprecation chain.
5. **The host is the sole vocabulary editor.** Listeners never modify the vocabulary; their relic state is independent.

---

## The lifecycle of a concept

```
draft ──► published ──► (optional) deprecated ──► (terminal) deprecated_replaced_by(X)
                  │
                  └──► (label changes via append-only concept_aliases)
```

### draft
- Created by the host while authoring an upcoming episode.
- Not yet referenced in any published bond.
- Can be freely edited or destroyed (key + label).

### published
- Locked into a published Episode's `anchors` or `bridges`.
- `key` is now immutable.
- `label` can change only by appending a new `ConceptAlias`.

### deprecated
- Marked obsolete. Still referenced by historical bonds.
- May (optionally) point to a successor concept via `deprecated_in_favor_of`.
- New episodes should not anchor or bridge to deprecated concepts.

---

## Rename procedure

When the host wants to relabel a published concept:

1. Choose effective episode `N` (must be ≥ next unpublished episode number).
2. Append a `ConceptAlias` row:
   ```yaml
   concept_id: <concept>
   label: "New Label"
   effective_from_episode_n: N
   effective_through_episode_n: null
   ```
3. Update the prior current alias's `effective_through_episode_n` to `N-1`.
4. Update `concepts.current_label` and increment `concepts.label_version`.

Listener relics built before `N` continue to render the prior label until the listener syncs past `N`. Listener-facing UI shows a small "renamed" affordance at the moment of cross-over.

---

## Deprecation procedure

When the host wants to retire a concept (e.g., decides "Network Effects" was never useful and should fold into "Cold Start Problem"):

1. Set `concepts.deprecated = true`.
2. (Optional) set `deprecated_in_favor_of = <successor_id>`.
3. Future episodes cannot bond to this concept.
4. Existing bonds remain. Relics rendering historical episodes still see this concept.
5. Listener-facing UI shows deprecated concepts in a muted style with a "→ <successor>" hint.

**Never delete a concept that has any bond.** The skill's "Evidence is Currency" applies — the historical evidence trail is the value.

---

## Merge procedure (advanced; deferred to post-v1)

Merging two concepts into one is a multi-step operation:

1. Deprecate `Concept A` in favor of `Concept B`.
2. Optionally append a `ConceptAlias` to `B` covering the period A was active.
3. For relic rendering: any bond to `A` resolves transitively to `B` if the user has synced past the merge episode.

Merges are destructive to the historical reading of the corpus and require host justification logged in `governance-evidence-vault.yaml`.

---

## Key naming convention

Keys are:
- 3 letters, SHOUTCASE (e.g., `OOD`, `SCA`, `R37`)
- ASCII only
- Show-scoped (two shows can both have `OOD` meaning different things in v1)
- Chosen at draft time; immutable at publish
- Should be mnemonic to the host, not the listener (listeners see labels, not keys)

Reserved prefixes: none in v1.

---

## What the listener experiences

| Host action | Listener sees |
|---|---|
| New concept introduced in ep N | New ballpoint doodle appears when listener reaches ep N |
| Concept renamed effective ep N | Old label until listener syncs past N; then label flips with a brief "renamed" annotation |
| Concept deprecated | Concept fades to muted; still visible in their historical relic |
| Concept merged into another (post-v1) | Bond visually re-routes after sync |

---

## Governance audit trail

Every vocabulary operation appends to `governance-evidence-vault.yaml`:

```yaml
- timestamp: 2026-04-21T15:00:00Z
  actor: host:augustave
  action: rename
  concept_key: OOD
  prior_label: "OODA"
  new_label: "OODA Loop"
  effective_from_episode_n: 6
  rationale: "Listeners in interviews kept saying 'OODA Loop' — match the speech."
```

No vocabulary operation is performed without a rationale entry. This is non-negotiable per the skill's governance principle.

---

## Failure modes

| Mode | Signal | Recovery |
|---|---|---|
| Host renames carelessly | Listeners report "I don't recognize this concept anymore" | Enforce 24hr cooling-off + require rationale before commit |
| Vocabulary inflation | >100 concepts and listeners can't navigate | Quarterly deprecation pass; merge near-duplicates |
| Cross-show drift | Same key means different things across shows | Accept in v1 (scoped per show); revisit if federation matters |
| Listener relic breaks on sync | Bonds to deleted concepts | Soft-delete only; deletes are bugs |

---

## Open questions

- Should listeners be able to "pin" their relic to a vocabulary snapshot and never sync changes? (Preserves their reading; complicates UX.)
- Is there a max-vocabulary-size signal we should expose to hosts? ("You have 47 concepts; the median show has 32.")
- Should rename rationales be public (transparency) or private (host comfort)?
