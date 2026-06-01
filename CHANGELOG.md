# Changelog

Product decisions across versions — what changed, and why.

---

## V3 — May 2026 (current)

**Theme: Make it feel worth taking seriously.**

The game logic was validated in V2 sessions. The problem was perception: players treated it like a rough prototype, which lowered their investment in the exercise. A workshop tool that doesn't feel deliberate doesn't get deliberate answers.

### Typography — complete replacement

V1 used `system-ui, -apple-system, Segoe UI, Roboto` — whatever the OS provides. No typographic identity.

Current version uses a deliberate three-font constructivist pairing:
- **Big Shoulders Display (800–900 weight)** for all headings — condensed, industrial, high contrast
- **Archivo** for body text — clean grotesque, readable at small sizes
- **JetBrains Mono** for all UI labels, buttons, metadata, and credits — signals technical precision

Every button label, field label, and navigation element is monospaced and uppercase. That's a consistent typographic voice, not a default.

### Color system — inverted and purposeful

V1: white card on light blue-grey gradient, `#0b66ff` blue accent. Generic SaaS palette.

Current: `#E0E0D0` warm khaki background, `#333333` near-black ink, `#DFFF00` neon yellow-green as the sole accent. Zero blue anywhere. The neon appears only on primary buttons and one geometric header element. That restraint makes it read as a signal, not decoration.

### Background texture — layered

V1: flat gradient.

Current: two pseudo-elements stacked on the fixed background — a 28px hairline grid (`rgba(51,51,51,0.10)`) and a 3px dot matrix at 4% opacity with `mix-blend-mode: multiply`. Neither is perceptible individually. Together they read as aged technical paper. Invisible to most users consciously, but the whole thing feels materially different from a browser app.

### Buttons — constructivist offset shadow

V1: `border-radius: 8px`, white background, standard hover.

Current: zero border-radius throughout. Primary buttons use a `4px 4px 0 var(--ink)` hard offset shadow — the constructivist/risograph print effect. On hover, the button lifts (`translateY(-2px)`, shadow grows to 6px). On click, it presses down (`translate(2px,2px)`, shadow collapses to zero). That's a physical press mechanic, not a color change.

### Header — redesigned as a navigation instrument

V1: centered `<h1>` with the app name in blue. Static.

Current: sticky three-column grid — geometric bookend shapes (neon square, outlined circle, triangle) on the left; monospaced brand identifier in the center; tiny monospaced metadata on the right (`INICIO · EAFIT · MMXXV`). Reads like a technical instrument panel, consistent with the sonar metaphor.

### Home screen — animated radar scope

V1: centered tagline, a button, credits. Static.

Current: animated radar sweep — rotating phosphor line, blips that ping and decay, telemetry readouts (`Range 3.2 km`, `Depth −120 m`, `Azimuth 274°`, `Speed 12 kn`, `Bearing N 34° W`). These do nothing functionally. They're world-building. Someone landing on V1 sees a form. Someone landing on current sees a world.

### Screen transitions — animated

V1: `display: none` / `display: block`. Instant.

Current: `@keyframes screenIn` — `opacity: 0 → 1` with `translateY(8px → 0)` over 360ms. Subtle, but navigation feels intentional rather than instantaneous.

### Card imagery — custom assets replacing emoji

V1: `?` and `!` emoji inside styled divs.

Current: `Pregunta.png`, `Caracteristica.png` for Phase 1 decks; `Submarine.png`, `Torpedo.png` for Phase 2. The submarine/torpedo pair extends the sonar metaphor into the mechanics — findings are torpedoes, Phase 2 is target acquisition.

### Close button — redesigned as an action

V1: small `×` text button, barely visible.

Current: fixed 38×38px, monospaced font, hard border. On hover: background becomes danger red, icon rotates 90°, border changes color. A deliberate exit action with real visual feedback.

### PostHog instrumentation

Added three tracked events: `phase_1_started` (players_count, org_type), `phase_2_started` (findings_count), `results_reached` (winners_count).

**Why:** No data existed on whether sessions were completing. The hypothesis was that drop-off was happening between Phase 1 and Phase 2. These events create the minimal funnel to test that without collecting personal data.

### Confirm-exit modal

**Why:** Facilitators were accidentally navigating away during Phase 2 and losing all findings. One click in a rare scenario prevents a session-ending error.

### VRIO warning on results screen

**Why:** Without it, teams were treating high-scoring findings as confirmed strategic assets. The game surfaces candidates, not conclusions.

### Print-ready results

**Why:** Facilitators need a physical artifact. Screenshotting loses the Winner/Qualifier table structure.

### Responsive layout

Three-column stages reflow to two-column on tablet, single-column on mobile.

**Why:** Some sessions happen on personal laptops; a few on tablets. The original layout required horizontal scrolling below 1100px.

---

## V2 — Late 2025

**Theme: Fix the flow. Don't touch the design.**

V1 was played in a first real session. The game logic worked. The interface didn't guide players through it.

Problems observed:
- Players didn't understand the Recurso/Capacidad distinction until mid-game
- The Phase 1 → Phase 2 transition was ambiguous — no clear signal that exploration was done
- No per-turn guidance on how to articulate a finding
- All buttons were visible simultaneously; players didn't know which one was "next"

**What changed:**

**Progressive disclosure.** Buttons became disabled until the prior step completed. The sequence — select cards → write finding → answer Yes/No → next turn — is now enforced by the interface, not instructions text. You can't use it out of order.

**Inline guidance.** A guidance strip appeared below the writing area: "Resource — start with a noun · Capability — start with an infinitive verb." Visible during every turn, not buried in a README.

**Type detection badge.** After submitting a finding, a badge flashes briefly: "Tipo detectado: Recurso" or "Tipo detectado: Capacidad." Makes the classification transparent and teaches the distinction through repetition rather than explanation.

**Progress pips.** Ten pip indicators below the writing area track how many findings have been logged. Players know where they are in Phase 1 without counting.

**Phase 2 gate.** "Go to Phase 2" button only appeared after a minimum finding count. Previously it was always visible, and sessions were ending Phase 1 early.

**Design unchanged.** V2 kept the blue-card system-font aesthetic from V1. The decision was to validate game logic and flow before investing in visual design.

---

## V1 — November 2025

**Theme: Does the concept work at all?**

First playable version. Built for a single session at EAFIT's strategy research seminar.

- Two-phase structure: individual exploration + collective voting
- Question deck (40 cards across 5 categories: tacit knowledge, informal networks, collective routines, intuition/decision-making, vulnerabilities/resilience)
- Feature deck (40 cards across 5 VRIO-adjacent categories)
- ★ Star deck (10 W&Q criteria questions)
- Scoring: Capacity = 5pts, Resource = 3pts, +1 if feature criterion met in Phase 1; Phase 2 vote nullifies (0pts) or confirms (keeps F1 score)
- Tie-break favors Sí — explicit design choice: in a discovery exercise, suppressing a finding is a worse error than including a weak one

**What V1 confirmed:** The two-phase structure worked. Players engaged with the question prompts. The vote mechanic created genuine debate. The type detection heuristic (infinitive verb = capacity) was imperfect but sufficient.

**What V1 didn't solve:** Visual design communicated "rough prototype," which affected participant engagement. Instructions were unclear enough that a facilitator had to intervene during Phase 1.
