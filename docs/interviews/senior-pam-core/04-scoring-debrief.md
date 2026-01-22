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

- [ ] **Strong Yes** - Will own it Day 1. Hire immediately.
- [ ] **Yes** - Solid hire. Some gaps but right instincts. Will ramp fast.
- [ ] **No** - Not ready for this role. Missing key dimensions.
- [ ] **Strong No** - Red flags. Will break production.

### 4. Gut Check
*Would you want to work with this person?*

- [ ] **Yes**
- [ ] **No**

**If you answered No, your vote should be No regardless of other signals.**

### 5. One Sentence Summary
*If you had to describe this candidate in one sentence to Samee, what would you say?*

```
[Write here]
```

---

## Detailed Scoring Rubric

**Rate each dimension 1-5.**

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Systems Thinking**<br>Do they think in loops, prevention, ownership, continuous improvement? | /5 | |
| **Customer Empathy**<br>Do they segment customers, understand trust dynamics, think from customer POV? | /5 | |
| **Measurement**<br>Do they have leading + lagging indicators, know what to track and why? | /5 | |
| **Risk Management**<br>Are they paranoid about blast radius? Do they have rollback plans? Prevention-first? | /5 | |
| **Execution Bias**<br>Do they have concrete first steps? Bias to action? Pragmatic quick wins? | /5 | |
| **Communication**<br>Is their writing clear, structured, easy to follow? | /5 | |
| **Humility**<br>Do they admit gaps, ask questions, show curiosity? | /5 | |
| **Experience**<br>(Bonus) Have they clearly done this before? | /5 | |

**Total:** _____ / 40

### Score Interpretation

- **32-40:** Strong Yes territory
- **24-31:** Yes territory
- **16-23:** No territory
- **Below 16:** Strong No territory

**But:** Use judgment. One critical dimension at 1-2 can be disqualifying even if overall score is high.

---

## What They Mentioned (Checklist)

**Did they naturally mention these without prompting?**

### Problem Definition
- [ ] Asked clarifying questions before writing solution
- [ ] Wanted to see call transcripts / talk to churned customers
- [ ] Separated objective failure from subjective dissatisfaction
- [ ] Looked for patterns (by customer type, call type, timing)

### Metrics & Measurement
- [ ] Leading indicators (sentiment, corrections, drop-offs)
- [ ] Lagging indicators (churn, complaints)
- [ ] Customer-level metrics (is a specific customer getting worse?)
- [ ] Call-level metrics (which types of calls fail?)
- [ ] Distinguishes "technically correct" from "felt good"

### Prevention (Not Just Detection)
- [ ] Guardrails (things the AI can't do)
- [ ] Tighter defaults for new customers
- [ ] Kill-switches for known bad scenarios
- [ ] Expectation-setting during onboarding
- [ ] Gradual capability expansion

### Rollout Safety
- [ ] Staged rollout with specific percentages (5% → 25% → 50%)
- [ ] Rollback criteria defined upfront
- [ ] Starts with low-risk cohort (new customers, specific segment)
- [ ] Monitors during rollout, not just after
- [ ] Considers segments (not just averages)

### Continuous Improvement
- [ ] Feedback loops that auto-surface issues
- [ ] Clear ownership (who owns what)
- [ ] Triage process (not "fix everything")
- [ ] System becomes self-correcting over time
- [ ] Dashboards that drive action

### Customer Segmentation
- [ ] Treats new eval customers differently than existing
- [ ] Understands trust is cumulative
- [ ] Different risk tolerance for different segments
- [ ] Different goals (zero surprises vs maintain trust)

### Execution
- [ ] Has concrete first steps (not just "understand the problem")
- [ ] Identifies quick wins (tighten defaults, kill-switches)
- [ ] Bias to action (can ship something in Week 1)

---

## Red Flags (Check Any That Apply)

- [ ] **Buzzword soup** - Sounds good but means nothing
- [ ] **No curiosity** - Jumped to solution without questions
- [ ] **Overconfident** - "This is easy, just do X"
- [ ] **No failure mode** - Can't articulate what could go wrong
- [ ] **Production blindness** - Treats prod like a sandbox
- [ ] **Defensive** - Got defensive when probed deeper
- [ ] **Name-dropping** - Dropped companies/tech without substance
- [ ] **Analysis paralysis** - "Need to understand first" with no action bias

**If 2+ red flags → Automatic Strong No**

---

## Threads You Pulled

**Which threads did you pull? What did you learn?**

### Thread 1: [Topic]
**Question asked:**
```
[Write the question you asked]
```

**Their answer:**
```
[Summary]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

### Thread 2: [Topic]
**Question asked:**
```
[Write the question you asked]
```

**Their answer:**
```
[Summary]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

### Thread 3: [Topic]
**Question asked:**
```
[Write the question you asked]
```

**Their answer:**
```
[Summary]
```

**Quality:** ✅ Great / ⚠️ Mediocre / ❌ Bad

---

## Candidate-Specific Notes

**For candidates with relevant experience:**

**What worked at their previous company?**
```
[Notes]
```

**What didn't work?**
```
[Notes]
```

**What would they do differently?**
```
[Notes]
```

**Can they scale from solo to team? (if applicable)**
```
[Notes]
```

**Red flags / concerns:**
```
[Notes]
```

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

### For Anujan/Juzer (Day-to-Day Interview)

**Copy this and send to them:**

```
In my interview, [Candidate Name] [did well / struggled / was unclear] on:
- [Specific area 1]
- [Specific area 2]
- [Specific area 3]

In your interview, test:
- Can they actually debug? (Give them "Pam said the wrong thing" scenario)
- Do they know our stack? (TypeScript, AWS, LLM systems)
- Can you imagine working with them day-to-day?

Red flags to watch for:
- [List any specific concerns]

We're looking for: Could they ship something useful in Week 1?

My vote: [Your vote]
```

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
- **If you're not sure, it's a No.** Default to No, not Yes.
- **Trust your gut.** If something feels off, it probably is.
- **Write notes immediately.** Don't wait—you'll forget details.
