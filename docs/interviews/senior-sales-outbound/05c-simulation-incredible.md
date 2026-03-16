# Simulation: Incredible Candidate

**Profile:** 5 years experience. Built a logistics automation platform at a mid-stage startup. Owned the product end-to-end — engineering, ops, customer relationships. Left to do something earlier-stage.

**Vote: Strong Yes (32/35)**

---

## Phase 1: Model the Domain

*After hearing [the scenario](02-cheat-sheet.md#the-scenario-say-this), she sits for about 20 seconds. Then:*

> "Before I start modeling — I want to make sure I understand the domain, not just the system. A few questions."

> "When you say 'lead' — is that the person, or is it the sales opportunity? Like, if one person submits on AutoTrader for Dealer A and Cars.com for Dealer B, is that one lead or two?"

**You:** "Two. A lead belongs to one dealership. Same human, different opportunities."

> "Okay. So Lead is the central entity. Not the customer — the opportunity. And we probably don't even try to de-dupe across dealerships."

> "The person attached to the lead — is it always one person? Or could there be a co-buyer, a spouse, someone else on the deal?"

**You:** "Primary buyer and sometimes a co-buyer."

> "So Contact is a separate entity from Lead. A lead has one or more contacts, one is primary. The contact has the phone number, email — that's what drives outreach. Not the lead itself."

> "On vehicles — when the customer says 'I want a Civic,' is that pointing at a specific car on the lot, or is it just their interest? Those feel like different things."

**You:** "Different things. We have a separate inventory service."

> "Right. So there's a VehicleOfInterest — the customer's intent. Make, model, year, maybe a VIN if they clicked on a specific listing. But it's not inventory. Inventory is external. I'd keep them separate because one is what the customer wants, the other is what actually exists. A VehicleOfInterest might not have a match on the lot."

*Starts writing the model:*

> "Let me build this up. The CRM side first.
>
> **Dealer** — the business. Has CRM credentials, polling config, their own settings — name, hours, address. This is context the AI will need but it's about the dealership, not about agent behavior.
>
> **Lead** — belongs to a Dealer. This is the unit of work. Has a lifecycle — I'd say at minimum: open, contacted, engaged, appointment_set. Then terminal states: won, lost, dead. 'Won' means they bought a car. 'Lost' means they went elsewhere. 'Dead' means the lead went cold or was bad data. The CRM probably owns the terminal states, not us — the dealer's sales team makes that call.
>
> One thing — you said we check eligibility before outreach. That means not every lead gets worked. I'd track eligibility on the lead: eligible or not, and the reason why not. 'No phone number,' 'already contacted,' 'walk-in lead.' That's important for analytics — you want to know what percentage of leads are even reachable.
>
> **LeadSource** — you said leads come from AutoTrader, Cars.com, OEM programs, walk-ins, phone calls. That's not just a label on the lead. A source has properties — it has a channel type (web, oem, phone, walk-in), and different sources mean fundamentally different customer intent. An AutoTrader lead actively searched for a car. An OEM lead might be a financing offer. A walk-in is already at the dealership. These aren't just strings — they determine how the AI should behave. So I'd make this a first-class entity. A Lead belongs to a LeadSource."

**You:** "Why not just a string on the lead?"

> "Because I'll need to use the source for routing — matching leads to the right AI behavior. If it's a string, I'm pattern-matching on free text. If it's an entity, I have a clean foreign key and I can put metadata on it — channel type, expected intent level, whether we should even do outreach for this source. And for analytics later, I want to slice performance by source. An entity gives me a clean dimension to group by.
>
> **Contact** — belongs to a Lead. Phone, email, name. Primary flag. And a do-not-contact flag — some people opt out.
>
> **VehicleOfInterest** — belongs to a Lead. Year, make, model, optional VIN. Primary flag if they have multiple. And some kind of availability state — do we know if it's in stock? On order? Just a vague interest? That could drive different conversation strategies.
>
> **Appointment** — belongs to a Lead, optionally linked to a specific VehicleOfInterest. Has a purpose: test_drive, showroom_visit, trade_in_appraisal. Has a lifecycle: scheduled → confirmed → completed, no_show, cancelled. And critically — who booked it. AI or human. That's your attribution metric.
>
> **CrmNote** — belongs to a Lead. You said we sync conversation summaries back. So this is the write-back record. Has a type — conversation summary, appointment booked, follow-up. Has a sync status — pending, synced, failed. Because if the CRM sync fails, I need to know."

```
Dealer 1──* Lead
Lead }o──|| LeadSource
Lead 1──* Contact (one primary)
Lead 1──* VehicleOfInterest
Lead 1──* Appointment
Lead 1──* CrmNote
Appointment 0..1──1 VehicleOfInterest
```

> "Now the agent side. This is the part I think most people skip.
>
> The AI isn't a black box — it's a configurable behavior. How does the AI know what to say? You mentioned different lead types get different treatment. So there's:
>
> **AgentConfig** — defines the AI's behavior. The system prompt, the greeting template, the tools it can use (check inventory, book appointment), and the conversation strategy — how aggressively to push for an appointment, how to handle objections, what topics to avoid.
>
> Dealership-specific info — name, hours, address — lives on the Dealer, not on AgentConfig. The agent combines behavior from its config with context from the dealer at runtime. Don't duplicate.
>
> Then **routing**. This is where LeadSource becomes the bridge between the two sides of the model.
>
> **RoutingRule** — maps (Dealer + LeadSource) → AgentConfig. An AutoTrader lead at Dealer X gets AgentConfig A. An OEM lead at the same dealer might get AgentConfig B — different conversation strategy because the intent is different.
>
> Each dealer has at least one default routing rule — the fallback when there's no source-specific rule. I'd put an `is_default` flag on the routing rule.
>
> So the full picture:"

```
Dealer 1──* Lead
Lead }o──|| LeadSource
Lead 1──* Contact (one primary)
Lead 1──* VehicleOfInterest
Lead 1──* Appointment
Lead 1──* CrmNote
Appointment 0..1──1 VehicleOfInterest
Dealer 1──* RoutingRule
LeadSource 1──* RoutingRule
RoutingRule }o──|| AgentConfig
```

> "LeadSource is the bridge. On the CRM side, it tells you where the lead came from. On the agent side, it determines which AI behavior handles it. That's the connection between what the product works with and how it behaves.
>
> This matters because it's not just 'which prompt' — it's the entire conversation strategy. And when you want to improve the AI later, this routing and config structure is what you'll need to experiment with."

---

### Assessment

**What she nailed:**
- Asked clarifying questions to discover every entity — didn't need to be told
- Lead as the opportunity, not the person — figured it out through the first question
- Contact separate from Lead, VehicleOfInterest separate from inventory — both from questions
- CrmNote surfaced from the scenario ("you said we sync summaries back") — with sync status for failed syncs
- Eligibility tracking on the lead — nobody prompted this, she derived it from "we check eligibility"
- Lifecycle states on Lead and Appointment — detailed and correct
- `booked_by` on Appointment — attribution instinct
- VehicleOfInterest availability states — "that could drive different conversation strategies" (connecting data model to product behavior)
- **LeadSource as a first-class entity unprompted** — argued against making it a string ("I'll need to use the source for routing," "for analytics I want to slice by source")
- **Modeled the agent side unprompted** — AgentConfig, RoutingRule, dealer info separated from agent behavior
- **Named LeadSource as the bridge** — "On the CRM side, it tells you where the lead came from. On the agent side, it determines which AI behavior handles it." Connected the two halves of the domain model explicitly.
- "This matters because when you want to improve the AI, this is what you'll need to experiment with" — she's already thinking about Phase 3 while in Phase 1

**Bonus signals:**
- `do_not_contact` on Contact — legal/compliance awareness
- CrmNote `sync_status` — she's already thinking about what breaks (Phase 2 thinking in Phase 1)
- "Different sources mean fundamentally different customer intent" — product thinking embedded in data modeling
- Default routing rule with `is_default` flag — clean fallback pattern
- The (Dealer + LeadSource) → AgentConfig routing is almost exactly how `ClientOrgCampaign` works in the real codebase

---

## Phase 2: Operationalize It

**You:** "When a dealer buys our product, a deal closes in HubSpot. Right now an engineer spends 30-60 minutes getting them live. We're at 40, going to 200. How would you make this zero engineer time?"

> "Okay. A deal closes in HubSpot — that's the trigger. The system takes it from there. Let me think about the stages.
>
> Based on what I designed, here's the pipeline:
>
> **Stage 1: Connected.** HubSpot fires a webhook. We create the Dealer record from HubSpot data — name, CRM type, credentials. Then we validate the CRM connection — not just 'ping the API,' but actually pull data. Can we authenticate? Can we fetch leads? If credentials are bad, the dealer stays in 'connected_failed' and the system alerts. Don't proceed until the CRM is confirmed working.
>
> **Stage 2: Discovered.** Now I pull their historical data — say last 6 months of leads. I'm not looking at individual leads — I'm analyzing the distribution. What sources do they have? AutoTrader, Cars.com, OEM, walk-ins? What's the volume per source? What does a typical lead look like for this dealer?
>
> From this I auto-create the LeadSource entities. Every distinct source in their data becomes a LeadSource.
>
> This also gives me a baseline — I know what to expect when we go live. If this dealer gets 20 AutoTrader leads per week and after go-live we're seeing zero, something's wrong."

**You:** "Good. What about the agent configs?"

> "**Stage 3: Configured.** For each discovered LeadSource, I need to assign an AgentConfig via a RoutingRule.
>
> I'd maintain a library of proven templates — our best-performing AgentConfig for AutoTrader leads, our best for OEM, etc. These are templates that we know convert well because they've been tested across other dealers.
>
> For each LeadSource: if there's an exact match in the template library → assign it automatically. AutoTrader → our proven AutoTrader agent. Done.
>
> If I see a source I've never encountered — something like 'GM Financial Customer Payoff Request' — I don't guess. I flag it for review. The dealer can go live with their known sources while we figure out the edge case. Don't block the entire onboarding for one unknown source, and don't auto-generate an agent that might say the wrong thing.
>
> **Stage 4: Verified.** Before going live, I run simulations. For each configured source, I inject a synthetic test lead and run it through the entire pipeline:
> - Does it pass eligibility?
> - Does the AI send the right first message?
> - If I simulate a customer response, does the conversation make sense?
> - Can it book an appointment?
> - Does the CRM note sync back?
>
> Each configured source gets its own simulation. If any source fails, that source stays disabled — but the others can proceed. I'm not going to block a dealer from going live on AutoTrader because the OEM agent config failed.
>
> **Stage 5: Live.** Enable polling. Real leads start flowing.
>
> The go-live can be autonomous — if all simulations pass, the system flips to live. No human needed for the happy path. For the 90% of dealers that have standard sources, this entire pipeline — HubSpot webhook to live — should be fully automatic.
>
> Each stage is idempotent. If stage 3 fails, I can re-run from stage 3 without re-pulling historical data. Every checkpoint is durable."

**You:** "What about after go-live? 200 dealers, things break."

> "The system has to protect itself.
>
> **Per-dealer monitoring:** For each dealer, track: leads polled, leads enrolled, appointments booked, CRM sync success rate, error rate. I know what to expect from the discovery stage — if this dealer was getting 20 AutoTrader leads per week and suddenly gets zero, something's wrong.
>
> **Auto-disable:** If a dealer's reliability drops below a threshold — error rate spikes, CRM sync starts failing, appointment rate craters — automatically pause their outreach. Don't let broken conversations go out to real customers. Flag it, pause it, alert someone.
>
> **Self-healing:** The most common failure is CRM note sync. Retry queue with exponential backoff. After N failures, dead-letter it and alert. For stuck leads — lead enrolled 24+ hours ago with no CRM note — automated detection and re-enrollment attempt.
>
> **Rollback:** If a dealer needs to go offline — disable polling, pause active journeys, preserve state so we can resume. The dealer goes back to 'configured' state, not deleted.
>
> The goal: the system runs 200 dealers autonomously. An engineer gets involved when the system can't self-heal — which should be rare if the templates are good and the monitoring is tight."

---

### Assessment

**What she nailed:**
- Connected to her Phase 1 model — LeadSources, RoutingRules, AgentConfigs are exactly what gets created
- Named stages with checkpoints (connected → discovered → configured → verified → live) — not a flat list
- **Discovery from historical data** — analyzed source distribution, not just created records. Used it to set volume baselines for monitoring.
- **Deterministic template matching** — proven templates for known sources, exact match
- **Flagged unknowns** — "I don't guess. I flag it." Didn't try to auto-generate for edge cases.
- **Per-source simulation** — not one smoke test, but a simulation per configured source. Failed sources stay disabled, others proceed.
- **Autonomous go-live for the happy path** — no human needed when simulations pass
- **Auto-disable** — reliability drops below threshold → pause outreach automatically. The system protects itself.
- Self-healing with retry queue, dead-letter, re-enrollment
- Rollback to 'configured' state — preserves work, doesn't destroy it
- Volume baselines from discovery — "if this dealer was getting 20 leads per week and suddenly gets zero, something's wrong"
- Idempotent stages — re-run from any checkpoint
- "An engineer gets involved when the system can't self-heal — which should be rare"

**Connection to Phase 1:** LeadSource entities are auto-created from historical data. RoutingRules are auto-assigned via template matching. CrmNote `sync_status` (which she designed in Phase 1) is exactly what the retry queue monitors. She was modeling for operability from the start.

---

## Phase 3: Own It

### Beat 1: The Customer Email

**You:** Read the inventory-first dealer email.

*She reads it. Pauses. Then:*

> "The dealer is proposing a conversation strategy change. Right now: ask for the appointment, then they see inventory in person. They want: show inventory first, then ask for the appointment.
>
> Both strategies have real tradeoffs. Inventory-first might increase appointment quality — the customer knows what they're coming for, so they're more likely to actually show up and buy. But it might decrease appointment volume — if we check and we don't have their exact car, they might disengage before we get them in the door. At least with appointment-first, they come in and the sales team shows them alternatives.
>
> The dealer thinks inventory-first is better. They might be right. But this is a hypothesis, not a fact. I wouldn't just change the prompt.
>
> Here's what I'd do:
>
> A/B test. Same dealer, same lead sources. Half the leads get inventory-first, half get appointment-first. Random assignment, no cherry-picking.
>
> The metric question is important. Appointment set rate is the obvious one — but it's not enough. If inventory-first books fewer appointments but they all show up, it's better. If appointment-first books more but half no-show, it's worse. I need to measure downstream.
>
> So: appointment set rate AND show rate. That's the comparison that actually matters."

**You:** "We don't track show rate."

> "Then I need to build that before I can run this test properly. The CRM should know if an appointment was completed or no-showed — that status exists in my data model. I just need to close the loop and pull that data back from the CRM.
>
> Actually — I'd build show rate tracking first, baseline it for a few weeks on the current appointment-first approach, THEN run the experiment. Otherwise I have no control to compare against.
>
> Don't ship the dealer's request. Don't run the experiment without the right metric. Build the measurement first."

---

### Beat 2: Systematic Optimization

**You:** "200 dealers, 6 months. Dealers constantly have opinions. How do you systematically make the AI better?"

> "Every dealer request is a hypothesis about what would convert better. Some will be right, some will be wrong, and the only way to know is to test.
>
> The system I'd build:
>
> **1. Agent variants as infrastructure.**
> My agent config from Phase 1 needs to support variants. An agent has a base config and one or more experimental variants. When a lead is enrolled, it gets randomly assigned to a variant. The variant ID is tracked on the lead so I can measure per-variant outcomes.
>
> This is a data model extension — I'd add a `variant` concept to the agent config and a `variant_id` to the lead. The routing layer becomes: (dealer, source) → agent config → randomly selected variant.
>
> **2. Metric hierarchy.**
> Not all metrics are equal. I'd define a hierarchy:
>
> - **Response rate** — did the customer reply? Easy to measure, but 'stop texting me' counts as a response. Low-quality signal.
> - **Engagement quality** — did they ask about a car, pricing, scheduling? Better, but hard to define cleanly.
> - **Appointment set rate** — did the AI book an appointment? Good, but intermediate.
> - **Show rate** — did they actually come in? This is where the real value is.
> - **Close rate / revenue per lead** — did they buy? The ultimate metric, but requires DMS integration we don't have.
>
> I'd optimize for the deepest metric I can reliably track. Right now that's appointment set rate. Once I build show rate tracking, I'd switch to that. Close rate is the long-term goal.
>
> **3. Experiment lifecycle.**
> For each experiment:
> - Define the hypothesis ('inventory-first increases show rate')
> - Define the metric and the success threshold
> - Calculate the minimum sample size — how many leads do I need per variant?
> - Run until statistical significance, not 'until it looks good'
> - Document the result — what worked, what didn't, why
>
> **4. Cross-dealer vs per-dealer.**
> Some experiments are universal — 'does suggesting a specific time convert better than open-ended scheduling?' I'd run those across all dealers to get volume.
>
> Some are dealer-specific — depends on their market, their customer base. I'd be careful about generalizing from one dealer's results.
>
> **5. Feedback loop.**
> When dealers ask for something, I don't just say no. I say: 'Let's test it. Here's how we'd know if it works.' That turns dealer feedback into a hypothesis pipeline. They feel heard, we get data, and the best ideas get adopted across all dealers."

---

### Follow-Up: The Measurement Gap

**You:** "You run inventory-first vs appointment-first. Inventory-first has lower appointment rate, but the dealer swears show rate is better. You don't track show rate. What do you do?"

> "I already answered this a bit — but to be explicit:
>
> I don't trust the dealer's perception. Not because they're wrong, but because they're looking at it through anecdotes — 'I feel like more people showed up this month.' That's not data.
>
> I keep both variants running. I build show rate tracking — pull appointment completion status from the CRM. I baseline show rate on the appointment-first variant for 2-3 weeks. Then I compare.
>
> If the data confirms that inventory-first has higher show rate AND the net outcome (appointments × show rate) is better — then inventory-first wins, even with fewer appointments. Revenue per lead is what matters, not raw appointment count.
>
> If the data shows no difference in show rate, then appointment-first wins because it books more.
>
> Either way, the decision is made by data, not dealer sentiment. And this is exactly why you build measurement infrastructure before running experiments — you don't want to be in a position where the experiment is done and you can't read the results."

---

### Assessment

**What she nailed:**
- Immediately recognized the dealer email as a hypothesis with real tradeoffs — didn't hesitate
- Articulated the inventory-first vs appointment-first tradeoff clearly (quality vs volume)
- "I wouldn't just change the prompt" — owner instinct
- A/B test design: random assignment, no cherry-picking, measure the right metric
- "Build show rate tracking first, baseline it, THEN run the experiment" — measurement before experimentation
- "Don't ship the dealer's request. Don't run the experiment without the right metric. Build the measurement first." — crystallized the priorities
- Extended Phase 1 agent model for variants cleanly — variant concept on agent config, variant_id on lead
- Metric hierarchy from response rate to revenue per lead — knows which are noisy vs meaningful
- Statistical rigor — sample size, significance, not "until it looks good"
- Cross-dealer vs per-dealer distinction — results don't always generalize
- "Turns dealer feedback into a hypothesis pipeline" — that's the system, not just process
- Revenue per lead as the real metric even though it's hard — knows the ideal even when settling for the practical
- Follow-up answer was airtight — keep both variants running, build the measurement, decide on data

---

## Meta-Signal

She connected all three phases without being prompted:

- In Phase 1, she modeled CrmNote with `sync_status` — because she was already thinking about what breaks (Phase 2)
- In Phase 1, she modeled agent config with routing — because she said "when you want to improve the AI, this is what you'll experiment with" (Phase 3)
- In Phase 2, CRM note sync failure was the first self-healing scenario — because she'd flagged it in her data model
- In Phase 3, she extended her Phase 1 agent model for variants — the model was designed to evolve
- In Phase 3, she said "build show rate tracking first" — which connects back to Phase 2's operational infrastructure (pulling data from the CRM)

The three phases weren't three exercises for her. They were one system seen from three angles. That's the owner signal.

---

## Overall

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Domain Modeling** | 5 | Discovered all entities through questions, modeled both CRM and agent sides, lifecycle states, eligibility tracking, sync status — already thinking about ops and measurement while modeling |
| **Ops Thinking** | 5 | State machine, idempotency, dry-run, failure modes at each transition, self-healing, per-dealer health, quantified target ("five minutes not sixty") |
| **Product Ownership** | 5 | "That's a hypothesis, not a fact." Articulated tradeoffs, refused to ship without testing. "Build the measurement first." |
| **Quantitative Rigor** | 5 | Metric hierarchy, A/B testing infrastructure, statistical rigor, "baseline then experiment," measurement before experimentation |
| **Model Evolution** | 5 | Extended agent config for variants cleanly. Model was already designed to evolve. |
| **Curiosity** | 4 | Deep clarifying questions for the domain. Could have asked more about dealer context in Phase 3. |
| **Communication** | 3 | Clear and structured, but verbose — takes more time than necessary on some explanations |

**Total: 32/35. Strong Yes.**

She thinks like an owner across every dimension. Her data model anticipates operational needs and experimentation. Her ops design is a state machine with self-healing. Her product instinct is to test, not ship. And she connects all three phases into one coherent system without being prompted.

The thing that separates her from the good candidate isn't just skill — it's instinct. The good candidate catches himself before shipping the feature request. She never considered shipping it. That's the difference between someone who can learn to own a product and someone who already does.
