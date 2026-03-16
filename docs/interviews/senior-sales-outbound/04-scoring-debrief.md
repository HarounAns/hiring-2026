# Scoring & Debrief Template

**When to use:** Fill this out within 5 minutes of the interview ending.

---

## Immediate Debrief (Write This First)

**Do this before you do anything else. Your memory will fade.**

### 1. Best Thing They Said
*The moment you knew they got it (or didn't).*

```
[Write here]
```

### 2. Biggest Concern
*What worries you most about hiring them?*

```
[Write here]
```

### 3. Your Vote
*Pick one. If you're not sure, it's a No.*

- [ ] **Strong Yes** — Will own this product Day 1. Hire immediately.
- [ ] **Yes** — Solid hire. Good instincts, will ramp fast.
- [ ] **No** — Not ready. Implementer, not owner.
- [ ] **Strong No** — Red flags. Wrong person for this role.

### 4. Gut Check
*Would you trust this person to take over the Sales product from you?*

- [ ] **Yes**
- [ ] **No**

**If you answered No, your vote should be No regardless of other signals.**

### 5. One Sentence Summary
*If you had to describe this candidate to Samee in one sentence:*

```
[Write here]
```

---

## Detailed Scoring Rubric

**Rate each dimension 1-5.**

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Domain Modeling**<br>Did they discover entities through questions? Model both CRM and agent sides? Think about lifecycle states? | /5 | |
| **Ops Thinking**<br>State machines? Failure modes? Idempotency? Verification before go-live? Self-healing? Per-dealer health? | /5 | |
| **Product Ownership**<br>Did they recognize the dealer email as a hypothesis? Propose testing? Articulate tradeoffs? | /5 | |
| **Quantitative Rigor**<br>Did they design experiments? Know what metric matters? Close the measurement loop? Ask for baselines? | /5 | |
| **Model Evolution**<br>Could they extend their Phase 1 model for A/B testing in Phase 3? Cleanly, not bolted on? | /5 | |
| **Curiosity**<br>Deep clarifying questions? Or jumped straight to solutions? | /5 | |
| **Communication**<br>Clear writing, structured thinking, easy to follow? | /5 | |

**Total:** _____ / 35

### Score Interpretation

- **28-35:** Strong Yes territory
- **21-27:** Yes territory
- **14-20:** No territory
- **Below 14:** Strong No territory

**But:** Use judgment. One critical dimension at 1-2 can be disqualifying even if overall score is high.

---

## What They Mentioned (Checklist)

### Phase 1: Domain Modeling

**CRM side — did they discover these through questions?**

- [ ] **Lead** as the central entity (not customer)
- [ ] **Contact** separate from Lead (co-buyers)
- [ ] **VehicleOfInterest** separate from inventory (intent vs reality)
- [ ] **Appointment** with purpose types and lifecycle states
- [ ] **CrmNote** as the write-back entity (surfaced from scenario)
- [ ] Lifecycle states on Lead (open → contacted → engaged → ... → won/lost)
- [ ] Lifecycle states on Appointment (scheduled → confirmed → completed/no_show/cancelled)
- [ ] Who booked the appointment — AI vs human (attribution)

**Agent side — did they model this?**

- [ ] Agent configuration as a first-class concept
- [ ] Different lead types or sources → different agent behavior
- [ ] Per-dealer customization (greeting, personality)
- [ ] Routing logic — how a lead gets matched to the right agent
- [ ] (Bonus) Campaign/orchestration layer intuited without being told

### Phase 2: Ops Automation

- [ ] Connected to their Phase 1 model ("I need to create these entities...")
- [ ] Thought in state machines / stages, not a flat checklist
- [ ] Asked about failure modes at each step
- [ ] Mentioned idempotency (re-running without side effects)
- [ ] Separated human decisions from automatable steps
- [ ] Designed verification / dry-run / smoke test before go-live
- [ ] Thought about ongoing per-dealer health monitoring
- [ ] (Follow-up) Automated detection of broken journeys
- [ ] (Follow-up) Self-healing with retry/backoff, not just scripts

### Phase 3: Own It

**Beat 1 — Customer email:**

- [ ] Recognized the email as a hypothesis, not a feature request
- [ ] Articulated the inventory-first vs appointment-first tradeoff
- [ ] Proposed A/B testing instead of just shipping the change
- [ ] Thought about what metric to optimize (appointment rate alone isn't enough)

**Beat 2 — Systematic optimization:**

- [ ] A/B testing as infrastructure, not ad hoc prompt changes
- [ ] Extended Phase 1 agent model to support variants
- [ ] Knew the right metric hierarchy (response → appointment → show → sold)
- [ ] Thought about statistical rigor (sample size, duration, generalizability)

**Follow-up — Measurement gap:**

- [ ] "I need to build show rate tracking before declaring a winner"
- [ ] "Design measurement before running experiments"
- [ ] Didn't trust dealer sentiment as a substitute for data
- [ ] Didn't optimize for the wrong metric (appointment rate alone)

### Meta-Signals

- [ ] Connected the three phases unprompted (model → ops → measurement)
- [ ] Asked "why does the dealer want this?" or "how would we know if this works?"
- [ ] Thought from the dealer's perspective, not just engineering
- [ ] Showed product sense — opinions about what to build, not just how

---

## Red Flags (Check Any That Apply)

- [ ] **"List the entities for me"** — Can't extract a model from a domain
- [ ] **Tables first** — Started with columns before relationships
- [ ] **No agent model** — Only modeled data, not behavior
- [ ] **"Build a dashboard"** — Solution to ops is always a UI
- [ ] **Shipped the feature request** — Changed the prompt because the dealer asked
- [ ] **"That's a PM question"** — Defers product thinking
- [ ] **Activity metrics** — "Track messages sent" instead of outcomes
- [ ] **Sentiment > data** — "If the dealer loves it, it's working"
- [ ] **Happy path only** — No failure modes mentioned
- [ ] **Implementer language** — "What do you want me to build?" energy throughout

**If 2+ red flags → Strong No**

---

## Phase-by-Phase Notes

### Phase 1: Domain Modeling

**Their model (sketch or describe):**
```
[Write here — what entities did they identify? What relationships?]
```

**CRM side quality:**
```
[Write here]
```

**Agent side quality:**
```
[Write here]
```

**Clarifying questions they asked:**
```
[Write here]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

### Phase 2: Ops Automation

**Their approach:**
```
[Write here]
```

**Did they connect to their Phase 1 model?**
```
[Write here]
```

**Failure modes they identified:**
```
[Write here]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

### Phase 3: Own It

**Beat 1 — How they handled the dealer email:**
```
[Write here]
```

**Beat 2 — Their system for optimization:**
```
[Write here]
```

**Follow-up — How they handled the measurement gap:**
```
[Write here]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

## Bonus: Equity Mining Curveball (If Used)

**How they handled it:**
```
[Write here]
```

**Did their model survive the extension?**
- [ ] Yes — clean generalization
- [ ] Partially — some refactoring needed
- [ ] No — bolted on / parallel tables

---

## Final Decision

### Your Vote
- [ ] **Strong Yes**
- [ ] **Yes**
- [ ] **No**
- [ ] **Strong No**

### Rationale
*Why did you give this vote? What were the deciding factors?*

```
[Write here]
```

### What Would Need to Change for a Yes?
*If you voted No, what would need to be different?*

```
[Write here]
```

---

## Share with Team

### For Samee (Closing)

**If they passed:**

```
[Candidate Name] - [Strong Yes / Yes]

Strengths:
- [Top 3 strengths]

Areas to develop:
- [Top 2-3 areas they'd need to grow]

Biggest concern:
- [What worries you most]

Confident they can hit Month 1 targets: [Yes / Maybe / No]
```

---

## Remember

- **One No = No Hire.** Everyone must say yes.
- **If you're not sure, it's a No.** Default to No.
- **Trust your gut.** If something feels off, it probably is.
- **Write notes immediately.** You'll forget the nuance within an hour.
