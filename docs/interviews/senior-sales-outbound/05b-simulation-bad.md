# Simulation: Bad Candidate

**Profile:** 6 years experience. Full-stack engineer at a large company. Strong resume — worked on high-scale systems. Hasn't worked at a startup or owned a product.

**Vote: No (13/35)**

---

## Phase 1: Model the Domain

*After hearing [the scenario](02-cheat-sheet.md#the-scenario-say-this). No questions. Starts writing immediately:*

> "Database schema:
>
> **dealers**
> - id (PK)
> - name
> - address
> - phone
> - crm_api_key
> - created_at
>
> **leads**
> - id (PK)
> - dealer_id (FK)
> - first_name
> - last_name
> - email
> - phone
> - source (varchar)
> - status (enum: new, in_progress, closed)
> - created_at
>
> **vehicles**
> - id (PK)
> - lead_id (FK)
> - year
> - make
> - model
> - vin
>
> **appointments**
> - id (PK)
> - lead_id (FK)
> - vehicle_id (FK)
> - type (enum: test_drive, showroom, trade_in)
> - scheduled_at
> - status (enum: scheduled, cancelled, completed)
>
> **messages**
> - id (PK)
> - lead_id (FK)
> - direction (enum: inbound, outbound)
> - body (text)
> - sent_at"

*No clarifying questions. No mention of contacts, CRM notes, agent config, or lifecycle states beyond the basics.*

**You:** "You jumped straight into columns. A couple things — can a lead have more than one contact person?"

> "Oh, sure. I could add a contacts table. Move the name/phone/email out of leads and into a contacts table with a lead_id foreign key and an is_primary flag."

**You:** "You have source as a varchar on leads. Leads come from AutoTrader, Cars.com, OEM, walk-ins — do different sources need different handling?"

> "I'd handle that in application logic. Like, if source is 'walk_in', skip the outreach. If it's 'AutoTrader', send a different first message. Just conditionals based on the source string."

**You:** "You have a messages table. You mentioned we sync notes back to the CRM — is that the same thing?"

> "I guess the messages are the conversation, and CRM notes would be summaries. I could add a notes table with a lead_id and a body field."

**You:** "What about the AI side? You said different lead types get different treatment — how does the AI know what to say?"

> "That would be in the application code, right? Like, if the lead source is AutoTrader, use prompt A. If it's OEM, use prompt B. An if/else in the service layer."

**You:** "You wouldn't model that in the data?"

> "I mean, I could have a prompts table. But prompts are more of a code concern than a data concern. I'd probably keep them in a config file."

---

### Assessment

**What went wrong:**
- Started with database columns immediately — no domain thinking
- No clarifying questions at all — assumed he understood the domain
- Contact was an afterthought — didn't think about it until prompted
- CRM notes only added when prompted — didn't surface from the scenario
- Lead lifecycle is shallow: "new, in_progress, closed" — missing contacted, engaged, appointment_set, won, lost
- Appointment status missing `no_show` and `confirmed`
- Source is a varchar on leads — no concept of LeadSource as an entity with properties
- "Conditionals based on the source string" — can't think about routing as a configurable system
- No concept of agent configuration in the domain — "that's application code, not data"
- Messages table is wrong — Pam doesn't store individual messages, OOS does
- "If/else in the service layer" for agent routing — hardcoded behavior, not configurable
- No bridge between the CRM and agent sides — because neither side is properly modeled

**Signal:** Thinks in database tables, not domain models. Treats source as a string and agent behavior as code logic — doesn't see either as a first-class domain concept. No curiosity — didn't ask a single question before designing.

---

## Phase 2: Operationalize It

**You:** "When a dealer buys our product, a deal closes in HubSpot. Right now an engineer spends 30-60 minutes getting them live. We're at 40, going to 200. How would you make this zero engineer time?"

> "I'd build an admin panel that gets triggered when a deal closes. It'd pull the dealer info from HubSpot and pre-fill a form — dealer name, CRM credentials, config. Someone reviews it and clicks 'Create Dealer.'
>
> For the AI config, there'd be a dropdown to pick an agent template — like 'Standard Sales' — and text fields for the dealership name and greeting.
>
> Then there's a 'Go Live' button that starts polling their CRM."

**You:** "You said zero engineer time. This still has someone reviewing a form and clicking buttons."

> "Right, but it's faster because the form is pre-filled. Maybe 5 minutes instead of 30."

**You:** "What about the lead sources? Different dealers have different sources — AutoTrader, Cars.com, OEM. How do those get configured?"

> "I'd have a multi-select in the form — pick which sources this dealer uses. Then it creates the routing config for each one."

**You:** "How do you know which sources the dealer has?"

> "The sales team would know that from the sales process. They'd tell us, or we'd ask the dealer."

**You:** "What if something fails? CRM credentials are wrong?"

> "The form would validate the credentials first — call the API and check. If it fails, show an error."

**You:** "200 dealers live. How do you know if one is having problems?"

> "I'd build a monitoring dashboard. Each dealer shows green if working, red if there are errors. Someone checks it periodically."

**You:** "Journeys break — CRM sync fails, leads get stuck. Right now someone runs a script."

> "I'd make the script easier to use. Put it behind a button in the admin panel — 'Re-enroll Lead' — so you don't have to SSH in."

---

### Assessment

**What went wrong:**
- "Admin panel with pre-filled form" — still requires a human for every dealer. Just made the manual process slightly faster.
- No discovery from data — lead sources come from "the sales team would tell us" or a multi-select dropdown. Manual, doesn't scale, error-prone.
- No concept of template matching or auto-assignment — agent config is a dropdown someone picks
- No simulation or verification — just "click Go Live"
- Failure handling: "show an error" — no idempotency, no rollback, no checkpoints
- Monitoring: "dashboard with green/red, someone checks periodically" — reactive, no alerting, no auto-disable
- Broken journeys: "put the script behind a button" — made manual work slightly more convenient, didn't eliminate it
- Never thought about the system bootstrapping itself from data — every step needs human input
- No mention of the system protecting itself — auto-disable, rollback, self-healing

**Signal:** His instinct for every ops problem is "build a UI." The HubSpot trigger becomes a pre-filled form. Source discovery becomes a dropdown. Monitoring becomes a dashboard someone looks at. He's making manual work prettier, not eliminating it. At 200 dealers this means someone's full-time job is clicking buttons and checking dashboards.

---

## Phase 3: Own It

### Beat 1: The Customer Email

**You:** Read the inventory-first dealer email.

> "Yeah, that's a good idea. Customers probably want to know the car is available before driving out there.
>
> I'd update the agent prompt to check inventory first. When the customer mentions a car, Pam would look it up and tell them if it's in stock before asking to book. Should be pretty straightforward — we already have inventory search as a tool.
>
> I'd make it configurable per dealer — a toggle in the admin panel, 'Show inventory before booking.'"

**You:** "How would you know if it's actually better?"

> "We could track appointment rate before and after the change. If it goes up, it's working."

**You:** "What if appointment rate goes down?"

> "Then we'd switch it back. Or make it optional — let dealers choose."

**You:** "One dealer has 15% appointment rate, another has 2%. Same market. What do you do?"

> "Some dealers probably just have better leads. Different customer bases, different markets. The 2% dealer might be in a less active area. Not much you can do about lead quality."

---

### Beat 2: Systematic Optimization

**You:** "200 dealers, 6 months in. How do you systematically make the AI better?"

> "I'd keep track of dealer feedback. When dealers ask for changes, we'd prioritize the most common requests and update the prompts. After each update, we'd monitor the metrics to make sure nothing got worse.
>
> We could also look at conversation logs — find the ones where the AI didn't convert and figure out what went wrong. Maybe build a tool to flag bad conversations automatically."

**You:** "How do you know which prompt changes actually help?"

> "We'd compare before and after. If the numbers improve after a change, it worked."

**You:** "What if the numbers change because of something else — seasonality, lead source mix shifting?"

> "I guess we'd try to account for that. Maybe compare to a similar time period."

---

### Follow-Up: The Measurement Gap

**You:** "You run inventory-first for a month. Appointment rate dropped, but the dealer insists show rate is better. You don't track show rate."

> "If the dealer says show rate is better, they probably know — they see who walks in the door. I'd trust their judgment and keep inventory-first for that dealer.
>
> For the others, I'd probably default to appointment-first since the numbers are better."

---

### Assessment

**What went wrong:**
- Shipped the feature request immediately — no hesitation, no tradeoff analysis
- "I'd update the prompt" — pure implementer response
- Before/after without control groups: "if it goes up, it's working" — doesn't isolate the variable
- "Some dealers just have better leads" — gives up on the variance question without investigating
- Systematic optimization = "collect feedback, update prompts, monitor" — entirely reactive, no experimentation
- "Compare to a similar time period" when pushed on confounds — no concept of control groups or A/B testing
- Trusts dealer sentiment over data: "they probably know" — this is the clearest red flag
- No mention of A/B testing at any point throughout Phase 3
- No curiosity about WHY the metrics differ
- Never questioned the engagement metric, never asked about show rate, never noticed the funnel is incomplete

**Signal:** Pure implementer throughout. Builds what's asked, doesn't question why. Measures before/after and calls it science. Defers to customer sentiment when data is inconvenient. Doesn't have the instinct to test, experiment, or dig into root causes.

---

## Overall

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Domain Modeling** | 2 | Columns first, no questions, agent side is "application code not data" |
| **Ops Thinking** | 2 | Admin panel, manual monitoring, made scripts prettier not automated |
| **Product Ownership** | 1 | Shipped the feature request, no pushback, defers to dealer |
| **Quantitative Rigor** | 1 | Before/after only, no A/B testing, trusts sentiment, gives up on variance |
| **Model Evolution** | 2 | Never needed to extend because model was thin to begin with |
| **Curiosity** | 2 | No clarifying questions, no investigation of variance, accepts at face value |
| **Communication** | 3 | Clear enough, structured, but shallow |

**Total: 13/35. No.**

He's a competent engineer who can build features in a well-structured environment. But this role requires someone who defines the structure. Every answer followed the same pattern: take the input at face value, build the obvious thing, measure what's easy. He never asked "why," never questioned an assumption, never proposed an experiment. The dealer email was the sharpest test — he didn't even pause before saying "I'd update the prompt."

The through-line: he solves every problem by building what he's told — a table, a panel, a prompt change. He never asks what outcome they're trying to drive. That's an implementer, not an owner.
