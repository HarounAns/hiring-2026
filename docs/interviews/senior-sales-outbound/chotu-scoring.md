# Scoring & Debrief: Chotu

**Date:** April 5, 2026
**Duration:** 49 minutes
**Format:** Retell AI interviewer (voice-only, practice simulation)
**Transcript:** [chotu-transcript.md](chotu-transcript.md)

---

## Immediate Debrief

### 1. Best Thing They Said

When the agent suggested pausing an entire dealer's outreach at 2am, Chotu pushed back: "Isn't that kind of going against the principle we said before? ... Shouldn't we just shut off the one that's problematic and leave the rest running?" This showed consistency of thinking, willingness to challenge, and the ability to carry a design principle across contexts.

### 2. Biggest Concern

Initially shipped the dealer's feature request without questioning it ("That sounds pretty reasonable to me. I think I'd do it.") — the textbook implementer response. Recovered after a nudge, but the instinct was wrong. On the killer question (one metric), couldn't land a definitive answer despite several minutes of reasoning. Struggled to connect "what the dealer cares about" to metric selection without heavy prompting.

### 3. Your Vote

- [ ] **Strong Yes**
- [ ] **Yes**
- [x] **No**
- [ ] **Strong No**

### 4. Gut Check — Would you trust this person to take over the Sales product from you?

- [ ] **Yes**
- [x] **No**

Not yet. Good instincts on several dimensions, but needed too many nudges to get there, and the product ownership phase revealed an implementer-first reflex.

### 5. One Sentence Summary

Curious and methodical domain modeler with solid ops instincts, but defaults to implementer mode on product decisions and struggles to identify the right metric without coaching.

---

## Detailed Scoring Rubric

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Domain Modeling** | 3.5/5 | Good CRM model discovered through questions. Separated Lead from Contact, identified VehicleOfInterest as optional, lifecycle states on Lead (uncontacted → contacted → engaged → booked). Missed CrmNote entirely, missed Appointment as first-class entity with its own lifecycle. Agent side required a nudge ("how does the AI know what to say?") but then reasoned well — landed on agent config per lead source with dynamic variables, and LeadSource as the bridge entity. |
| **Ops Thinking** | 3/5 | Good instinct on HubSpot webhook trigger, CRM credential validation, and discovery from historical data. Flagged unknown sources for human review unprompted. Got to evals/verification after a nudge. Got to monitoring after a nudge (error logging, LLM-as-judge, booking rate thresholds, healthy vs unhealthy accounts). Auto-disable came after a nudge, but then corrected the interviewer on surgical vs blunt disable — strong. Missing: state machine thinking, idempotency, retry/backoff, self-healing, rollback. |
| **Product Ownership** | 2.5/5 | Initially shipped the feature request ("I think I'd do it") — red flag. Recovered to A/B testing after "How do you know it's actually better?" Proposed 10-20-30% rollout, cross-dealer testing. But needed prompting to think beyond booking rate to show rate. On the measurement gap, proposed running the experiment in parallel while building tracking — pragmatic but didn't say "design measurement before running experiments." |
| **Quantitative Rigor** | 2.5/5 | Identified the right metrics in the funnel (engagement → booking → show → close) but couldn't pick one. Killer question answer was indecisive — spent several minutes going back and forth between booking rate and show rate, eventually needed the interviewer to frame it. Didn't ask for baselines. Didn't think about sample size or statistical rigor for A/B tests. |
| **Model Evolution** | 3/5 | When asked if the data model supports A/B testing variants, acknowledged it doesn't and would need to change the agent config to support variants. Mentioned PostHog as an alternative. Didn't sketch out how the model would actually change — stayed abstract. |
| **Curiosity** | 4/5 | Strong. Asked lots of clarifying questions in Phase 1 — "Is a lead the same as a CRM?", "Can you explain each lead type?", "Do all leads have vehicles of interest?", "What's the goal of the system?", "Are we just warming them for a human?" Phase 2 also asked good questions — "Is HubSpot the CRM?", "How are engineers getting the credentials today?", "What's in a config?" Sometimes too many questions before starting to build, but overall a positive signal. |
| **Communication** | 2.5/5 | Coherent thinking but very meandering. Lots of verbal processing ("like, you know, so so so"), restarts, and tangents. Hard to follow the thread at times. In a written format this would likely be stronger, but for voice-only it was hard to track his reasoning. |

**Total:** 21 / 35

### Score Interpretation

21 is at the boundary of Yes territory (21-27) and No territory (14-20). However, the critical Product Ownership dimension at 2.5 and the initial implementer instinct on the dealer email are concerning for a role that is fundamentally about product ownership.

