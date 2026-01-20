# Interview Guide: Senior Pam Core Engineer (LLM Reliability)

## Interview Structure

| Stage | Interviewer | Focus | Duration |
|-------|-------------|-------|----------|
| 1. Culture Fit | Haroun | Values, motivation, grit | 15 min |
| 2. Tech Interview 1: "Solve Our Problem" | Haroun | Strategic thinking, LLM reliability at scale | 60 min |
| 3. Tech Interview 2: Pam Core Day-to-Day | Anujan/Juzer | Hands-on ability, debugging, systems thinking | 60 min |
| 4. Closing | Haroun + Samee | Values, feedback, offer | 30-45 min |

**Rule: Everyone must say yes. One no = no hire.**

---

## Stage 1: Culture Fit (Haroun)

Use the standard culture fit interview process.

---

## Stage 2: Tech Interview 1 - "Solve Our Problem" (Haroun)

### Philosophy
This is free consulting. We present our actual problem and see how they think. Bonus points for drawing on real experience.

**We're testing:**
- Aptitude: Are they smart? Do they think well?
- Strategic thinking: Can they frame the problem correctly?
- LLM reliability intuition: Do they have the right instincts?
- Experience: Have they seen this before? (bonus, not required)

### Setup (5 min)

> "I'm going to give you a scenario. I want to see how you think through it. There's no trick—I genuinely want to hear your approach. Feel free to ask clarifying questions."

### The Problem (Present This)

> "Imagine you're working on an AI voice assistant that handles inbound calls for businesses—booking appointments, answering questions, routing calls. It's live and handling real calls at scale, hundreds of customers relying on it every day.
>
> The problem: New customers are churning during their evaluation period because the product 'doesn't feel good.' The hypothesis is it's an LLM quality issue—sometimes the AI says the wrong thing, misunderstands what the caller wants, or gives a response that makes people lose trust.
>
> You're the senior engineer who owns LLM reliability. You have a hypothesis that a change to prompts or model selection could improve things. How do you approach improving the system without breaking it for all the live customers?"

### Let Them Talk (30-40 min)

Don't lead them. Let them drive. Ask clarifying questions if they get stuck:

- "How would you know if the change is actually better?"
- "What's your biggest concern about shipping this?"
- "How would you handle a situation where the change is better for some customers but worse for others?"
- "What would make you confident enough to roll it out to everyone?"

### What Great Looks Like

They should naturally touch on:
- How to measure success (not just vibes—actual metrics)
- How to test safely on real traffic without breaking things
- How to roll out incrementally
- How to know when to rollback
- How to build confidence before full deployment

*Don't prompt for these—see if they get there themselves.*

### What Good Looks Like

- Asks smart clarifying questions
- Thinks about risk and downside
- Has a structured approach, not "ship it and see"
- Draws on past experience if relevant

### What Bad Looks Like

- Jumps straight to "A/B test 50/50"
- No mention of measuring quality
- "Ship it and monitor" without specifics
- Can't articulate what could go wrong
- Overconfident without a plan

### Follow-Up Probes

If they're doing well, go deeper:

**On measurement:**
> "You mentioned measuring quality. How would you actually do that for an LLM? What metrics would you trust?"

**On edge cases:**
> "What if the new version is better on average but significantly worse for a specific type of call—say, Spanish speakers or complex multi-service appointments?"

**On team:**
> "How would you communicate this rollout to the rest of the team? What would you want them to know?"

### Scoring

| Score | Meaning |
|-------|---------|
| Strong Yes | Nailed it. Structured thinking, right instincts, bonus if they've done it before. |
| Yes | Good approach, some gaps, but teachable. Asks good questions. |
| No | Unstructured thinking, "ship and hope" mentality, doesn't consider risk. |
| Strong No | Overconfident, dismissive of the problem, or clearly hasn't worked on production AI. |

---

## Stage 3: Tech Interview 2 - Pam Core Day-to-Day (Anujan/Juzer)

### Philosophy
Can this person actually do the work day-to-day? Debugging, systems thinking, working with our stack.

**We're testing:**
- Skill: Have they done the thing?
- Debugging ability: Can they dig into a problem?
- Systems thinking: Do they understand how pieces fit together?
- Collaboration: Can they work with the team?

### Suggested Areas (Anujan to refine)

**1. Debugging Scenario**
> "A dealer calls and says 'Pam booked the wrong appointment time.' Walk me through how you'd investigate this."

*Looking for:*
- Where do they start? (Logs, call recording, database?)
- Do they ask about context? (Which dealer, when, what did the customer say?)
- Can they trace through a system?

**2. LLM-Specific Debugging**
> "A customer says 'Pam keeps asking me to repeat myself.' What could be going wrong?"

*Looking for:*
- Thinks about: transcription, intent recognition, prompt issues, context window
- Structured approach vs random guessing

**3. System Design (Light)**
> "If you wanted to track how well Pam is handling a new type of call (e.g., tire rotation requests), how would you instrument it?"

*Looking for:*
- Logging, metrics, ability to slice data
- Thinks about what "success" means for this call type

**4. Working with the Team**
> "You find a bug in code someone else wrote. How do you handle it?"

*Looking for:*
- Respectful, collaborative
- Fixes it vs blames them
- Communicates clearly

### Scoring

| Score | Meaning |
|-------|---------|
| Strong Yes | Could debug and ship on Day 1. Clear thinker, has done this before. |
| Yes | Solid fundamentals, would ramp quickly. |
| No | Gaps in debugging or systems thinking. Would need a lot of hand-holding. |
| Strong No | Can't trace through a problem. Surface-level answers. |

---

## Stage 4: Closing (Haroun + Samee)

This is the offer call. We bury the lead—don't tell them they got an offer until the end.

### Structure

**1. Pam Values Overview**
Walk through what it means to work at Pam. Cover our values and what we expect.

**2. Feedback on Their Interview**
- What they did well
- Where they would need to improve / grow

**3. The Offer**
Present the offer after the values and feedback discussion.

---

## Debrief Template

After all interviews, each interviewer fills out:

| Question | Answer |
|----------|--------|
| **Your vote** | Strong Yes / Yes / No / Strong No |
| **Culture fit** | Notes |
| **Aptitude (thinks well)** | Notes |
| **Skill (has done it)** | Notes |
| **Would you want to work with them?** | Yes / No |
| **Biggest concern** | |
| **Biggest strength** | |

**Rule: One No = No Hire. Discuss any disagreements before making a decision.**
