# Single-User Commitment — One-Way Door

**Date:** 2026-04-21
**Authority:** Senior agent (per founder delegation)
**Status:** LOCKED. Revisit only after Phase IV gate.

---

## The decision

**The Relic is a listener-consumption artifact.**

The user is a serious podcast listener who follows ideas-driven shows and feels their listening doesn't compound into anything reusable.

## What we are building

A per-listener artifact, tied to a single podcast, that:
- Grows as the listener consumes episodes
- Reveals second-order structure (emergent bridges) the show implies but never states
- Is exportable, portable, ownable

## What we are NOT building (rejected paths)

| Rejected | Reason |
|---|---|
| **Host-authoring SaaS / CMS** | Commodity layer. Host hand-authors via simple files in v1. |
| **Multi-tenant publisher infrastructure** | Platform play, not a product. Wrong shape for solo founder. |
| **Audio playback / podcast app** | Not our business. We sit alongside playback. |
| **LLM-based concept extraction** | Violates narrative truth — auto-extracted concepts can't be trusted as durable. Manual authoring is the moat in v1. |
| **A note-taking app (Readwise/Obsidian competitor)** | Different user behavior. Text-input centric. The relic is passive-accretion centric. |

## Why listener over host

- Per-listener artifact is the **defensible value** — unique, sharable, retentive.
- Host-side tooling can be a thin layer added later; the listener artifact is what makes the show worth more than its feed.
- A great listener product creates demand for great host tooling; the reverse is not true.
- Solo-founder feasible: listener-side is a single artifact + a thin sync layer. Host-side as a product is a 5-person team.

## Implications for every later phase

- **Phase I** interviews are with listeners, not hosts.
- **Phase II** ER schema centers `Listener.PersonalRelic` as the primary entity; `Host.CanonicalRelic` is the upstream source they sync from.
- **Phase III** brand language addresses the listener directly. Host-facing materials are a deferred concern.
- **Phase IV** narrative is "you own the structure of what you've listened to," not "publish a knowledge graph."

## Override conditions

This decision is revisitable only if:
- Phase I evidence shows the listener pain is unfalsifiable or trivial, AND
- Host interviews (out of scope for v1) reveal a stronger pain.

Anything short of that = the decision holds.
