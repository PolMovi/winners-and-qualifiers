Winners & Qualifiers — PM Case Study
A browser-based workshop tool that helps organizational teams identify tacit strategic assets.
→ Live product · → Repo

The problem
Organizational strategy theory has known for decades that the most defensible competitive advantages come from resources and capabilities that are hard to see — tacit knowledge, informal networks, unwritten routines, intuitions built over years. These don't show up in org charts or asset registers.
The practical problem: how do you surface these in a room full of people, without it becoming a consultant-led interview exercise that produces a slide deck nobody reads?
The research team at EAFIT's strategy seminar needed a tool that:

Works without a consultant in the room
Gets to the tacit stuff — not just what people think they should say
Creates a real artifact teams walk away with
Scales from 3 to 10 players in a classroom setting


Hypothesis

A card-based game with a structured two-phase flow — individual exploration followed by collective voting — will surface tacit assets more effectively than a guided discussion, because it distributes the discovery burden across all players and uses democratic pressure to separate what's genuinely valued from what's merely volunteered.

Secondary hypothesis: the game needs to feel like it was designed on purpose. A rough tool gets rough engagement.

Product decisions
Two-phase structure
Phase 1 (Exploration) is individual and timed. Each player draws one question card and one feature card, then articulates a finding — a resource or capability they've observed in the organization. The 5-minute timer is intentional: it prevents overthinking and forces first-instinct answers, which tend to be more tacit.
Phase 2 (Classification) is collective. All findings from Phase 1 go into a deck. Players draw a ★ criterion card and vote democratically on whether each finding is a Winner (strategically differentiating) or a Qualifier (valuable but not rare or inimitable). This separation matters: if players voted on their own findings in real time, social dynamics would anchor the group toward validation.
The decks
Question deck (40 cards): Organized across five categories grounded in tacit knowledge literature — tacit knowledge, informal networks, collective routines, intuition and decision-making, vulnerabilities and resilience. Questions are written in first person and designed to trigger recall ("What trick do you use at work that's not in any manual?") rather than reflection ("What are your core competencies?"). The difference is important: recall surfaces specific, tacit, real things. Reflection surfaces things people think sound good.
Feature deck (40 cards): Five VRIO-adjacent categories — singularity vs. competition, customer-perceived value, rarity and distinctive origin, difficulty of imitation, organizational capacity to exploit. These are not VRIO checkboxes. They're conversation prompts framed as characteristics ("It would take years or major investment for another organization to build an equivalent").
★ Star deck (10 cards): The W&Q criteria. These operationalize "what makes a Winner" without relying on expert judgment. Questions like "Is this difficult to copy or replicate?" and "Does it generate visible value for the customer?" give the voting group a shared anchor. Without this, votes converge on who spoke most convincingly in Phase 1.
Tie-break favors Yes
When the vote is split, the finding is classified as a Winner.
This was a deliberate design choice. In a discovery exercise, the error cost is asymmetric: suppressing a finding that was actually strategic (false negative) is worse than including a weak one (false positive). The game explicitly produces candidates, not conclusions — the VRIO warning on the results screen handles the interpretation question.
Type detection (Recurso / Capacidad)
The app automatically classifies each finding as a Resource or a Capability based on the first word: infinitive verbs ending in -ar/-er/-ir classify as Capability. Anything else classifies as Resource. Players see a brief badge confirming the classification after each submission.
Why keep a heuristic this simple? Because the classification boundary isn't the point — it's a teaching scaffold. The badge creates a moment where players either confirm or question the classification, which teaches the distinction through repetition. A more sophisticated NLP classifier would remove that moment and add a dependency.
Scoring

Capability finding: 5 base points
Resource finding: 3 base points
+1 bonus if Phase 1 feature criterion was met
Phase 2 vote: confirmed → keeps Phase 1 score; rejected → score becomes 0

The differential (5 vs. 3) reflects that capabilities are generally harder to identify than resources and more strategically valuable. It also creates an incentive to articulate findings as capabilities, which improves output quality over the course of a session.
No backend, no accounts
All state lives in memory. When the session ends, it's gone. The only data that leaves the device is the three PostHog events documented below.
Why: The tool runs in classrooms where network reliability varies and time pressure is real. No login, no sync, no waiting for a server. The constraint forced better design — the confirmation modal before exiting mid-game exists because losing session data is a real and unrecoverable failure.

