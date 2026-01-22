# CHEAT SHEET: Senior Pam Core Interview

**Have this open during the interview. Glance at it, don't read it.**

---

## The Question (Paste This in Google Doc)

> **Imagine you're responsible for an AI voice assistant that handles inbound calls for businesses. It's live in production, answering real customer calls every day.**
>
> **We're seeing a problem:** new customers are churning during their evaluation period, and some existing customers report complaints from their end customers. The feedback is vague—"it doesn't feel good," "customers get confused," "it sounds off sometimes."
>
> **You own quality and customer trust across the system.**
>
> **At a high level, how would you design the product, process, and feedback loops so that:**
> - New customers don't churn during onboarding
> - Existing customers stay happy
> - Issues are caught and fixed before they turn into customer complaints?
>
> **Walk me through how you'd think about this end to end.**
>
> *(Take your time. Use this doc to write out your thinking. I'm looking for how you structure the problem, not perfect answers.)*

---

## Your Job During Interview

### Minutes 0-5: SETUP
- Share Google Doc
- Paste question above
- Say: "Use the doc to write out your thinking. I'll read along and might ask follow-ups."

### Minutes 5-20: SHUT UP & LISTEN
- Let them write/talk
- Only speak if they ask you a question → see [03-faq-questions.md](03-faq-questions.md)
- Take notes on what they mention / don't mention

### Minutes 20-50: THREAD-PULL
Pick 3-4 threads based on what they're missing. Use table below.

---

## Thread-Pulling Quick Reference

| **If they didn't mention...** | **Ask this** | **🟢 Great includes** | **🔴 Bad sounds like** |
|-------------------------------|-------------|---------------------|---------------------|
| **Defining the problem** | "What do you think 'doesn't feel good' actually means? How would you figure that out?" | Call transcripts, talk to churned customers, drop-off analysis, separate subjective from objective | "Look at logs", assumes they know |
| **Metrics** | "How would you know if things are actually getting better?" | Leading indicators (sentiment, corrections) + lagging (churn), customer-level + call-level tracking | "Success rate", "satisfaction scores" |
| **Prevention** | "What would you do to prevent bad experiences from happening in the first place?" | Guardrails, tighter defaults, limit edge cases, kill-switches, onboarding expectations | "More testing", only monitoring |
| **Rollout safety** | "How do you roll it out without breaking things for existing customers?" | Feature flags, low-risk cohort first, clear rollback criteria, staged rollout (5%→25%→100%) | "A/B test 50/50", "deploy and monitor" |
| **Continuous improvement** | "How do you make sure quality keeps improving over time, not just this once?" | Auto-surfacing feedback loops, clear ownership, triage process, self-correcting system | "Keep monitoring", "regular reviews" |
| **Customer segments** | "Would you handle a new eval customer differently than a year-old customer?" | Yes—new: more guardrails; existing: more trust, focus on containment | No difference, treats as monolith |

---

## 💀 KILLER QUESTION (Use on strong candidates)

> **"What would you do in the first two weeks—starting Monday—that would immediately reduce risk?"**

**🟢 Great:** Tighten defaults, add kill-switches, reduce surface area, improve fallbacks  
**🔴 Bad:** "Collect data", "need to understand first", ship risky changes

---

## Candidate-Specific Probes

**For candidates with relevant experience (e.g., Yousof @ CallBox):**

After their answer:
- "You did this at [Company]. What actually worked? What didn't?"
- "What would you do differently with a team vs solo?"
- "How would your approach change at 10x scale?"

**Watch for:**
- ✅ Humility, learning, curious about Pam's approach
- ❌ Know-it-all, dismissive, "I already solved this"

---

## Instant Red Flags 🚨

**If you hear 2+ of these → Strong No**

- Buzzword soup ("collect data, build dashboards, iterate")
- No questions, assumes they know the problem
- Overconfident ("just do X")
- Can't say what could go wrong
- Treats production like a playground
- Gets defensive when probed

---

## What to Watch For

### 🟢 Great Signals
- Asks clarifying questions before writing
- Breaks problem into parts (new vs existing customers)
- Mentions prevention, not just detection
- Thinks about blast radius / rollout safety
- Mentions metrics (leading + lagging)
- Customer empathy (talks about their POV)
- Admits gaps / says "I'd need to figure out..."

### 🔴 Bad Signals
- Jumps straight to solution (model, prompt)
- No questions asked
- "Ship and monitor" with no specifics
- Can't articulate what could go wrong
- One-size-fits-all (treats all customers same)
- Vague on measurement
- Overconfident without a plan

---

## Scoring (Pick One)

| Vote | Meaning |
|------|---------|
| **Strong Yes** | Will own it Day 1. Clear systems thinker. Has done this. |
| **Yes** | Solid hire. Some gaps but right instincts. Will ramp fast. |
| **No** | Missing key dimensions. Gaps in judgment. Not ready. |
| **Strong No** | Red flags. Will break production. Fake seniority. |

**Final check:** Would I want to work with this person? (Gut matters.)

---

## After Interview

**Within 5 minutes, write down:**
1. Best thing they said
2. Biggest concern
3. Your vote (Strong Yes / Yes / No / Strong No)
4. Would you want to work with them?

→ Use [04-scoring-debrief.md](04-scoring-debrief.md)

---

## Remember

- **Shut up during Phase 2.** Silence is okay. Wait at least 10 minutes.
- **One No = No Hire.** If you're not a Yes, that's a No.
- **Trust your gut.** Data + gut, not just data.