---

## What They Mentioned (Checklist)

### Phase 1: Domain Modeling

**CRM side — did they discover these through questions?**

- [x] **Lead** as the central entity (not customer)
- [x] **Contact** separate from Lead (co-buyers not mentioned, but 1:many relationship identified)
- [x] **VehicleOfInterest** separate from inventory (identified as optional depending on source)
- [ ] **Appointment** with purpose types and lifecycle states — mentioned appointment as a terminal state on Lead, but never modeled it as its own entity
- [ ] **CrmNote** as the write-back entity — never surfaced despite "we sync everything back" in the scenario
- [x] Lifecycle states on Lead (uncontacted → contacted → engaged → booked → showed)
- [ ] Lifecycle states on Appointment — not modeled separately
- [ ] Who booked the appointment — AI vs human (attribution) — never mentioned

**Agent side — did they model this?**

- [x] Agent configuration as a first-class concept (after nudge)
- [x] Different lead types or sources → different agent behavior
- [x] Per-dealer customization (greeting, personality, dynamic variables)
- [x] Routing logic — lead source maps to agent config
- [ ] Campaign/orchestration layer intuited without being told — got close with LeadSource → AgentConfig but didn't name an explicit routing entity

### Phase 2: Ops Automation

- [x] Connected to their Phase 1 model ("go spin up all the lead sources and tie them to the dealership")
- [ ] Thought in state machines / stages, not a flat checklist
- [x] Asked about failure modes (credential validation, unknown sources)
- [ ] Mentioned idempotency
- [x] Separated human decisions from automatable steps (unknown sources → human, known → auto)
- [x] Designed verification / evals before go-live (after nudge)
- [x] Thought about ongoing per-dealer health monitoring (after nudge)
- [ ] Automated detection of broken journeys — mentioned thresholds/alerts but not journey-level detection
- [ ] Self-healing with retry/backoff
- [x] Auto-disable (after nudge, then refined to surgical disable)

**Unprompted vs nudged:**

| Concept | Unprompted? |
|---------|------------|
| HubSpot webhook trigger | Yes |
| CRM credential validation | Yes |
| Discovery from historical data | Nudged ("What could you learn...") |
| Template matching for known sources | Yes (auto-create agent configs) |
| Flag unknown sources | Yes |
| Don't block dealer for unknowns | Yes |
| Verification / evals | Nudged |
| Monitoring | Nudged |
| Auto-disable | Nudged, then refined unprompted |

### Phase 3: Own It

**Beat 1 — Customer email:**

- [ ] Recognized the email as a hypothesis, not a feature request — initially didn't ("I think I'd do it")
- [x] Articulated the inventory-first vs appointment-first tradeoff (after nudge)
- [x] Proposed A/B testing instead of just shipping the change (after nudge)
- [x] Thought about what metric to optimize — eventually got to booking rate + show rate

**Beat 2 — Systematic optimization:**

- [x] A/B testing as infrastructure, not ad hoc prompt changes — proposed a self-learning system with LLM-as-judge recommending prompt changes
- [ ] Extended Phase 1 agent model to support variants — acknowledged it would need to change but didn't design it
- [ ] Knew the right metric hierarchy — struggled, mentioned booking rate primarily
- [ ] Thought about statistical rigor — never mentioned sample size or duration

**Follow-up — Measurement gap:**

- [ ] "I need to build show rate tracking before declaring a winner" — instead proposed running the experiment in parallel while building tracking
- [ ] "Design measurement before running experiments" — not stated
- [x] Didn't trust dealer sentiment as a substitute for data
- [x] Didn't optimize for the wrong metric alone

**Killer question — One metric:**

- [ ] Named a downstream metric with conviction — went back and forth, couldn't land it
- [x] Reasoned through the funnel (engagement → booking → show → close → revenue)
- [ ] Arrived at an answer independently — needed the interviewer to frame "what does the dealer actually care about?"

### Meta-Signals

- [ ] Connected the three phases unprompted — transitions were driven by the agent
- [ ] Asked "why does the dealer want this?" or "how would we know if this works?" — initially skipped this
- [x] Thought from the dealer's perspective (eventually — "the dealer wants to sell more cars")
- [ ] Showed product sense unprompted — opinions about what to build came after prompting

---

## Red Flags (Check Any That Apply)

- [ ] "List the entities for me"
- [ ] Tables first
- [ ] No agent model (needed a nudge, but got there)
- [ ] "Build a dashboard"
- [x] **Shipped the feature request** — "That sounds pretty reasonable to me. I think I'd do it."
- [ ] "That's a PM question"
- [ ] Activity metrics
- [ ] Sentiment > data
- [ ] Happy path only (did mention failure modes)
- [ ] Implementer language

