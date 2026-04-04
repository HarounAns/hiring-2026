# Pam Screen — AI-First Hiring Pipeline

**Role:** Senior Engineer — New Product (0→1)
**Linear:** [HAR-30](https://linear.app/pam-ai/issue/HAR-30)

---

## Funnel

```
78 LinkedIn applicants
        │
   Stage 0: Pam Call (15 min, async)
        │
   ~15-20 pass
        │
   Stage 1: Async Judgment Call (60 min, async)
        │
   ~5-8 pass
        │
   Stage 2: Live Session (45 min, Haroun)
        │
   ~2-3 pass
        │
   Stage 3: Paid Week (real codebase)
        │
   1 hire
```

---

## Pipeline Stages

### Stage 0: Pam Call

**Owner:** Pam (automated)
**Duration:** 15 min per candidate
**Haroun's time:** ~3 min reviewing top-scored transcripts

| | Detail |
|---|--------|
| **Input** | LinkedIn applicant list (name, phone, email, role applied for) |
| **Process** | Pam calls candidate, asks 2 judgment questions with adaptive follow-ups |
| **Scoring** | Transcript → Claude scores against rubric (1-5 per dimension) |
| **Output** | Scored transcript + Claude summary + pass/soft-pass/fail classification |
| **Pass criteria** | Demonstrated ownership (pushed back on a request with reasoning) + ops thinking (named a specific failure mode and detection method) |
| **Fail criteria** | Can't answer either question, gives generic answers, implementer signals |

#### Questions

**Q1: Ownership filter**
> "Tell me about a time a customer or stakeholder asked for a feature and you didn't build it. What happened?"

Follow-ups (adaptive based on response):
- Surface answer → "What specifically made you push back? What data did you use?"
- Strong answer → "How did the stakeholder react? Did you end up being right?"
- No answer → "Can you think of a time you disagreed with a product decision? What did you do?"

**Q2: Ops thinking filter**
> "You're scaling a product from 40 customers to 200. What's the first thing that breaks and how do you know it's breaking?"

Follow-ups (adaptive based on response):
- Surface answer ("more servers") → "I mean specifically — which component fails first and what's the symptom?"
- Strong answer → "How would you detect that automatically before a customer notices?"
- Great answer → "What would you build in week 1 to protect against that?"

#### Scoring Rubric (for Claude)

| Dimension | 5 | 3 | 1 |
|-----------|---|---|---|
| **Ownership** | Real story of pushing back with evidence/data | Has an example but reasoning is thin | "I always build what's asked" or can't answer |
| **Ops thinking** | Names specific component, failure mode, and detection | General awareness of scaling issues | "Add more servers" or "hire more people" |
| **Communication** | Clear, structured, concise | Coherent but meandering | Rambling, can't land a point |
| **AI awareness** | Notices they're talking to AI, has opinions | Engages naturally | Confused or disengaged |

#### Hidden Signal

The candidate is talking to the product they'd be working on. Do they notice? Do they comment on it? Do they have opinions on how the conversation felt? This is a bonus signal, not a pass/fail criterion — but it's strong context for Stage 2.

---

### Stage 1: Async Judgment Call

**Owner:** Candidate (self-serve) + Claude (scoring)
**Duration:** 60 min (time-boxed)
**Haroun's time:** ~5 min reviewing top submissions

| | Detail |
|---|--------|
| **Input** | Candidate email + Google Doc link with scenario |
| **Process** | Candidate writes their diagnosis, plan, and verification approach in the doc. AI tools fully allowed. |
| **Scoring** | Submission → Claude scores against rubric |
| **Output** | Scored Google Doc + Claude summary |
| **Pass criteria** | Correct (or defensible) diagnosis + proposed measurement + articulated uncertainty |
| **Fail criteria** | Picked an answer without reasoning, no measurement plan, no acknowledgment of what they don't know |

#### The Scenario

> "Here's a dealer's last 30 days of data. Appointment set rate dropped 22%. Three things changed in that period: we updated the greeting template, a new lead source started sending volume, and the dealer changed their business hours in the CRM.
>
> What's your diagnosis, what do you do, and how do you verify you're right?"

Provide: mock data (appointment counts by day, source breakdown, greeting change date, hours change date).

#### What This Tests

AI tools can analyze the data. AI tools can write a coherent narrative. What AI can't do:
- Decide which of the three changes matters most when the data is ambiguous
- Articulate what additional data they'd need to be sure
- Say "I think it's X but I could be wrong because Y"
- Propose a verification plan that doesn't just confirm their bias

---

### Stage 2: Live Session

**Owner:** Haroun
**Duration:** 45 min
**Haroun's time:** 45 min

| | Detail |
|---|--------|
| **Input** | Stage 0 transcript + Stage 1 submission + candidate's resume |
| **Process** | Live Google Doc session — start from their Stage 1 submission, shift the problem every 5 min |
| **Scoring** | Haroun scores using existing 7-dimension framework |
| **Output** | Score card + Strong Yes / Yes / No / Strong No vote |
| **Pass criteria** | Connects domain modeling → ops → product ownership without prompting. Adapts when the ground shifts. |
| **Fail criteria** | 2+ red flags, can't reason in real-time, collapses under challenge |

#### Structure

This is the existing 3-phase interview (domain modeling → operationalize → own it), compressed because you already have signal from Stages 0-1. Key difference: start from their prior work.

1. **Challenge their Stage 1 diagnosis** (10 min) — "You said it was the new lead source. I pulled the data — the greeting change correlates more strongly. Update your diagnosis."
2. **Domain modeling** (15 min) — Phase 1 from existing interview (model the CRM + agent config sides)
3. **Operationalize** (10 min) — "How do you go from 40 to 200 dealers with zero engineer time?"
4. **Product ownership** (10 min) — The dealer email curveball (inventory-first vs appointment-first)

Every 5 minutes, shift the problem. Test clock-speed of reasoning, not depth of preparation.

---

### Stage 3: Paid Week

**Owner:** Candidate + team
**Duration:** 5 days
**Haroun's time:** ~90 min total (check-ins)

| | Detail |
|---|--------|
| **Input** | Real codebase access, real Slack, real ticket |
| **Process** | Candidate works on a genuinely ambiguous ticket. AI tools encouraged. |
| **Scoring** | Did they make the product better in a way we didn't predict? |
| **Output** | Hire / No hire decision |
| **Pass criteria** | "Would I miss them if they left?" |
| **Fail criteria** | Generated plausible-looking code that falls apart under review, didn't ask questions, waited for direction |

#### The Ticket

Should be ambiguous, not spec'd:
> "This dealer's CRM sync is flaky and they're complaining. Figure out what's going on and fix it."

What you're watching for:
- Do they talk to the ops team before diving into code?
- Do they read logs before forming an opinion?
- Do they fix the instance or fix the pattern?
- Do they ask "has this happened with other dealers?" or just solve the one case?
- When they use AI tools, are they directing or following?

---

## Time Budget Per Hire

| Stage | Your Time | Candidates Evaluated |
|-------|-----------|---------------------|
| Stage 0 (Pam) | ~45 min total (reviewing 15-20 transcripts × 3 min) | 78 |
| Stage 1 (Async) | ~30 min total (reviewing 5-8 submissions × 5 min) | 15-20 |
| Stage 2 (Live) | ~2-3 hrs total (3-5 candidates × 45 min) | 5-8 |
| Stage 3 (Paid) | ~90 min (check-ins over 5 days) | 2-3 |
| **Total** | **~5 hrs per hire** | **78 → 1** |

---

## What Needs to Be Built

- [ ] Pam call script with adaptive follow-ups (Stage 0)
- [ ] Claude scoring prompt + rubric (Stage 0 + Stage 1)
- [ ] Mock dealer data for Stage 1 scenario
- [ ] Google Doc template for Stage 1
- [ ] Candidate communication templates (pass/fail emails per stage)
- [ ] LinkedIn applicant export with contact info
