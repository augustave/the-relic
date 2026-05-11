# Phase I Interview Script — Listener Pain Discovery

**Format:** 30 min, semi-structured, recorded with consent. Mom Test rules — past behavior, not future intent. Pitch nothing.

**Target cohort:** 5 interviews.
- 3 from founder's personal network (bias acknowledged; will discount confidence accordingly)
- 2 cold-sourced (Reddit r/podcasts, PodcastNotes Discord, Twitter mutuals of host candidates)

**Screening criteria:** Listens to ≥5 hrs/week of long-form ideas-driven podcasts. Names specific shows.

---

## Questions (in order)

**Q1.** Walk me through the last podcast episode you listened to. When was it? What was it about?

**Q2.** Three weeks from now — without going back to look — what do you think you'll remember about it?

**Q3.** Show me anything you've ever saved or noted from a podcast. Apple Notes, Readwise, screenshots, Twitter bookmarks, whatever exists.

**Q4.** Has there ever been a moment you wanted to revisit a podcast episode and either couldn't find it or gave up? Walk me through that.

**Q5.** Are there podcasts where you feel like episodes are building up to something — that the show as a whole is more than its parts? Which ones? What does "building up" mean to you in that case?

**Q6.** Do you follow shows by individual episode, or as a continuous body of work? Why?

**Q7.** If a show you loved produced a "thing" — a document, a webpage, a physical artifact — that grew with each episode you listened to, would you use it? When? How often? What would make you stop?

**Q8.** What's the most you've ever paid for podcast-adjacent products? Plus tiers, Patreon, Supercast, merch, books by the host. What did you get out of it?

---

## Listening guide

### Signal (write these down verbatim)

- Unprompted pain ("I forget everything," "I can't find that one episode where...") before Q4
- Existing workaround behavior (they actually screenshot, note, or share clips)
- Prior paid relationships with creators (predicts willingness-to-pay)
- Emotional intensity — frustration, longing, recurring complaint
- Phrasing the founder didn't seed (their own words for the pain)

### Noise (discount these)

- Polite enthusiasm about the idea ("That's cool!" — useless without past behavior)
- Hypothetical future use ("I would totally use that" — also useless)
- Feature requests ("It should have AI summaries" — not pain, it's design)
- Validation of the founder's hypothesis (treat with suspicion)

---

## Synthesis protocol

After each interview:
1. 30 min within 24 hrs: write 5-bullet summary into `docs/01-interviews/[N]-[firstname]-[date].md`
2. Mark each bullet as: `primary-pain`, `workaround`, `willingness-to-pay`, `disconfirming`, `noise`

After all 5 interviews:
3. Cross-interview synthesis (1 hr): pain confirmation matrix in `docs/01-pain-matrix.md` — rows = candidate pain statements, columns = interviewees, cells = direct quote or N/A
4. Finalize `docs/01-market-requirement.yaml` with evidence trail

---

## Pre-flight checklist

- [ ] Recorder + consent script ready
- [ ] Screening criteria confirmed for each interviewee
- [ ] No mention of "The Relic," knowledge graph, emergent bridges, or any solution language during interview
- [ ] 5 minutes pre-call: re-read this script, mute the urge to pitch

---

## What happens if Phase I fails

**Fail condition:** Fewer than 2 of 5 interviewees express the core pain unprompted, OR the workaround behavior question (Q3) returns nothing across the cohort.

**Recovery:** Do not advance to Phase II. Either:
- Re-scope the user segment (e.g., "newsletter readers who also podcast-listen") and rerun, OR
- Acknowledge the thesis is unvalidated; pivot or stop.

This is the most important gate. Do not rationalize past it.
