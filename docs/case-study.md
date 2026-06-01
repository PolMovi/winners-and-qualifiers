# Winners & Qualifiers — PM Case Study

**A browser-based workshop tool that helps organizational teams identify tacit strategic assets.**

[→ Live product](https://winners-and-qualifiers.vercel.app) · [→ Repo](https://github.com/PolMovi/winners-and-qualifiers)

---

## The problem

Organizational strategy theory has known for decades that the most defensible competitive advantages come from resources and capabilities that are hard to see — tacit knowledge, informal networks, unwritten routines, intuitions built over years. These don't show up in org charts or asset registers.

The practical problem: how do you surface these in a room full of people, without it becoming a consultant-led interview exercise that produces a slide deck nobody reads?

The research team at EAFIT's strategy seminar needed a tool that:
1. Works without a consultant in the room
2. Gets to the tacit stuff (not just what people think they *should* say)
3. Creates a real artifact teams walk away with
4. Scales from 3 to 10 players in a classroom setting

---

## Hypothesis

> A card-based game with a structured two-phase flow — individual exploration followed by collective voting — will surface tacit assets more effectively than a guided discussion, because it distributes the discovery burden across all players and uses democratic pressure to separate what's genuinely valued from what's merely volunteered.

Secondary hypothesis: **The game needs to feel like it was designed on purpose.** A rough tool gets rough engagement.

---

## Product decisions

### Two-phase structure

**Phase 1 (Exploration)** is individual and timed. Each player draws one question card and one feature card, then articulates a *finding* — a resource or capability they've observed in the organization. The 5-minute timer is intentional: it prevents overthinking and forces first-instinct answers, which tend to be more tacit.

**Phase 2 (Classification)** is collective. All findings from Phase 1 go into a deck. Players draw a ★ criterion card and vote democratically on whether each finding is a *Winner* (strategically differentiating) or a *Qualifier* (valuable but not rare/inimitable). This separation matters: if players voted on their own findings in real time, social dynamics would anchor the group toward validation.

### The decks

**Question deck (40 cards):** Organized across five categories grounded in tacit knowledge literature — tacit knowledge, informal networks, collective routines, intuition & decision-making, vulnerabilities & resilience. Questions are written in first person and designed to trigger recall ("What trick do you use at work that's not in any manual?") rather than reflection ("What are your core competencies?"). The difference is important: recall surfaces specific, tacit, real things; reflection surfaces things people think sound good.

**Feature deck (40 cards):** Five VRIO-adjacent categories — singularity vs. competition, customer-perceived value, rarity & distinctive origin, difficulty of imitation, organizational capacity to exploit. These are not VRIO checkboxes; they're conversation prompts framed as characteristics ("It would take years or major investment for another organization to build an equivalent").

**★ Star deck (10 cards):** The W&Q criteria. These operationalize "what makes a Winner" without relying on expert judgment. Questions like "Is this difficult to copy or replicate?" and "Does it generate visible value for the customer?" give the voting group a shared anchor. Without this, votes converge on who spoke most convincingly in Phase 1.

### Tie-break favors Yes

When the vote is split, the finding is classified as a Winner.

This was a deliberate design choice. In a discovery exercise, the error cost is asymmetric: suppressing a finding that was actually strategic (false negative) is worse than including a weak one (false positive). The game explicitly produces candidates, not conclusions — the VRIO warning on the results screen handles the interpretation question.

### Type detection (Recurso / Capacidad)

The app automatically classifies each finding as a Resource or a Capability based on the first word: infinitive verbs (ending in -ar/-er/-ir in Spanish) classify as Capability; anything else classifies as Resource. Players see a brief badge confirming the classification after each submission.

**Why keep a heuristic this simple?** Because the classification boundary isn't the point — it's a teaching scaffold. The badge creates a moment where players either confirm or question the classification, which teaches the distinction through repetition. A more sophisticated NLP classifier would remove that moment and add a dependency.

### Scoring

- Capability finding: 5 base points
- Resource finding: 3 base points  
- +1 bonus if Phase 1 feature criterion was met
- Phase 2 vote: confirmed → keeps Phase 1 score; rejected → score becomes 0

The differential (5 vs. 3) reflects that capabilities are generally harder to identify than resources and more valuable for strategy. It also creates an incentive to articulate findings as capabilities, which improves quality over the course of a session.

### No backend, no accounts

All state lives in memory. When the session ends, it's gone. The only data that leaves the device is the three PostHog events (see below).

**Why:** The tool runs in classrooms where network reliability varies and time pressure is real. No login, no sync, no "wait for the server" moments. The constraint forced better design — the confirmation modal before exiting mid-game exists because losing session data is a real and unrecoverable failure.

---

## Design evolution

### V1 — November 2025: Validate the concept

Blue-card, system-font UI. Emoji placeholders for card deck imagery. Desktop-only. No instrumentation. Built to answer one question: does the two-phase structure work?

It did. Players engaged with the prompts. The vote mechanic produced real debate. The type detection heuristic was rough but sufficient.

What it revealed: the UI signaled "rough prototype," which reduced participant investment. The facilitator had to verbally explain Phase 1 instructions multiple times. The Phase 1 → Phase 2 transition was unclear.

### V2 — Late 2025: Fix the flow, don't touch the design

Kept the V1 visual design (blue-card, system fonts). Fixed the interface. The core problem: all buttons were visible simultaneously and players didn't know which one was "next." V2 introduced progressive disclosure — buttons disabled until the prior step completed, making the sequence enforceable by the UI rather than instructions text.

Also added: inline per-turn guidance ("resource → noun, capability → infinitive verb"), an automatic type detection badge that flashes briefly after each submission, progress pips tracking how many findings have been logged, and a Phase 2 gate so sessions couldn't leave Phase 1 prematurely.

Decision rationale: validate game logic and flow before investing in visual design.

### V3 — May 2026: Make it feel worth taking seriously

The game worked. The tool didn't feel like it deserved the serious organizational context it was being used in.

Complete visual overhaul. Three-font constructivist system: Big Shoulders Display for headings, Archivo for body, JetBrains Mono for every label, button, and metadata element. Neon (#DFFF00) as the sole accent — used only on primary buttons and one geometric header element, nowhere else. Warm khaki background (#E0E0D0) with a layered grid + dot texture that reads as aged technical paper. Zero border-radius throughout. Primary buttons use a hard 4px offset shadow that physically presses on click.

Home screen replaced with an animated radar scope: rotating phosphor sweep, blips that ping and decay, telemetry readouts (Range, Depth, Azimuth, Speed, Bearing). All fake, all world-building. Phase 2 card decks rethemedas submarine/torpedo — findings are torpedoes, Phase 2 is target acquisition.

Functional additions: confirm-exit modal, responsive layout, print-ready results, PostHog instrumentation, screen entrance animations.

---

## What's instrumented and why

PostHog EU captures three events per session:

| Event | Properties | What it answers |
|---|---|---|
| `phase_1_started` | `players_count`, `org_type` | Are sessions being started? What's the typical group size? |
| `phase_2_started` | `findings_count` | Are sessions completing Phase 1? What's the average finding yield? |
| `results_reached` | `winners_count` | Are sessions completing end-to-end? What's the Winner rate? |

**The gap I'm watching:** the drop between `phase_1_started` and `phase_2_started`. The hypothesis is that some sessions stall in Phase 1 — players lose steam before reaching the 10-finding cap, or facilitators skip Phase 2. If that's confirmed, the intervention would be lowering the minimum findings required to unlock Phase 2, or making the transition more explicit.

**What I'm not tracking:** player names, finding text, organization name, votes. The tool explicitly tells players "data is not transmitted or stored" — I'm not going to make that a lie for analytics I don't need.

---

## Roadmap

These are prioritized by impact on the core hypothesis, not by implementation ease.

### P0 — In-game narrator (spy character)

The current mental model problem: players believe they should answer the question card directly in the writing box. They read the question, they answer it. Wrong — the question is a conversation prompt; the writing box is for the *finding* that emerges from the conversation. The distinction between "answering a question" and "surfacing what the debate reveals about your organization" is the entire conceptual unlock for Phase 1.

The instructions exist in multiple places — guidance strip, phase header, screen instruction text. Players don't read them under social pressure in a group setting. This is not a bug.

**The solution:** a contextually aware in-game narrator consistent with the strategic intelligence aesthetic. When Phase 1 loads, a brief entry animation plays — the spy appears and explains the sequence while the relevant UI elements are highlighted in turn. Not a tutorial modal. A character who lives in the world of the game explaining the rules the way a game master would. Reference points: Bastion (narrator reacts to what you do), Portal (the world teaches you, not a help menu). A skip button exists for returning players.

After the entry animation, the spy collapses to a small icon in the bottom-left corner. Clicking it at any moment triggers a contextually aware response — not generic help text, but a read of the current app state: which phase, which step, what action is expected, why it matters. The implementation is a function that evaluates state at click time and returns the right line in character voice.

Phase 2 version is lighter — the spy appears briefly at entry to explain the tie-break rule and the Winner/Qualifier distinction, then recedes.

**Long-term goal:** zero dependency on external onboarding. A group that has never seen the tool should be able to play a complete session correctly from the interface alone.

### P1 — Validate funnel data (no-code)

Wait for 10+ completed sessions in PostHog. Confirm or deny the Phase 1 drop-off hypothesis before building anything.

### P1 — Variable game length

Currently capped at 10 findings. Facilitators running 60-minute sessions vs. 3-hour workshops need different pacing. Add a setup option to configure min/max findings (3–15 range).

**Why this matters:** The 10-finding cap was set for a specific seminar format. If sessions are starting but not completing, this is likely a contributing factor.

### P2 — Session export

Allow downloading findings + votes as CSV or PDF at the results screen, in addition to print.

**Why this matters:** Facilitators currently print or screenshot. CSV gives them something they can bring into a spreadsheet and share with leadership. This is a retention play — if the artifact is more useful, facilitators run the game again.

### P3 — Facilitator mode

A second URL parameter (`?facilitator=true`) that unlocks controls for managing the session from a shared screen — advancing turns, overriding the timer, revealing findings in Phase 2 without requiring everyone to crowd around one laptop.

**Why this matters:** The current UX assumes one person runs the game on their own device. In practice, larger sessions use a projector and a facilitator who isn't one of the players.

### P4 — Multi-language support

English version of the decks. The game logic is language-agnostic; the cards are not.

**Why this matters:** The current user base is Spanish-speaking (EAFIT, Colombian organizations). International research groups have expressed interest. This unlocks a larger potential audience without changing the core mechanic.

---

## Reflections

**What worked:** The constraint of single-file HTML forced deliberate trade-offs. No dependencies means no dependency hell, no build failures, no "npm install" before a session. The downside is that the codebase grows less maintainable — a V4 would likely extract JS into a module.

**What I'd do differently:** Instrument earlier. V1 and V2 ran with no analytics, so the funnel data I'd most want — how many sessions completed, where they dropped off — doesn't exist. The baseline only starts from V3.

**The open question:** The game produces qualitative output (findings and votes) but the results screen shows a *ranking* — who scored highest. The ranking is a game mechanic that creates engagement, but it may distort behavior: players optimize for points rather than for honest discovery. I don't have data on this yet. It's the thing I'd most want to test with a controlled session.

---

*Built by [Paul Moscoso V.](https://www.linkedin.com/in/paulmoscosov) · EAFIT Strategy Research Seminar · 2025–2026*
