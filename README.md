# THE RELIC

> A podcast that dissolves into a knowledge object.

**Live:** [augustave.github.io/the-relic](https://augustave.github.io/the-relic/)

Every episode deposits a fragment. Fragments dock on shared concepts. Enough fragments in, and the episodes stop being the point — the structure they were always assembling becomes the artifact. The podcast recedes into scaffolding; the relic remains.

---

## The frame

Most shows produce a feed — a stack of discrete, timestamped files. The relic inverts that. Each episode is built to produce **one piece of a larger object that nobody designed in advance.** Over a season, the pieces auto-dock through a shared vocabulary of concepts. Past a threshold, a **second-order structure** emerges: concepts that repeatedly co-occurred across episodes quietly form bonds the podcast itself never explicitly stated. Those bonds are the knowledge.

The point is not to visualize episode content. The point is to build a structure that outlives the listening.

---

## What's in this repo

| File | Role |
|---|---|
| `index.html` | The Relic — the primary artifact. Single-file HTML, no build, no deps. |
| `atlas.html` | Early prototype — a 4-phase ambient backdrop loop. Kept as a visual reference point. |

Both are self-contained pages. Open in any modern browser.

---

## How the Relic works

### Two modes

**Personal** — your copy. A slider reveals episodes ≤ N. Unheard concepts appear as dashed ghosts: silhouettes of docking points waiting for episodes you haven't heard yet. Your relic is a record of your own progression.

**Canonical** — the full cumulative state across all episodes. The shared, authoritative relic.

### The three kinds of structure

1. **Episode tiles** — rubber-stamped hexagonal blocks, one per episode. Each declares its **anchors** (concepts it introduces) and **bridges** (concepts it inherits from prior episodes).
2. **Concept nodes** — ballpoint-pen circles, typewriter labels. Size scales with how many episodes have touched them.
3. **Emergent bridges** — mustard-highlighted concepts that have appeared in ≥3 episodes. These are the load-bearing members of the relic. The ticker announces each one the moment it forms.

### The dissolve

Press **"Dissolve the Podcast"** and the episode tiles fade into the paper. In their place, a new layer rises: concept-to-concept **co-occurrence edges** — every pair of concepts that appeared together in ≥2 heard episodes draws a rust-ink bond, thicker for more co-occurrences. This is the knowledge graph the podcast implied but never stated. The dissolve is the payoff: the episodes were always scaffolding for this.

### Export

Export your personal relic as JSON — a portable specimen containing the episodes you've heard, every concept you've touched, and the emergent bridges your listening has forged. Intended to be shared, remixed, or fed into downstream tooling.

---

## The art direction

Designed as a **flatbed-scanned zine collage**: yellowed ledger paper with faint blue rule lines, SVG-turbulence grain, edge vignette, coffee-ring stains, transparent tape strips. Episode tiles are rust-red rubber stamps with off-register CMYK smears. Concepts are navy ballpoint doodles with dusty typewriter labels. Emergent bridges get a neon mustard highlighter slab. Engraved eagle, Americana shield, "SPECIMEN № 001" oval, "NOT FOR CIRCULATION" classified mark.

Aesthetic references: 1990s DIY punk zine ephemera, FBI case files, Risograph prints, USGS field reports.

**Type stack:** IM Fell English SC (engraved headlines), Special Elite (typewriter body), Courier Prime (system text).

---

## Authoring an episode

Episodes are hand-authored for now — each one a declaration of its conceptual footprint. Add to `EPISODES` / `MANUAL` in `index.html`:

```js
{
  n: 6,
  title: "Command at the Speed of Intuition",
  blurb: "What System 1 knows before System 2 wakes up.",
  anchors: ["HEU", "S1", "S2"],        // concepts this episode introduces
  bridges: ["OOD", "ORI", "FTR"]        // concepts inherited from prior episodes
}
```

A new concept that hasn't appeared before needs to be added to the `CONCEPTS` vocabulary:

```js
const CONCEPTS = {
  ...
  HEU: "Cognitive Heuristics",
  ...
};
```

### Authoring rules of thumb

- **Anchors are scarce.** Each episode should introduce at most 3–5 genuinely new concepts. More than that and nothing compounds.
- **Bridges are the point.** Every episode past ep 1 should declare at least 2 bridges. Bridges are what make the relic one thing rather than 50 things.
- **Name the glyph, not the take.** Concepts should be durable, re-usable ideas (*"Fast Transients"*) not episode-specific claims (*"Why Boyd was right about the F-15"*).
- **Aim for emergent bridges.** The moment of magic is when a concept crosses the 3-episode threshold. Author with that payoff in mind.

---

## Technical architecture

Single-file HTML, Canvas 2D, no frameworks, no build step.

- **Graph:** nodes are `episode` or `concept`. Edges are `episode → concept` labeled `anchor` or `bridge`.
- **Layout:** force-directed — centering gravity + kind-weighted repulsion + spring attraction along edges. Concepts with high degree naturally pull their episodes into clusters.
- **Visibility:** `episodeVisible(n)` returns true if mode is canonical or n ≤ heardN. Concepts are alive if they touch any visible episode.
- **Emergent bridges:** computed each frame. A concept becomes a bridge when `heardCount >= 3`.
- **Dissolve mode:** animates a `reveal` float from 0 → 1. Episode layer fades; concept co-occurrence edges fade in. Co-occurrence is recomputed from visible episodes each frame.
- **Rendering quirks:**
  - Off-register CMYK smears on stamps (3 offset draws in cyan/yellow/rust)
  - Ballpoint wobble: edges drawn as segmented lines with trig-noise perpendicular offset
  - Deterministic per-node rotation and specks via FNV-1a hash seeded on node id
  - Mustard highlighter slabs drawn behind bridge labels, rotated

---

## Roadmap

Near-term:
- [ ] Real episode authoring drawer (add/edit without touching source)
- [ ] Shareable URL hash state (`#heardN=25&mode=canonical&reveal=1`)
- [ ] Threshold-triggered auto-crystallization (dissolve animates in when N bridges exist)
- [ ] "Seam view" — highlight the episodes that contributed the most load-bearing bridges
- [ ] Import a personal relic JSON

Medium-term:
- [ ] Printable PDF field-report export, styled as the zine
- [ ] Per-episode printable card (letter-pressed rubber-stamp tile with concept list)
- [ ] Audio hook: scrub the relic and the playhead moves through episode timestamps

Speculative:
- [ ] Inter-relic docking — two listeners' personal relics can overlay and show their intersection
- [ ] Query mode: click a concept pair and the relic surfaces the episodes that forged their link

---

## Provenance

Built in a conversation between `@taoconrad` and Claude Sonnet 4.6 on 2026-04-20/21 as a design exploration for a podcast about 20 books on complexity, wartime operations, deep tech, and cognition. The concept vocabulary is seeded from that booklist but intentionally decoupled from it — the relic is designed to hold any domain whose episodes commit to a durable shared glyph set.

## License

MIT.
