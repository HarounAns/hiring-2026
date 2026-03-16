# FAQ: Clarifying Questions Candidates Ask

**When to use:** Reference this when candidates ask you questions during the interview.

**Your stance:** Be helpful but don't lead them. Answer what they ask, don't volunteer extra.

---

## Phase 1: Data Modeling Questions

### Q: "What's a 'lead' exactly — is that the person, or the sales opportunity?"

**What to say:**
> "The opportunity. A lead belongs to one dealership. The same person could submit on AutoTrader for a Honda at one dealer and a Toyota at another — those are separate leads."

**Why this is excellent:** ✅✅ Asking about entity semantics before modeling — exactly right

---

### Q: "Does a lead have one contact or multiple?"

**What to say:**
> "A lead can have a primary buyer and a co-buyer. So multiple contacts, but one is primary."

**Why this is good:** ✅ Discovering entity boundaries through questions

---

### Q: "When you say vehicles — is that what the customer wants, or what the dealership has in stock?"

**What to say:**
> "Both exist, but they're different. The customer has vehicles they're interested in — a make, model, year, maybe a specific VIN they saw online. The dealership has inventory — actual cars on the lot. They're separate concepts. Inventory is a separate service you can query."

**Why this is excellent:** ✅✅ Separating intent from reality — this is the ontology instinct you're testing for

---

### Q: "What happens after an appointment? Can it be rescheduled? No-showed?"

**What to say:**
> "Yes. An appointment can be scheduled, confirmed, completed, no-showed, or cancelled. A customer might reschedule, which creates a new appointment."

**Why this is good:** ✅ Asking about lifecycle states before designing

---

### Q: "What does 'done' mean for a lead? Who decides?"

**What to say:**
> "A lead is 'open' until it's won (bought a car), lost (went elsewhere), or marked dead/inactive. The CRM controls that — the dealer's sales team makes the call, not us."

**Why this is good:** ✅ Asking about lifecycle termination — thinks about end states, not just happy path

---

### Q: "How does the AI know what to say? Is there some kind of config?"

**What to say:**
> "Good question. Each AI agent has a prompt, a personality, a greeting, and a set of tools it can use — like checking inventory or booking an appointment. Different lead types might get handled by different agent configurations."

**Why this is excellent:** ✅✅ Discovered the agent configuration layer through domain reasoning

---

### Q: "Does each dealership get its own AI agent, or is it one for everyone?"

**What to say:**
> "Right now it's mostly one default agent with per-dealer customization — greeting, dealership name, personality tweaks. But different lead sources might warrant different agent behavior."

**Why this is good:** ✅ Thinking about the configuration/customization model

---

### Q: "How does a lead get routed to the right behavior? Is there a campaign concept?"

**What to say:**
> "Great question. Yes — there's a routing layer. The lead's source and type can determine which agent behavior handles it. Right now it's simple but needs to get more sophisticated."

**Why this is excellent:** ✅✅ Intuited the orchestration layer without being told — top signal

---

### Q: "You mentioned syncing back to the CRM — what gets synced?"

**What to say:**
> "Conversation summaries, appointment confirmations, follow-up notes. Basically anything the dealer's sales team needs to pick up where the AI left off."

**Why this is good:** ✅ Discovering CrmNote as an entity through the scenario description

---

## Phase 2: Ops Automation Questions

### Q: "Are all dealers on the same CRM, or do we need to support multiple?"

**What to say:**
> "Right now all on Tekion. But CDK and DealerSocket are coming. Whatever you build should treat the CRM as a parameter."

**Why this is excellent:** ✅✅ Thinking about extensibility — the adapter/abstraction instinct

---

### Q: "How many people do onboarding today? Is it always an engineer?"

**What to say:**
> "Always an engineer. Usually me. There's no ops team for this product."

**Why this is good:** ✅ Understanding the current state before proposing solutions

---

### Q: "What's the most common thing that breaks?"

