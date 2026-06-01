# Changelog

Product decisions across versions — what changed, and why.

---

## V3 — May 2026 (current)

**Theme: Make it feel worth taking seriously.**

The underlying game logic was validated in V2 sessions. The problem was perception: players treated it like a rough prototype, which lowered their investment in the exercise. A workshop tool that doesn't feel deliberate doesn't get deliberate answers.

### Design system overhaul

Replaced system-font/blue-card aesthetic with a constructivist visual language: Big Shoulders Display for headings, Archivo for body, JetBrains Mono for labels and metadata. Neon (#DFFF00) as the single accent color. Grid texture + dot texture on the background. Zero border-radius on interactive elements.

**Why:** The visual identity needed to signal "this was designed for a purpose" without looking corporate. The constructivist aesthetic — dense, typographic, geometric — communicates rigor while staying distinct from enterprise software.

### Submarine/radar/torpedo metaphor

Home screen replaced with an animated radar scope — concentric rings, a sweeping phosphor effect, neon blips that pulse and decay. Card deck imagery: question cards show a periscope view, feature cards show a sonar characteristic diagram, findings cards show a submarine, ★ criterion cards show a torpedo.

**Why:** The game is about detecting hidden things. The sonar metaphor is accurate: you're scanning an organization for signals that are hard to see directly. It also makes the home screen a conversation piece before the game starts.

### 3D card flip animations

Cards flip on a Y-axis when drawn, revealing content on the back face.

**Why:** Mirrors the physical card game experience that facilitators are already familiar with. The animation creates a moment of attention — players look at what was just revealed rather than skimming past it.

### PostHog instrumentation

Added three tracked events:
- `phase_1_started` — captures `players_count` and `org_type`
- `phase_2_started` — captures `findings_count`
- `results_reached` — captures `winners_count`

**Why:** No data existed on whether sessions were completing. The hypothesis was that drop-off was happening between Phase 1 and Phase 2, possibly due to time pressure or unclear instructions. These events create the minimal funnel needed to test that hypothesis without collecting personal data.

### Confirm-exit modal

Added a modal when users attempt to leave mid-game, warning that all session data will be lost.

**Why:** In early sessions, facilitators accidentally navigated away during Phase 2 and lost all findings. The modal costs one click in a rare-but-not-zero scenario and prevents a session-ending error.

### VRIO warning on results screen

Added a visible callout: "Winners should always be subjected to VRIO analysis to be validated as strategic resources or capabilities."

**Why:** The game surfaces candidates, not conclusions. Without this, teams were treating high-scoring findings as confirmed strategic assets. The warning anchors the correct interpretation.

### Print-ready results

Results screen renders cleanly when printed, hiding navigation and extraneous UI.

**Why:** Facilitators need a physical artifact at the end of the session. The alternative — screenshotting — loses the Winner/Qualifier table structure.

### Responsive layout

Three-column Phase 1 and Phase 2 stages reflow to two-column on tablet and single-column on mobile.

**Why:** Some sessions happen on personal laptops; a few on tablets. The original desktop-only layout required horizontal scrolling below 1100px.

---

## V2 — Late 2025

**Theme: Fix the flow, not the look.**

V1 was played in a first real session. Problems observed:

- Players didn't understand the Recurso/Capacidad distinction until mid-game
- The Phase 1 → Phase 2 transition was ambiguous — no clear signal that exploration was over
- No per-turn guidance on how to articulate a finding

Changes:
- Added inline guidance ("start with a noun for a resource, an infinitive verb for a capability") visible during each turn
- Added automatic type detection with a visible "Tipo detectado" badge that appears briefly after submitting — makes the classification transparent and teaches the distinction through repetition
- Made the "Go to Phase 2" button only appear after a minimum number of findings, removing the ambiguity
- Added progress pips showing how many findings have been logged

**Design unchanged** — V2 kept the blue-card system-font aesthetic from V1. The decision was to validate game logic before investing in design.

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