Design evolution
V1 — November 2025: Validate the concept
Generic white card UI on a light blue-grey gradient. System fonts. Emoji placeholders for card deck imagery. All buttons visible simultaneously. No instrumentation. Built to answer one question: does the two-phase structure work?
It did. Players engaged with the prompts. The vote mechanic produced real debate. The type detection heuristic was rough but sufficient.
What it revealed: the UI signaled "rough prototype," which reduced participant investment. Players had to be verbally guided through the sequence by the facilitator. The mental model problem surfaced immediately — players believed they were supposed to answer the question card directly in the writing box. Wrong. The question opens a debate. The writing box captures what that debate reveals. That distinction is the entire conceptual unlock for Phase 1, and the interface was not communicating it.
V2 — Late 2025: Fix the flow, start the visual identity
Two things happened in parallel.
UX fix: Introduced progressive disclosure driven by button state. Buttons are now disabled until the prior step is complete. The sequence — select cards → write finding → answer Yes/No → next turn — is enforced by the interface, not by instruction text. Players can't proceed out of order because out-of-order actions are physically unavailable. Added inline guidance visible during each turn. Made the type detection badge visible immediately after submission. Added progress tracking for Phase 1.
Visual identity start: Replaced the generic blue accent with a constructivist design direction. Introduced the three-font pairing: Big Shoulders Display for headings, Archivo for body, JetBrains Mono for all UI labels and metadata. Established the neon yellow-green (#DFFF00) as sole accent on a warm khaki background. Zero border-radius on any element. Hard offset shadows on primary buttons (the classic constructivist print effect). Grid and dot-matrix background textures layered to create a technical paper feel.
The goal was to make the tool feel like it belongs in a strategy context — not a classroom exercise, not a SaaS product, not a game show. The visual language signals seriousness without formality.
V3 — May 2026: Complete the world
Full execution of the design direction established in V2.
Home screen: Animated radar/sonar sweep with phosphor blip decay and fake telemetry readouts (Range, Depth, Azimuth, Speed, Bearing). These instrument readings are purely aesthetic — they extend the strategic intelligence metaphor before the game starts. Someone landing on V1 saw a form. Someone landing on V3 sees a world.
Card imagery: Custom assets replace emoji placeholders — Pregunta.png, Caracteristica.png for Phase 1 decks; Submarine.png, Torpedo.png for Phase 2. The submarine and torpedo pair extends the sonar metaphor into the mechanics.
Button interactions: Primary buttons lift on hover (translateY(-2px), shadow deepens) and press on click (translate(2px,2px), shadow collapses). A physical press mechanic, not just a color change.
Screen transitions: Every screen entrance animates in (opacity: 0→1, translateY(8px→0), 360ms). Navigation feels deliberate rather than instantaneous.
Close button: Fixed position, hard border, rotates 90 degrees and turns danger red on hover. An action with real visual weight.
Functional additions: Exit confirmation modal, responsive layout, print-ready results screen, PostHog instrumentation, privacy notice on the setup screen.
Credit restructure: Listed as Developer separately from academic leads. Ownership clarified.

The onboarding problem — and where it's going
What's still broken
Progressive disclosure solved the sequence problem. It did not solve the mental model problem.
Players still believe the question card is a prompt they should answer directly. The instructions exist in multiple places — the guidance box, the phase header, the screen instruction text. Players don't read them. This is not a bug. It's a known property of humans under social pressure in a group setting.
The distinction that needs to land: the question card opens a conversation. What you write in the box is what that conversation reveals about your organization. That shift — from answering a question to surfacing a finding — is conceptually simple but repeatedly misunderstood on first contact.
Instruction text doesn't fix this. More instruction text makes it worse.
The vision: contextually aware in-game narrator
The reference points are Bastion and Portal — games where a voice character explains the world as you move through it. The rules are never delivered as a manual. The world teaches you through a voice that belongs to it.
For Winners & Qualifiers that voice is a spy — consistent with the strategic intelligence aesthetic already established in the visual design.
Phase 1 entry animation: When Phase 1 loads, the spy appears and walks through the sequence while the relevant UI elements are highlighted in real time. He explains that the question card is not a question to answer — it's a signal to start a conversation. The writing box captures what that conversation surfaces. The skip button exits the animation immediately for returning players and facilitators who don't need it.
Persistent spy icon: After the animation, the spy collapses to a small icon in the bottom-left corner. Clicking at any point triggers a contextually aware response — a live read of appState at click time:

Current phase and step
What action is expected right now
Why that action matters in the context of the game

This is not a help menu or a FAQ. It's a character who knows where you are and tells you what to do next in the voice of the game. The implementation is a function that evaluates current state and returns the appropriate message. The character voice is what makes it feel like the game rather than a tooltip.
Phase 2: Lighter entry animation. The spy explains the tie-break rule and the Winner/Qualifier distinction, then recedes. Less friction in Phase 2 means less intervention needed.
Long-term goal: Zero dependency on external onboarding. No facilitator guide, no tutorial video, no instructions page. A group that has never seen the tool should be able to complete a full session correctly from the interface alone. The tutorial video currently in production is a bridge to that state, not the destination.
Success metric: Sessions completing Phase 1 without facilitator intervention, measured via PostHog by tracking the ratio of phase_2_started to phase_1_started. A rising completion rate after the spy ships is the signal.

What's instrumented and why
PostHog EU captures three events per session:
EventPropertiesWhat it answersphase_1_startedplayers_count, org_typeAre sessions being started? What's the typical group size?phase_2_startedfindings_countAre sessions completing Phase 1? What's the average finding yield?results_reachedwinners_countAre sessions completing end-to-end? What's the Winner rate?
The gap I'm watching: the drop between phase_1_started and phase_2_started. The hypothesis is that some sessions stall in Phase 1 — players lose steam before reaching the 10-finding cap, or the mental model problem causes enough confusion that facilitators abandon the session. If that drop is significant, the intervention is the spy narrator, not a UI tweak.
What I'm not tracking: player names, finding text, organization name, votes. The tool explicitly tells players "data is not transmitted or stored." That statement needs to stay true.

Roadmap
Prioritized by impact on the core hypothesis, not by implementation ease.
P0 — Validate funnel data (no-code)
Wait for 10+ completed sessions in PostHog. Confirm or deny the Phase 1 drop-off hypothesis before building anything. If the drop is small, the spy is a nice-to-have. If it's large, the spy is P1.
P1 — Spy narrator
Contextually aware in-game character as described above. Entry animation for Phase 1 with skip. Persistent help icon reading live app state. Phase 2 lighter variant. This is the highest-leverage UX investment available — it addresses the one failure mode that instruction text cannot fix.
P2 — Variable game length
Currently capped at 10 findings. Facilitators running 60-minute sessions vs. 3-hour workshops need different pacing. Add a setup option to configure min/max findings in the 3–15 range. If PostHog confirms Phase 1 drop-off, this ships alongside P1 as a complementary mitigation.
P3 — Session export
Allow downloading findings and votes as CSV or PDF at the results screen, in addition to print. Facilitators currently screenshot or print. CSV gives them something they can share with leadership. This is a retention play — if the artifact is more useful, facilitators run the game again.
P4 — Facilitator mode
A second URL parameter (?facilitator=true) that unlocks controls for managing the session from a shared screen — advancing turns, overriding the timer, revealing findings in Phase 2 without requiring everyone to crowd around one laptop. Current UX assumes one person runs the game on their own device. Larger sessions use a projector.
P5 — Multi-language support
English version of the decks. The game logic is language-agnostic. The cards are not. This unlocks international research groups without changing the core mechanic.

Reflections
What worked: The single-file HTML constraint forced deliberate trade-offs. No dependencies means no dependency hell, no build failures, no install friction before a session. The downside is a growing codebase — a V4 would likely extract JS into modules.
What I'd do differently: Instrument earlier. V1 and V2 ran with no analytics. The funnel data I'd most want — how many sessions completed in the early months, where they dropped off — doesn't exist. The baseline only starts from V3. The lesson: instrumentation is not a feature you add when the product is ready. It's infrastructure you put in before the first real user.
The open question: The game produces qualitative output but the results screen shows a ranking — who scored highest. The ranking is a game mechanic that creates engagement, but it may distort behavior: players optimize for points rather than for honest discovery. I don't have data on this yet. It's the thing I'd most want to test with a controlled session where the ranking is hidden until the end versus shown in real time.

Built by Paul Moscoso V. · EAFIT Strategy Research Seminar · 2025–2026
