# Winners & Qualifiers

**A browser-based facilitation game that helps organizational teams surface tacit resources and capabilities — built, iterated, and instrumented by a PM.**

[**→ Play it live**](https://winners-and-qualifiers.vercel.app) · [**→ Read the case study**](docs/case-study.md) · Universidad EAFIT · Strategy Research Lab · 2025

---

## What this is

Most organizations have strategic assets they can't see — the informal network that unblocks deals, the unwritten process that never fails, the tacit know-how that walks out the door when someone leaves. Winners & Qualifiers makes those visible.

It's a structured two-phase workshop game for 3–10 players:

- **Phase 1 — Exploration:** Each player draws a question card + feature card, articulates a *finding* (a resource or capability they've observed), and answers whether it meets the feature criterion. A 5-minute timer creates productive pressure.
- **Phase 2 — Classification:** All findings go into a deck. Players draw a W&Q ★ criterion card and vote democratically on whether each finding is a **Winner** (strategically differentiating) or a **Qualifier** (valuable but not rare). Tie-breaks favor Yes — because false negatives cost more than false positives.
- **Results:** A ranked podium, split Winner/Qualifier tables, and a VRIO warning reminding teams this is a starting point, not a diagnosis.

The question, feature, and ★ criterion decks are grounded in organizational strategy theory (resource-based view, VRIO framework, tacit knowledge literature).

---

## Why this repo exists

This is a product portfolio artifact. The goal was to demonstrate PM thinking by shipping something real:

- Shipped to a real audience (EAFIT strategy research seminar)
- Iterated from V1 prototype to current version based on observed friction
- Instrumented with PostHog to measure what actually happens in sessions
- Deliberate design decisions documented — not just "it works"

The [case study](docs/case-study.md) walks through all of it: the problem, hypotheses, decisions made and why, what changed across versions, what's measured and why, and what's next.

---

## Tech

Single-file HTML/CSS/JS — no build step, no dependencies, no backend. Deploys to Vercel from `main`. This was a deliberate constraint: the tool needs to run on any device in a classroom without install friction.

**Instrumentation:** PostHog (EU cluster) captures three events — `phase_1_started`, `phase_2_started`, and `results_reached` — with context on player count, org type, finding count, and winner count. Enough to measure funnel drop-off and session completion without collecting personal data.

---

## Status

Active. V3 shipped May 2026. Roadmap in the [case study](docs/case-study.md#roadmap).

**Built by:** [Paul Moscoso V.](https://www.linkedin.com/in/paulmoscosov)
**Research leads:** Martha Reyes Sarmiento · John Macías · Jorge Iván Vélez Castiblanco