**What to say:**
> "CRM credentials expiring, polling misconfiguration, leads getting enrolled that shouldn't be, and CRM note sync failures. Roughly in that order."

**Why this is good:** ✅ Wants to know where the pain is before designing the solution

---

### Q: "Is there a staging environment? Can I test without hitting real dealers?"

**What to say:**
> "We have a sandbox CRM adapter. But the line between staging and production is thin. Better separation is part of the job."

**Why this is good:** ✅ Thinking about safety and testing

---

## Phase 3: Own It Questions

### Q: "What's our current appointment set rate? What's the baseline?"

**What to say:**
> "About 8%. Human BDC teams typically do 5-15% depending on source quality."

**Why this is excellent:** ✅✅ Wants a baseline before evaluating — scientific instinct

---

### Q: "Do we track show rate? Do people actually come to the dealership?"

**What to say:**
> "We don't track it yet. That's one of the biggest gaps. We know we book appointments but don't know what happens after."

**Why this is excellent:** ✅✅ Spotted the biggest measurement gap

---

### Q: "How is 'engaged' defined? What counts as engagement?"

**What to say:**
> "Right now, 'the customer replied.' That includes 'stop texting me.'"

**Why this is excellent:** ✅✅ Questions the metric definition — understands metric quality matters

---

### Q: "Is the 8% consistent across all dealers, or is that an average?"

**What to say:**
> "It's an average. High variance — some dealers much higher, some much lower."

**Why this is excellent:** ✅✅ Knows averages hide information — statistical thinking

---

### Q: "How many leads per day does a typical dealer get? Is there enough volume for an A/B test?"

**What to say:**
> "Varies a lot. Big dealers might get 20-30 leads a day, small ones might get 3-5. You'd need to think about whether you test per dealer or pool across dealers."

**Why this is excellent:** ✅✅ Thinking about statistical power — knows volume matters for experiments

---

## Dangerous Questions (Red Flags)

### Q: "What's the tech stack?"

**What to say:**
> "TypeScript, Next.js, Prisma, AWS. But let's focus on the domain for now."

**Why this is a weak signal:** ⚠️ Implementation-focused, not domain-focused. Not disqualifying alone.

---

### Q: "Can I see the current schema?"

**What to say:**
> "I want to see your instinct for how you'd model it, not how we did it."

**Why this is weak:** ⚠️ Wants to copy rather than think. Watch what they do next.

---

### Q: "Is there a PRD I can look at?"

**What to say:**
> "No. You're the product person. What would you build and how would you measure it?"

**Why this is bad:** ❌ Wants to be told what to do — implementer mindset

---

### Q: "What does the dealer want us to build?" (in response to the email in Phase 3)

**What to say:**
> "They told you in the email. The question is what you do with that request."

**Why this is bad:** ❌ Looking for the spec instead of thinking about the problem

---

## No Questions At All

**If they don't ask any clarifying questions and just start designing:**

- ✅ Might mean they're confident and assumptions are good — watch the output
- ❌ Might mean they're not curious — watch for wrong assumptions

**What to do:** Let them go. If their model is built on bad assumptions, probe later: "You assumed X. Why didn't you ask?"

---

## Quick Reference: Question Quality

| Quality | Examples | What It Reveals |
|---------|----------|-----------------|
| **Excellent** ✅✅ | "Is a lead the person or the opportunity?", "How does the AI know what to say?", "Do we track show rate?", "What's the baseline for 8%?" | Domain thinker, scientific instinct, discovers entities through questions |
| **Good** ✅ | "What breaks most?", "Multiple CRMs?", "What's the lead lifecycle?" | Practical thinker, wants context before designing |
| **Weak** ⚠️ | "What's the stack?", "Can I see the schema?" | Implementation-focused, not domain-focused |
| **Bad** ❌ | "Is there a PRD?", "What does the dealer want?", "Can you list the entities?" | Implementer mindset, needs to be told what to do |
