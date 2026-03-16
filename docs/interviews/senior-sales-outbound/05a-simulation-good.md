# Simulation: Good Candidate

**Profile:** 4 years experience. Backend engineer at a Series B SaaS company. Built integrations and data pipelines. Solid engineer, hasn't owned a product end-to-end before but wants to.

**Vote: Yes (23/35)**

---

## Phase 1: Model the Domain

*After hearing [the scenario](02-cheat-sheet.md#the-scenario-say-this), pauses, then starts:*

> "Okay, let me think about what's in this domain.
>
> The central thing is a **Lead** — a sales opportunity at a dealership. Not the person, the opportunity. A lead belongs to one dealership."

**You:** *Nod.*

> "A lead has a **Contact** — the person. Name, phone, email. Actually — can a lead have more than one contact?"

**You:** "Yes. Primary buyer and co-buyer."

> "Okay, so Lead has multiple Contacts, one is primary. The phone number is on the contact, not the lead — that's what we use for outreach.
>
> Then there's **Vehicles**. The customer is interested in certain cars. Year, make, model, maybe a VIN. One lead could be interested in multiple vehicles."

**You:** "When you say vehicles — is that what the customer wants, or what's on the lot?"

> "Good question. I'd say what the customer wants. Like, 'I want a 2024 Civic.' Whether the dealer has one is a separate question. So this is a VehicleOfInterest, not inventory."

> "You mentioned leads come from AutoTrader, Cars.com, OEM, walk-ins. Is the source just a label, or does it actually matter for how the lead gets handled?"

**You:** "It matters. Different sources mean different customer intent."

> "Then I'd track it on the lead — a source field. Something like 'AutoTrader' or 'OEM' or 'walk_in.'"

*Starts drawing:*

```
Dealer 1──* Lead
Lead 1──* Contact (one primary)
Lead 1──* VehicleOfInterest
Lead has source (string)
```

> "Then **Appointments**. A lead can have appointments — test drives, showroom visits, trade-in appraisals. An appointment has a status — scheduled, cancelled, no-show, completed. I'd also want to know who booked it — the AI or a human — for tracking purposes.
>
> And the **CRM sync** — you said we write conversation summaries back to the dealer's CRM. So there's some kind of note or record we're creating. Let me call it **CrmNote** — has a type, content, and whether it's been synced."

```
Lead 1──* Appointment
Lead 1──* CrmNote
```

> "What about the lead lifecycle? What statuses does a lead go through?"

**You:** "What do you think?"

> "I'd say: open, contacted, engaged, has an appointment... and then eventually won or lost. The CRM probably controls when it's won or lost — the dealer's sales team decides that, not us."

*Pauses. Doesn't mention the agent configuration side.*

**You:** "You mentioned the AI reaches out and has conversations. How does that fit into your model?"

> "Hmm. I was thinking of the AI as sort of... external to this model. Like, it reads the lead and contact, does its thing, and creates appointments and CRM notes.
>
> But you're right — there's probably some configuration. Like, the AI needs to know what to say. Each dealership would have different info — their name, hours, personality. And you said different lead types get different treatment — so there's some kind of routing."

**You:** "What would that look like?"

> "Let me think... An **AgentConfig** entity. It would have:
> - The system prompt — the instructions for how the AI behaves
> - A greeting template — what the first message looks like
> - Which tools the agent can use — like, can it check inventory? Can it book appointments?
> - Conversation strategy — how aggressively to push for an appointment, how to handle objections.
>
> Dealership-specific info — name, hours, address — I'd keep on the Dealer, not on the agent config. The agent config is about behavior, the dealer is about context. At runtime the AI combines both.
>
> Then there's the routing question. AutoTrader leads get this config, OEM leads get that config. I'd have some kind of **RoutingRule** — ties a dealer and a lead source to a specific AgentConfig."

**You:** "You have source as a string on Lead. How does the routing rule reference it?"

> "Hmm. I'd match on the source string. The routing rule would have a source field and a dealer field — look up the rule where dealer matches and source matches.
>
> For defaults, I'd have a rule with a null source — if there's no exact match for that lead's source, fall back to the default for that dealer."

**You:** "Would it make sense for the source to be its own entity instead of a string?"

> "Actually, yeah. Sources like AutoTrader and Cars.com aren't just labels — they have properties. A web lead is different from a walk-in. They have a channel type. And if I make it an entity, the routing rule has a real foreign key instead of matching on a string. That's cleaner.
>
> Let me add **LeadSource** — name, channel type. Lead belongs to a LeadSource. RoutingRule maps (Dealer + LeadSource) → AgentConfig."

```
Dealer 1──* Lead
Lead }o──|| LeadSource
Dealer 1──* RoutingRule
LeadSource 1──* RoutingRule
RoutingRule }o──|| AgentConfig
```

> "Now LeadSource is the bridge between the CRM side and the agent side. A lead came from a source, the source determines routing, routing picks the agent config. That connects the whole model."

---

### Assessment

**What he got right:**
- Lead as central entity — figured out it's the opportunity, not the person
- Contact separate from Lead — asked about co-buyers
- VehicleOfInterest separate from inventory — caught it with a nudge
- CrmNote as a write-back entity — surfaced from the scenario
- Lifecycle states on Lead and Appointment
- `booked_by` on Appointment — thought about attribution
- Agent config with prompt, tools, and conversation strategy
- Separated dealership info from agent behavior — got this on his own
- LeadSource as a first-class entity — got there with a nudge ("would it make sense for source to be its own entity?")
- Saw that LeadSource bridges the CRM and agent sides — "that connects the whole model"

**Where he needed help:**
- Didn't model the agent side until prompted ("how does the AI fit in?")
- Source started as a string — needed a prompt to elevate it to an entity
- Didn't ask many clarifying questions upfront — started designing fairly quickly

**Signal:** Solid CRM domain instincts. Thinks in entities and relationships, not tables. Can model the agent config and routing when directed to think about it — and makes good decisions once he's there (default routing, separating dealer from agent, seeing LeadSource as the bridge). But doesn't naturally see the product holistically — needed nudges to think about both the AI behavior and the source as first-class domain concepts.

---

## Phase 2: Operationalize It

**You:** "When a dealer buys our product, a deal closes in HubSpot. Right now an engineer spends 30-60 minutes getting them live. We're at 40, going to 200. How would you make this zero engineer time?"

> "Okay, so the trigger is a HubSpot deal close. That kicks off an onboarding pipeline.
>
> Based on my model, here's what needs to happen:
> 1. Create the Dealer record from HubSpot data — name, CRM credentials, dealership info
> 2. Connect to their CRM and validate — can we actually pull data?
> 3. Create the LeadSources and RoutingRules
> 4. Set up AgentConfigs
> 5. Verify it works
> 6. Go live — enable polling
>
> Each step should be idempotent — re-running doesn't create duplicates. Upsert on external IDs."

**You:** "You said create the LeadSources. Where do they come from?"

> "Good question. If we have CRM access, we could pull their historical leads and look at the source distribution. Like, pull last 6 months of leads and see: 40% AutoTrader, 25% Cars.com, 15% OEM, 20% other. That tells us which LeadSources to create.
>
> For the AgentConfig — if we know AutoTrader leads, we probably have a standard agent template that works for AutoTrader. So we'd match known sources to existing templates."

**You:** "What if you see a lead source you've never encountered before?"

> "Hmm. I think the safest thing is to flag it. Don't try to guess what agent behavior to use for an unknown source. Create the LeadSource but don't assign an AgentConfig — flag it for someone to review. The dealer can go live with their known sources in the meantime."

**You:** "How do you verify everything works before going live?"

> "I'd run a health check after setup. Trigger a poll, see if leads come back, check that one would pass eligibility.
>
> Actually, a proper simulation would be better — inject a test lead for each configured source, run it through the full pipeline, verify the AI responds correctly. But that's more complex to build. I'd start with credential validation and a basic data check, and build toward full simulation testing."

**You:** "What about once they're live? 200 dealers, things break."

> "I'd want per-dealer health metrics. For each dealer: leads polled, leads enrolled, appointments booked, CRM sync success rate. If a dealer's numbers drop to zero or error rate spikes, that's an alert.
>
> For broken journeys — retry logic with backoff. If CRM sync fails, retry a few times. After max retries, alert someone.
>
> I think you'd also want the ability to auto-disable a dealer if things are really broken — pause their outreach so bad conversations don't keep going out. Then someone investigates."

---

### Assessment

**What he got right:**
- Connected to his Phase 1 model — LeadSources, RoutingRules, AgentConfigs
- HubSpot as the trigger — understood the event-driven framing
- Discovery from historical data — "pull last 6 months and see the source distribution"
- Template matching for known sources — "we probably have a standard template for AutoTrader"
- Flag unknown sources — didn't try to guess, proposed safe handling
- Idempotency — upsert on external IDs
- Per-dealer health metrics and alerting
- Auto-disable for broken dealers — got there when prompted

**Where he fell short:**
- Framed it as a numbered list, not stages with checkpoints — thinks in steps, not a state machine
- Simulation testing was an afterthought ("that's more complex, I'd start with a basic check") rather than a core requirement
- Discovery was reactive — pulled data to see what's there, but didn't think about what the patterns tell you (volume expectations, lead quality signals)
- Auto-disable was the last thing he mentioned, not a core part of the design
- No mention of rollback — what does "go back to safe state" look like?

**Signal:** Gets the core concepts — discovery, template matching, flagging unknowns, monitoring. But treats verification and self-protection as nice-to-haves rather than requirements. Thinks in steps rather than a pipeline with checkpoints and rollback. Would need to grow into building systems that protect themselves.

---

## Phase 3: Own It

### Beat 1: The Customer Email

**You:** Read the inventory-first dealer email.

> "That makes sense. Customers probably do want to know if the car is available before committing to a visit.
>
> I'd... actually, let me think about this. Is this always a good idea?
>
> If we check inventory and the car isn't there, the customer might disengage. But if we just book the appointment, at least they come in and the sales team can show them alternatives. So there's a tradeoff.
>
> I think I'd want to test it. Like, try both approaches — some leads get inventory-first, some get appointment-first — and see which one books more appointments."

**You:** "What metric would you measure?"

> "Appointment set rate. Does one approach book more appointments than the other?
>
> Actually... booking rate alone might not be enough. If inventory-first books fewer appointments but they're higher quality — like, the customer actually shows up — then it might be better. But I'm not sure how you'd track that."

**You:** "We don't track show rate."

> "Yeah, that's a gap. Without show rate, I'd probably go with appointment set rate as the primary metric and try to get show rate tracking built as a follow-up."

---

### Beat 2: Systematic Optimization

**You:** "200 dealers, 6 months in, dealers constantly have opinions. How do you systematically make the AI better?"

> "I'd collect the requests, look for patterns — if 10 dealers ask for the same thing, that's a signal. Then prioritize the changes that affect the most dealers.
>
> For each change, I'd want before/after metrics. What was the appointment rate before the change, what is it after. Give it a week or two to see the impact.
>
> I think building A/B testing into the system would be the right move eventually. Instead of changing the prompt for everyone and hoping it's better, run both versions and measure. That way you know for sure.
>
> For the agent config — I'd need to support some kind of variant or version. Like, 'agent config A' and 'agent config B' run simultaneously and leads get randomly assigned."

**You:** "Would your Phase 1 agent model support that?"

> "Not as I designed it. I'd need to add a concept of variants. The agent config would have a base version and one or more experimental versions. Each lead gets tagged with which version it saw. Then I can compare metrics per version.
>
> That's a data model change but not a huge one — add a `variant_id` to the lead or the journey, and make the agent config support multiple versions."

---

### Assessment

**What he got right:**
- Saw the tradeoff in the dealer email — didn't just ship it
- Got to "I'd want to test it" on his own
- Recognized appointment rate alone isn't enough — intuited that show rate matters
- Before/after thinking as a starting point, evolved to A/B testing
- Could extend his data model for variants — acknowledged the gap and proposed a clean fix

**Where he fell short:**
- Initial instinct was "that makes sense, I'd build it" before catching himself
- Systematic optimization started with "collect requests, look for patterns" — reactive, not proactive
- Didn't think about statistical rigor — sample size, how long to run, generalizability
- Accepted "I'd go with appointment rate" when he knew show rate was the better metric — settled for the available data instead of pushing to close the measurement loop
- Before/after without control groups isn't rigorous (he got to A/B testing but it wasn't his first instinct)

**Signal:** Has the right instincts — can see tradeoffs, gets to testing eventually, can evolve a data model. But his first instinct is to be reactive (collect feedback, ship changes, measure before/after) rather than proactive (design experiments, build infrastructure, close the funnel). He'd grow into the role but would need some coaching on quantitative rigor.

---

## Overall

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Domain Modeling** | 3 | Solid CRM model, agent side needed prompting |
| **Ops Thinking** | 3 | Good concepts (idempotency, health metrics) but thinks in scripts not state machines |
| **Product Ownership** | 3 | Caught the tradeoff, but initial instinct was to ship |
| **Quantitative Rigor** | 3 | Got to A/B testing eventually, settled for available metrics, no statistical rigor |
| **Model Evolution** | 4 | Acknowledged the gap and proposed a clean variant extension |
| **Curiosity** | 3 | Some good questions, some assumptions without checking |
| **Communication** | 4 | Clear, structured, easy to follow |

**Total: 23/35. Yes.**

He's a solid engineer who can think through each problem but doesn't naturally connect them or drive proactively. Each phase was a separate exercise — he didn't link his data model to the ops automation to the measurement system unprompted. He'd be a good hire who ramps into owning the product, but he'd need some guidance early on to think like a full owner rather than a strong IC.
