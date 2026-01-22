# FAQ: Clarifying Questions Candidates Ask

**When to use:** Reference this when candidates ask you questions during the interview.

**Your stance:** Be helpful but don't lead them. Answer what they ask, don't volunteer extra.

---

## Question Type 1: Understanding Current State

### Q: "What does the system look like today? What LLM are you using?"

**What to say:**
> "We're using a mix of models. Architecture is standard voice AI—transcription, LLM for intent/response, TTS. It's in production, handling real calls. Assume it's reasonably well-built, not a mess, but also not perfect."

**Why this is good:** ✅ Wants baseline, not jumping to solutions

---

### Q: "What metrics do you track today?"

**What to say:**
> "Basic stuff: call success rate, some satisfaction metrics, support tickets. But honestly, we don't have great visibility into *why* they churn. That's part of the problem."

**Why this is good:** ✅ Wants to know what data exists, not assuming metrics are perfect

---

### Q: "Do you have call recordings? Transcripts?"

**What to say:**
> "Yes, we have recordings and transcripts. Assume you have access to everything—raw data, logs, whatever you need."

**Why this is good:** ✅ Wants qualitative data, not just metrics

---

### Q: "How many customers? What's the scale?"

**What to say:**
> "Hundreds of customers live in production. Thousands of calls per week. This is not a toy system. Changes affect real businesses."

**Why this is good:** ✅ Understanding blast radius, calibrating risk

---

## Question Type 2: Understanding the Problem

### Q: "When you say 'doesn't feel good,' who's saying that—the business owner or the callers?"

**What to say:**
> "Good question. Both. The business owner hears complaints from their customers (callers) and evaluates it themselves during trial. Mix of direct feedback and second-hand complaints."

**Why this is excellent:** ✅✅ Separating end user from decision maker—top 1% thinking

---

### Q: "Is this all new customers or specific types? Industries, use cases?"

**What to say:**
> "We're seeing it across the board, but we haven't sliced the data carefully yet. Could be patterns we're missing. Something you'd want to investigate."

**Why this is good:** ✅ Thinking in segments, not assuming one problem

---

### Q: "How long into eval do they typically churn? Day 1? Week 2?"

**What to say:**
> "Good question. Typically after they've tried it for a bit—maybe 1-2 weeks in. Not immediate, but before they commit to paying."

**Why this is good:** ✅ Timing matters, thinking about customer journey

---

### Q: "Are there customers who aren't churning? What's different about them?"

**What to say:**
> "Yes, plenty convert and stay happy. Great question—comparing churned vs retained would be smart."

**Why this is excellent:** ✅✅ Looking for positive deviance, shows product sense

---

## Question Type 3: Constraints & Resources

### Q: "What's the team look like? How many engineers?"

**What to say:**
> "You'd have 2-3 other engineers, mostly junior. They're smart and can execute, but don't have deep LLM or production reliability experience. You'd be the senior person setting direction."

**Why this is good:** ✅ Understanding resources, thinking about delegation

---

### Q: "Do I have support from leadership? Is this top priority?"

**What to say:**
> "Yes. This is a top priority. You'd have support and time to fix it, but we also need to move with urgency—customers are churning now."

**Why this is good:** ✅ Understanding if they'll be empowered, realistic about needing support

---

### Q: "What's the timeline? Weeks? Months?"

**What to say:**
> "It's urgent, but you have time to do it right. We're not looking for a hack—we want a real fix. But also, every week we're losing customers. Urgency with discipline."

**Why this is good:** ✅ Understanding constraints, balancing speed vs quality

---

### Q: "Can I make product changes, or just technical changes?"

**What to say:**
> "Yes. You own quality and trust, which means you can make product decisions in service of that goal. You'd collaborate with leadership, but you have a seat at the table."

**Why this is excellent:** ✅✅ Understands it's not just a technical problem, wants to own outcome

---

## Question Type 4: Customer Context

### Q: "What do these businesses do? What kinds of calls?"

**What to say:**
> "Varies. Could be appointment booking, answering questions, routing calls. Different industries, different use cases. The AI needs to handle a range of scenarios."

**Why this is good:** ✅ Understanding use case, knows context matters

---

### Q: "Are complaints specific—'wrong answer'—or vague like 'felt off'?"

**What to say:**
> "Mostly vague. 'Doesn't feel good,' 'customers got confused,' 'it sounded off.' We're not getting clear, actionable feedback. That's part of why this is hard."

**Why this is excellent:** ✅✅ Distinguishing objective vs subjective, recognizes vague feedback is harder

---

### Q: "Are there specific call types that fail more? Complex vs simple?"

**What to say:**
> "We suspect so, but we haven't instrumented it well enough to know for sure. That's something you'd need to figure out."

**Why this is good:** ✅ Hypothesis-forming, thinking about edge vs common cases

---

## Question Type 5: Dangerous Questions (Red Flags)

### Q: "What LLM should we use? Is it GPT-4? Claude? What's the prompt?"

**What to say:**
> "Let's not jump to solutions yet. Assume the current setup is reasonable. How would you approach improving things?"

**Why this is bad:** ❌ Jumping straight to solution, no problem definition first

---

### Q: "Can't we just fine-tune a model on good calls?"

**What to say:**
> "Maybe. But how would you approach this more broadly? I'm curious about your thinking, not just one tactic."

**Why this is bad:** ❌ Jumping to specific tactic, no measurement or safety plan, overconfident

---

### Q: "What does the competition do?"

**What to say:**
> "Not super relevant here. Focus on solving the problem for our customers, not copying competitors."

**Why this is weak:** ⚠️ Avoiding the problem, looking for shortcuts

---

## No Questions At All

**If they don't ask any questions and just start writing:**

**What it might mean:**
- ✅ Confident they have enough context
- ❌ Making assumptions without checking
- ❌ Not curious

**What to do:**
- Let them go. See what they write.
- If their answer is full of wrong assumptions, probe later: "You assumed X. Why didn't you ask about that?"

**Watch for:** Are their assumptions reasonable? Do they caveat them? Or confidently wrong?

---

## Quick Reference: Question Quality

| Quality | Examples | What It Reveals |
|---------|----------|-----------------|
| **Excellent** ✅✅ | "New vs existing customers different?", "What do non-churned customers do?", "Can I change product?" | Systems thinker, customer empathy, owns outcomes |
| **Good** ✅ | "What metrics exist?", "Do you have recordings?", "What's scale?" | Wants data, understands context, thinks before acting |
| **Mediocre** ⚠️ | "What's tech stack?", "Timeline?", "Team size?" | Okay but surface-level, task-oriented |
| **Weak** ❌ | "What LLM?", "Can we fine-tune?", "What's the prompt?", "What does competition do?" | Solution-jumping, no curiosity |
| **None** 🤷 | (Doesn't ask, just starts) | Could be confident OR dangerous assumptions—watch their answer |

---

## How to Use This

1. They ask a question
2. Glance at this doc (have it open on another screen)
3. Give them the answer
4. Mentally note: "Good question" or "Red flag"
5. Write in your notes: **"Asked about X"**

**Questions reveal:**
- What they think matters
- What they're worried about
- Whether they jump to solutions or understand first
- Whether they think in systems or tasks
