# Comprehensive Interview Prep Guide

**Position:** Senior Pam Core Engineer (LLM Reliability)

**When to use:** Read this 1 day before the interview (30-45 min read)

---

## Table of Contents

1. [Interview Philosophy](#interview-philosophy)
2. [Interview Structure](#interview-structure)
3. [The Problem Statement](#the-problem-statement)
4. [Deep Dive: The Seven Threads](#deep-dive-the-seven-threads)
5. [Red Flags](#red-flags)
6. [Scoring Framework](#scoring-framework)
7. [Candidate-Specific Strategy](#candidate-specific-strategy)

---

## Interview Philosophy

**This is not a trick question. This is free consulting.**

You want to see:
1. **How they think** (structure, curiosity, depth)
2. **Systems intuition** (loops, prevention, ownership)
3. **Production maturity** (safety, measurement, rollback)
4. **Experience** (bonus if they've done it, not required)

**You're not testing knowledge. You're testing judgment.**

### Why This Format Works

**Shared Google Doc approach:**
- Writing forces clarity (can't hide behind buzzwords)
- You see their process, not just their conclusion
- Async-friendly (matches how your team works)
- Reduces pressure (they're thinking, not performing)

---

## Interview Structure

### Phase 1: Setup (5 min)

Share the Google Doc with them. Say:

> "I'm going to paste a problem into this doc. I want to see how you think through it. There's no trick—this is a real problem we care about.
>
> Use the doc to write out your thinking. You can write bullets, paragraphs, diagrams, whatever helps you think. I'll read along and might ask follow-up questions.
>
> Take your time. I'd rather see how you structure the problem than get a fast answer."

---

### Phase 2: Let Them Lead (10-15 min)

Paste the question (see [The Problem Statement](#the-problem-statement)).

**Your job: SHUT UP.**

Seriously. Don't help. Don't hint. Let them struggle if they need to.

**What you're watching for:**

| **🟢 Great signals** | **🟡 Okay signals** | **🔴 Bad signals** |
|---------------------|--------------------|--------------------|
| Asks clarifying questions before writing | Starts writing immediately | Jumps straight to solution |
| Breaks problem into parts | Has a structured approach | Stream of consciousness |
| Writes clear, organized thoughts | Bullets are coherent | Incoherent or circular |
| Pauses to think | Steady writing | No pauses (not thinking) |
| References customers explicitly | Has a plan | No mention of customers |

**Common mistake:** Jumping in too early because you're uncomfortable with silence.

**Don't.** Wait at least 10 minutes before you say anything, unless they ask you a question.

---

### Phase 3: Thread-Pulling (30-40 min)

Now you read what they wrote and pull threads.

**The art of thread-pulling:**
1. Identify what they mentioned vs what they didn't
2. Pick 3-4 threads to pull (don't try to cover everything)
3. Go deep on those threads to see how they think under pressure
4. Let their answers guide where you go next

**Think of this like a poker hand:** You're watching for tells. Do they get defensive? Do they go deeper? Do they say "good question" and think, or do they bullshit?

---

## The Problem Statement

**Paste this verbatim into the Google Doc:**

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

## Deep Dive: The Seven Threads

### Thread 1: Defining the Problem

**When to pull:**
- They jumped straight to solutions
- They didn't ask what "doesn't feel good" means
- They assumed they know what the problem is

**What to ask:**
> "You mentioned [their solution]. But help me understand—what do you think 'doesn't feel good' actually means? How would you figure that out?"

**Why this matters:**
This tests curiosity and customer empathy. Bad engineers solve the wrong problem confidently. Good engineers are paranoid they don't understand the problem yet.

**What 🟢 Great looks like:**

They say something like:
> "Actually, I'm making assumptions. I'd want to:
> - Listen to calls where customers churned vs stayed
> - Talk to 5-10 churned customers (if they'll talk to us)
> - Review complaints from existing customers—look for patterns
> - Check where new customers drop off during eval (Day 1? Week 2? Specific use cases?)
> - Separate 'objectively wrong' (AI gave wrong info) from 'subjectively off' (tone, pacing, confidence)
>
> I'd look for: Are there specific call types that feel worse? Is it all new customers or a segment? Are complaints about accuracy, tone, or something else?"

**Signals:**
- ✅ Admits they don't know yet
- ✅ Wants qualitative + quantitative
- ✅ Thinks in segments (types of calls, types of customers)
- ✅ Separates objective from subjective
- ✅ Looks for patterns, not anecdotes

**What 🟡 Mediocre looks like:**
> "I'd look at the logs and see where errors are happening. Maybe run a survey."

**What 🔴 Bad looks like:**
> "It's probably the LLM model. Let's just try a better model and see if churn improves."

**Follow-up if they're doing well:**
> "You listen to some calls. What would tell you 'this is the problem' vs 'this is just one bad call'?"

---

### Thread 2: Metrics & Measurement

**When to pull:**
- They haven't mentioned how to measure success
- They said "monitor it" without specifics
- They only mentioned lagging indicators (churn)

**What to ask:**
> "Let's say you implement some changes. How would you know if things are actually getting better?"

**Why this matters:**
"Ship and hope" kills companies. Senior engineers measure before and after. They know what to track and why.

**What 🟢 Great looks like:**

> "I'd track a few things:
>
> **Leading indicators** (real-time, tells us fast):
> - Call sentiment trajectory (does it get worse during the call?)
> - Repeated corrections (caller has to repeat themselves)
> - Escalations / transfers to human
> - Drop-off mid-call
> - Support tickets within 24 hours of a call
>
> **Lagging indicators** (slow, but ultimate truth):
> - New customer churn (conversion from eval to paid)
> - Existing customer complaints
> - NPS / CSAT
>
> **Customer-level** (is a specific customer getting worse?):
> - Per-customer success rate over time
> - Which customers are complaining repeatedly
>
> **Call-level** (which types of calls are bad?):
> - By call type (appointment vs question vs routing)
> - By complexity (multi-step vs simple)
>
> I'd also distinguish between 'technically correct' (AI said the right thing) and 'felt good' (caller was satisfied)."

**Signals:**
- ✅ Leading + lagging indicators
- ✅ Multiple levels (call, customer, system)
- ✅ Thinks about slicing data
- ✅ Understands "correct" ≠ "good"
- ✅ Wants fast feedback

**What 🟡 Mediocre looks like:**
> "I'd track success rate, customer satisfaction, and see if churn goes down."

**What 🔴 Bad looks like:**
> "We'd see if churn improves."

---

### Thread 3: Prevention vs Reaction

**When to pull:**
- They only talk about detecting and fixing issues
- Everything is reactive ("when we see a problem...")
- No mention of designing the system to prevent failures

**What to ask:**
> "You mentioned [detecting/fixing issues]. What would you do to prevent bad experiences from happening in the first place?"

**Why this matters:**
Junior engineers fix bugs. Senior engineers make bugs impossible. This tests if they think about system design for safety.

**What 🟢 Great looks like:**

> "Detection is good, but prevention is better. I'd think about:
>
> **Guardrails** (things the AI can't do):
> - Can't transfer until it confirms the reason
> - Can't book appointment without confirming date/time back
> - Can't give medical/legal advice
> - If confidence is low, must say 'let me get you to someone who can help'
>
> **Tighter defaults for new customers**:
> - Start with narrower scope (only basic appointment booking)
> - Expand capabilities as they mature
> - More conservative behavior during eval
>
> **Onboarding expectations**:
> - Tell customers what it's great at and what it's not
> - Set clear boundaries upfront
>
> **Kill-switches**:
> - If we know a scenario fails, route to human
> - If customer is in eval, route edge cases to human
>
> **Reduce surface area**:
> - Limit what new customers can do until comfortable
> - Gradual feature rollout
>
> The goal: Make it hard for the system to fail in surprising ways."

**Signals:**
- ✅ Thinks in constraints (what it can't do)
- ✅ Different treatment for new vs mature customers
- ✅ Expectation management
- ✅ Escape hatches (route to human)
- ✅ Gradual capability expansion
- ✅ "Make failures impossible" mindset

**What 🟡 Mediocre looks like:**
> "We'd do more testing before we ship. Better QA."

**What 🔴 Bad looks like:**
> "You can't prevent everything. Just need to monitor and fix fast."

---

### Thread 4: Blast Radius & Rollout Safety

**When to pull:**
- They said "A/B test it" without details
- They want to deploy to everyone at once
- No mention of rollback strategy
- Overconfident about no risk

**What to ask:**
> "You want to try [their idea]. How do you roll it out without breaking things for your existing customers?"

**Why this matters:**
This is THE question that separates people who've run production systems from people who haven't. Production veterans are paranoid. Amateurs are confident.

**What 🟢 Great looks like:**

> "I'd roll this out in stages:
>
> **Phase 0: Define rollback criteria upfront**
> - If [metric] drops by X%, we rollback immediately
> - If we get Y complaints in Z hours, we pause
> - One person on-call to make the call
>
> **Phase 1: Low-risk cohort (Week 1)**
> - New customers only (no expectations yet)
> - Start with 5% of that cohort
> - Monitor for 3-5 days
>
> **Phase 2: Expand (Week 2)**
> - If Phase 1 looks good, expand to 25%
> - Still monitoring closely
> - Check: Wins across different call types? Or just specific scenarios?
>
> **Phase 3: Existing customers (Week 3-4)**
> - Start with high-volume customers (more data, faster learning)
> - Gradual: 10% → 25% → 50%
>
> **Phase 4: Full rollout (Week 5+)**
> - Remove feature flag
>
> **Key:** I'd rather go slow and be confident than ship fast and break trust. Watch for 'better on average but worse for a segment.'"

**Signals:**
- ✅ Staged rollout with specific percentages
- ✅ Rollback criteria defined upfront
- ✅ Starts with low-risk cohort
- ✅ Monitors during rollout
- ✅ Thinks about segments (not just averages)
- ✅ Willing to go slow for safety
- ✅ Clear ownership

**What 🟡 Mediocre looks like:**
> "I'd A/B test it. 50/50 split, monitor for a week, roll out if better."

**What 🔴 Bad looks like:**
> "Deploy to everyone and monitor. If there are problems, we'll fix them."

---

### Thread 5: Ownership & Continuous Improvement

**When to pull:**
- They're treating this as a one-time fix
- No mention of how things improve over time
- Vague on who owns what
- "Monitor it" without saying how that leads to improvements

**What to ask:**
> "Let's say you ship this and it works. How do you make sure quality continues to improve over time, not just this one time?"

**Why this matters:**
This tests if they think in systems or just tasks. You're not hiring a task-completer. You're hiring someone to own an outcome.

**What 🟢 Great looks like:**

> "The goal isn't to fix this once—it's to build a system that gets better. I'd think about:
>
> **Feedback loops that auto-surface issues:**
> - Bad calls automatically flagged
> - Weekly report: 'Top 10 worst calls this week'
> - Customer complaints tagged and routed to triage
> - Support has 'Flag this for LLM review' button
>
> **Clear ownership:**
> - One person owns 'voice quality' end-to-end
> - Clear escalation path
> - Weekly sync: What broke? Why? What are we doing?
>
> **Triage & prioritization:**
> - Collect → Cluster (same root cause?) → Prioritize (frequency + impact) → Fix
> - Track: Discovered → Root cause → Fix shipped → Validated
>
> **Make system self-correcting:**
> - Catch issues faster over time
> - Guardrails get tighter as we learn
> - New failure modes added to 'known bad' list
>
> **Dashboards people actually use:**
> - Not just pretty graphs—actionable data
> - Team checks daily
> - Alerts when something gets worse
>
> This isn't a project with a done state. It's continuous improvement."

**Signals:**
- ✅ Thinks in systems, not fixes
- ✅ Auto-surfacing (not manual search)
- ✅ Clear ownership + escalation
- ✅ Triage process
- ✅ Self-correcting over time
- ✅ Dashboards drive action
- ✅ "Never done" mindset

**What 🟡 Mediocre looks like:**
> "We'd keep monitoring metrics and have regular team reviews."

**What 🔴 Bad looks like:**
> "Once it's fixed, we move on to the next problem."

---

### Thread 6: Customer Segmentation

**When to pull:**
- They're treating all customers the same
- No distinction between new and existing customers
- "One size fits all" approach

**What to ask:**
> "You mentioned [their approach]. Would you handle a brand-new evaluation customer differently than a customer who's been with you for a year?"

**Why this matters:**
Customer trust is cumulative. New customers have zero trust—one bad call and they churn. Existing customers have built trust—one bad call is forgivable. Smart engineers treat these differently.

**What 🟢 Great looks like:**

> "Absolutely different.
>
> **New evaluation customers:**
> - High risk, low trust. One bad call and they're gone.
> - More guardrails: Keep it simple, stay in our lane
> - More conservative: If not sure, route to human
> - Faster detection: Flag bad calls immediately, support follows up
> - Expectation-setting: Tell them what it's good at
> - Goal: Zero surprises. Boring and reliable, not impressive and risky.
>
> **Existing customers (1 year in):**
> - Lower risk, high trust. One bad call won't kill them.
> - More flexibility: Advanced features, handle edge cases
> - Focus on containment: Fix before their customers complain repeatedly
> - Goal: Keep trust high, handle issues before escalation.
>
> **Key difference:** New customers need hand-holding and safety. Existing need continuous quality and fast issue resolution."

**Signals:**
- ✅ Clearly distinguishes the two
- ✅ Understands trust is different
- ✅ Treats risk differently
- ✅ Different goals
- ✅ Explains the "why"

**What 🟡 Mediocre looks like:**
> "New customers would get more attention. We'd check in more often."

**What 🔴 Bad looks like:**
> "No, we should treat all customers equally. It's the same product."

---

### Thread 7: The First Two Weeks ⭐

**When to pull:**
Use this on candidates who are doing well to separate the top 1% from the top 10%.

**What to ask:**
> "You've given me a good long-term plan. But what would you do in the first two weeks—like, starting Monday—that would immediately reduce the risk of a customer having a bad experience?"

**Why this matters:**
This tests:
- **Execution bias:** Do they know how to start?
- **Prioritization:** Can they pick the highest-leverage action?
- **Risk reduction instinct:** Do they think about quick wins that reduce downside?

**What 🟢 Great looks like:**

> "First two weeks. I want to reduce risk immediately without breaking things:
>
> **Week 1, Day 1-2:**
> - Get access, understand codebase
> - Listen to 20-30 calls (good and bad)
> - Talk to support: 'Top 3 complaints you hear repeatedly?'
>
> **Week 1, Day 3-5:**
> - **Quick win: Tighten defaults**
>   - Identify top 2-3 scenarios that fail most
>   - Add kill-switches: If we detect these, route to human
>   - Example: Complex multi-service request? Don't try—just transfer
>   - Low-risk (prevents bad) and high-impact (immediate)
>
> **Week 2:**
> - **Improve fallback behavior**
>   - When AI doesn't know, say 'Let me get you to someone who can help' instead of guessing
>   - Clearer error messages
> - **Start customer health visibility**
>   - Even if scrappy: Which customers having most issues?
>   - Quick dashboard: Customer → # of bad calls this week
>
> **Key:** Low-risk, don't need deep codebase knowledge, immediately reduce bad call chance. Buy time for bigger stuff later."

**Signals:**
- ✅ Concrete actions (not "understand problem")
- ✅ Low-risk, high-impact
- ✅ Doesn't require weeks of ramp
- ✅ Bias toward prevention
- ✅ Can ship something by end of Week 1
- ✅ Balances quick wins with long-term

**What 🟡 Mediocre looks like:**
> "I'd meet with team, understand codebase, collect data on issues. Then prioritize and start fixes."

**What 🔴 Bad looks like:**
> "I'd improve the prompt and test a better model. Ship it by end of Week 2."

---

## Red Flags

**If you hear 2+ of these, it's a Strong No regardless of other signals.**

| Red Flag | What it sounds like | Why it's dangerous |
|----------|--------------------|--------------------|
| **Buzzword soup** | "We'd build dashboards, collect feedback, iterate on quality." | Sounds good, means nothing |
| **No curiosity** | Jumps to solution without questions | Will solve wrong problem confidently |
| **Overconfident** | "This is easy, just do X" | Doesn't respect complexity. Will break things |
| **No failure mode** | Can't articulate what could go wrong | Lacks risk awareness |
| **Production blindness** | "Deploy to everyone and monitor" | Treats prod like playground. Will cause outages |
| **Defensive** | Gets defensive when probed | Can't take feedback. Won't collaborate |
| **Name-dropping** | Drops companies/tech without substance | Trying to impress, not think |
| **Analysis paralysis** | "Need to deeply understand first" with no action | Will never ship. Overthinks |

---

## Scoring Framework

### Dimensions (Rate each 1-5)

| Dimension | 5 (Exceptional) | 3 (Solid) | 1 (Weak) |
|-----------|----------------|-----------|----------|
| **Systems Thinking** | Loops, prevention, ownership, continuous improvement | Some systems intuition but gaps | Task-oriented, fixes not systems |
| **Customer Empathy** | Segments customers, understands trust, their POV | Mentions customers but surface | No customer perspective |
| **Measurement** | Leading + lagging, multi-level, knows what/why | Has metrics but generic | Vague or no metrics |
| **Risk Management** | Paranoid about blast radius, rollback plans, prevention | Mentions risk but not deeply | "Ship and monitor" mentality |
| **Execution Bias** | Concrete first steps, bias to action, pragmatic wins | Has a plan but abstract | Analysis paralysis or reckless |
| **Communication** | Clear writing, structured thinking, easy to follow | Coherent but not exceptional | Rambling or unclear |
| **Humility** | Admits gaps, asks questions, curious | Confident but not arrogant | Overconfident or defensive |
| **Experience** | Clear they've done this (bonus) | Smart but learning | Red flags they'll break things |

### Overall Vote

| Vote | Meaning | When to give |
|------|---------|--------------|
| **Strong Yes** | Will own it from Day 1. | 4-5 on most dimensions, especially Systems + Risk + Execution |
| **Yes** | Solid hire, will ramp quickly. | Mostly 3-4's, no 1's |
| **No** | Not ready for this role. | Any 1's in critical dimensions or red flags |
| **Strong No** | Dangerous in production. | Multiple red flags or 1's across board |

### Final Gut Check

After scoring:
1. **Would I want to work with this person?**
2. **Would I trust them to own LLM reliability on Day 1?**
3. **Do I believe they'll hit Month 1 success criteria?**

If answer to any is "No" or "Not sure," your vote is No.

**Remember: One No = No Hire.**

---

## Candidate-Specific Strategy

### For Candidates with Direct Experience

If they've built similar systems (e.g., Yousof @ CallBox):

**After they give their answer, ask:**
> "You've done this at [Company]. What did you actually do when you hit this problem?"

> "What worked? What didn't? What would you do differently with a team?"

> "How did you handle reliability when solo vs with a team?"

**Listen for:**
- ✅ Humility (admits what didn't work)
- ✅ Learning (has grown from experience)
- ✅ Can scale from solo to team
- ✅ Curious about how Pam does it
- ❌ Overconfident ("we solved it perfectly")
- ❌ Dismissive ("I already know")
- ❌ Can't articulate lessons learned

---

## Post-Interview: Immediate Debrief

**Within 5 minutes of interview ending, write down:**

1. **Best thing they said** (the moment you knew)
2. **Biggest concern** (what worries you)
3. **Your vote** (Strong Yes / Yes / No / Strong No)
4. **Would you want to work with them?** (Gut check)

Use [04-scoring-debrief.md](04-scoring-debrief.md) for full template.

---

## Remember

- **Shut up during Phase 2.** Silence is okay. Wait at least 10 minutes.
- **One No = No Hire.** Everyone must say yes.
- **If you're not sure, it's a No.** Default to No, not Yes.
- **Trust your gut.** Data + gut, not just data.
- **Write notes immediately.** Don't wait—you'll forget.

**Good luck. You've got this.**