**Red flag count: 1** — Not disqualifying alone, but it was the single most important question in Phase 3.

---

## Phase-by-Phase Notes

### Phase 1: Domain Modeling

**Their model:**
- Dealership (primary entity)
- Contact (belongs to dealership, 1:many with leads)
- Lead (the event/opportunity, has lifecycle: uncontacted → contacted → engaged → booked)
- LeadSource (bridge entity — separate table, many:many with dealers)
- VehicleOfInterest (optional, depends on source)
- AgentConfig (per lead source, with dynamic variables, tools, greeting)
- Missing: Appointment (as entity), CrmNote, RoutingRule

**CRM side quality:** Good. Discovered entities through questions. Separated Lead from Contact correctly. Lead lifecycle was solid. Missed Appointment and CrmNote.

**Agent side quality:** Required a nudge but then reasoned well. Went through the spectrum (one agent for everything → agent per contact → agent per lead source) and landed in the right place. LeadSource as bridge was discovered organically.

**Clarifying questions they asked:** Many — understood the problem before designing. Asked about lead sources, vehicle of interest optionality, system goals, terminal states. Good signal.

**Quality:** ✅ Great on CRM side / ⚠️ Needed nudge on Agent side

---

### Phase 2: Ops Automation

**Their approach:** HubSpot webhook → validate CRM creds → pull historical leads to discover sources → auto-create agent configs for known sources → flag unknowns → run evals → go live → monitor with thresholds and LLM-as-judge → surgical auto-disable.

**Did they connect to Phase 1 model?** Yes — "go spin up all the lead sources and tie them to the dealership."

**Failure modes they identified:** Bad CRM credentials, unknown lead sources, AI sending bad messages at 2am, broken agent configs.

**What they missed:** State machine stages (connected → discovered → configured → verified → live), idempotency, retry/backoff queues, self-healing, explicit rollback mechanism.

**Quality:** ⚠️ Mediocre-to-Good — Right instincts but needed multiple nudges. The surgical disable correction was the standout moment.

---

### Phase 3: Own It

**Beat 1 — How they handled the dealer email:** Initially shipped it. After "How do you know it's actually better?" pivoted to A/B testing at 10-20-30% traffic. Proposed cross-dealer testing. But the initial instinct was wrong.

**Beat 2 — Their system for optimization:** Proposed a self-learning system: LLM-as-judge reads conversations → identifies improvement areas → recommends prompt changes → A/B tests them → auto-rollout if metrics improve. Creative and ambitious, but didn't think about statistical rigor, and acknowledged the data model would need to change without designing how.

**Follow-up — Measurement gap:** Proposed running experiment in parallel with building show rate tracking ("tortoise and hare"). Pragmatic, but didn't frame it as "measurement before experiments." Eventually identified CRM appointment completion status as the data source for show rate.

**Killer question:** Struggled. Went back and forth between booking rate and show rate. Couldn't land a conviction. Eventually talked through the full funnel (engagement → booking → show → close → revenue) but needed heavy coaching. Said "honestly I'm not sure I have a great answer for you."

**Quality:** ⚠️ Mediocre — Implementer instinct on the email. Creative on systematic optimization but lacked rigor. Indecisive on metrics.

---

## Final Decision

### Your Vote
- [ ] **Strong Yes**
- [ ] **Yes**
- [x] **No**
- [ ] **Strong No**

### Rationale

Strong curiosity and solid domain modeling instincts — the CRM side was well-discovered through questions, and the lead source as bridge entity was a genuine insight. Ops thinking was decent with good instincts on discovery, flagging unknowns, and surgical auto-disable.

However, three things push this to a No:

1. **Shipped the feature request.** The single most revealing moment in the interview. The instinct was "I'd do it" — implementer mode. Recovered after nudging, but the first instinct matters because in this role, there's no one nudging you.

2. **Couldn't pick a metric.** The killer question is supposed to reveal whether someone thinks about the product from outcomes. Several minutes of reasoning, never landed with conviction. This role requires opinionated thinking about what matters.

3. **Nudge-dependent throughout.** Discovery from data, verification, monitoring, auto-disable — all required prompting. The right person hits most of these unprompted. Getting there after nudges shows potential but not readiness.

### What Would Need to Change for a Yes?

- Ship the feature request as a hypothesis on first instinct, not after nudging
- Land on a metric with conviction and defend it
- Hit at least 3-4 of the Phase 2 concepts unprompted (discovery, verification, monitoring, auto-disable)
- Model Appointment and CrmNote without being prompted
